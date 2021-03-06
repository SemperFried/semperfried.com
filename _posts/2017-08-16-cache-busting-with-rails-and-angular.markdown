---
layout: post
title:  "Adventures in Cache-Busting with Angular CLI and Rails"
date:   2017-08-16 17:24:47 -0500
categories: ruby rails angular cache-busting fingerprinting
---

If you're anything like me (and chances are, if you've found your way to this site, you are. Gawd help you.), you love making apps with Ruby on Rails apis and Angular front-ends, running as two separate applications, as the man upstairs intended. With your ideal setup, everything to do with the view layer of your application would be handled by Angular, leaving the model and controller to Rails. All minification, fingerprinting, etc... would be handled by webpack and seamlessly integrated into your application. In the real world, however, we don't always get what we want, and sometimes, your beautiful Angular application gets sandwiched into a legacy rails application, and said rails application still relies on sprockets for cache-busting (That is, unless you have Rails 5.1 or above, [built with support for webpack][rails-webpacker]). While this is all well and good for your legacy code (I guess), if your Angular app is built using the angular cli tool, you have the option of using webpack, which bundles support for those super-cool cache-busting hash-fingerprints that sprockets provides when compiling its assets. While the CLI's documentation says this feature is turned on by default, I found the opposite to be true, and my app would generate nothing but the plain-vanilla bundles (booo!). 
![Old busted junk](/assets/webpack-fingerprinting-before.png)

I searched high and low for config options to turn this on, only to find out that 
  1. Most of the [old articles][cache-busting-angular-cli] on the subject were now deprecated since Angular-CLI switched to webpack, and... 
  2. The CLI team had hidden the webpack config by default, (it's not a bug, it's a *[feature][angular-cli-meets-webpack]*) and were not planning on exposing it, at all. The only way you could expose the config was by '[ejecting][eject]' the cli, meaning I'd lose access to all the scripts provided by the cli, and would need to rewrite all my scripts to do without it. No, thank you. 

Luckily, the fix was pretty easy. We run all of our build scripts straight from npm, so most of our scripts are launched from `package.json`. 

I altered our `build:prod` script to use the option `--output-hashing all`...

 {% highlight json linenos %}
{
  ...
  "scripts": {
    ...
    "build:prod": "./node_modules/.bin/ng build --env=prod --base-href /ng2/ --vendor-chunk true --aot false --output-hashing all",
    ...
  }
}
{% endhighlight %}


... and that was half my problem solved. The other half had to do with the Rails template, which was at the time, blissfully unaware of my new fingerprinted files (remember, Rails takes care of this on it's own with sprockets, and I don't want to ditch that yet, due to dependent legacy code.) How do we make the rails app load the correct files? `Dir.entries` and `Rails.root.join()` to the rescue! 

Old busted junk: 
 {% highlight slim linenos %}
     = javascript_include_tag '/ng2/inline.bundle.js'
     = javascript_include_tag '/ng2/styles.bundle.js'
     = javascript_include_tag '/ng2/vendor.bundle.js'
     = javascript_include_tag '/ng2/main.bundle.js'
 {% endhighlight %}



 New hotness: 
 {% highlight slim linenos %}
     = javascript_include_tag "/ng2/#{Dir.entries(Rails.root.join('./public/ng2/').to_s).grep(/inline/)[0] }", type: 'text/javascript'
     = javascript_include_tag "/ng2/#{Dir.entries(Rails.root.join('./public/ng2/').to_s).grep(/styles/)[0] }", type: 'text/javascript'
     = javascript_include_tag "/ng2/#{Dir.entries(Rails.root.join('./public/ng2/').to_s).grep(/vendor/)[0] }", type: 'text/javascript'
     = javascript_include_tag "/ng2/#{Dir.entries(Rails.root.join('./public/ng2/').to_s).grep(/main/)[0] }", type: 'text/javascript'
{% endhighlight %}


Like magic, we now have Rails loading the cache-busting, fingerprinted files we just built in webpack with the angular-cli and npm.

![New hotness](/assets/webpack-fingerprinting-after.png)

I hope this helps someone, it was a pain in the ass to figure it out myself, mainly due to the lack of info on the subject, rather than the degree of difficulty.

[rails-webpacker]: https://github.com/rails/webpacker#installation
[cache-busting-angular-cli]: https://medium.com/@jonnysamps/cache-busting-with-angular-cli-916db52c8db0
[angular-cli-meets-webpack]: https://medium.com/@jeff.boothe/angular-cli-meets-webpack-7c9b1a1e1e89
[eject]: https://github.com/angular/angular-cli/wiki/eject
