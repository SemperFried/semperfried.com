---
layout: post
title:  "Adaptive Best Practices"
date:   2015-11-20 13:28:06
categories: best-practices
---
I've been reading up on best practices lately, not just in software, but in general, and came across Lindsey Dunn's article entitled [Best practices don't matter, here's what does...][best-practices-dont-matter]. The article raises some great points about the blind implementation of best practices and argues for an adaptive culture, citing Toyota's great success, and how they teach the adaptive methods. Now, this may leave some scratching their heads a bit... you may ask what an article in an online hospital review magazine and an automobile manufacturer's decisions about best practices have to do with software development. There are some that will be reading the linked article and in their head, they're bare-chested, swinging their shirts around their heads, and screaming "WOO-HOO!!! THERE'S NO RULES!!!". You guys, put your shirt back on, and all of you bear with me for a moment, there is a point to this.

The quote that struck me the most from the article goes like this:

> "We know we cannot implement perfect processes because, first of all, we are human and humans aren't perfect. Secondly we know that, even if we design a perfect process, the environment will change around that process in unknown and unknowable ways. Therefore, although we work hard to design the best process possible, it is much more important for us to know when our processes fail and then improve them or the environment around them as quickly, simply and easily at the lowest-cost possible."

So, identify process failures, then rapidly implement new 'best practices' to solve them. While on the surface, the article seems to speak against best practices, the point it actually makes is that we can't be blind slaves to them; If something in your process breaks or changes, what you previously thought of as a best practice could end up not being so great after all (it's kind of a "best practice" in and of itself, when you think about it - ironic, huh?). How this relates to software development should be obvious, by now, as this is the essence of the Agile programming model, and a metaphor for the pace at which technology and product life-cycle changes can affect our lives as developers.

Case in point... In 2010, OpenStruct was listed in [Rails Best Practices][rbp-openstruct-2010], and as late as 2013, Ruby devs were singing the praises of [OpenStruct over Hashie::Mash][hashie-considered-harmful]. Of course, by this time people were already starting to [doubt][dont-pass-openstruct-to-controller], and with improvements to the Ruby 2.x codebase in 2015, there's now evidence that POROs constructed with keyword args greatly outperform not only OpenStruct, but Hash as well, prompting at least one dev to make the argument that [you should never, ever use OpenStruct][never-use-openstruct].

Case 2: Everyone remember the [Waterfall model][waterfall]? When software development first became a thing, there was no process model for development cycles, so the Waterfall model was straight-up lifted from production and manufacturing- and for a while, it was the de-facto standard for working on projects in the industry; Although there were naysayers and mutations to the model, it worked, more or less, for a very long time.

Nothing lasts forever, though.

When [Agile software development][agile] was introduced in 2001, its' iterative nature, short timeframes, feedback loops, and instant-gratification feel left a lot of us wondering why we'd ever wasted our time with Waterfall. One of my least-favorite phrases in the English language is 'This is the way we've always done it' (as if that was any justification whatsoever to continue doing something, even when you know that there may be better options available), and Agile seemed to fit my way of thinking to a tee, at the time.

_The 12 Principles of the Agile Manifesto:_

>1. Customer satisfaction by early and continuous delivery of valuable software
>2. Welcome changing requirements, even in late development
>3. Working software is delivered frequently (weeks rather than months)
>4. Close, daily cooperation between business people and developers
>5. Projects are built around motivated individuals, who should be trusted
>6. Face-to-face conversation is the best form of communication (co-location)
>7. Working software is the principal measure of progress
>8. Sustainable development, able to maintain a constant pace
>9. Continuous attention to technical excellence and good design
>10. Simplicity—the art of maximizing the amount of work not done—is essential
>11. Self-organizing teams
>12. Regular adaptation to changing circumstance

Agile wasn't perfect, either, though - there have been many refinements since it was introduced (one might say that this itself fits in with the spirit of Agile, as it's all about responding to changes and quickly adapting accordingly), and even outright challenges to it's assumptions... The [Software Craftsmanship][software-craftsmanship] manifesto is one such response. Nowadays, I tend to be in the middle of this argument - there's no reason why Software Craftsmanship and Agile can't live side-by-side in harmony. "Projects are built around motivated individuals who should be trusted" - why should they be trusted? If a dev devotes him/herself to the rigors of precision, predictability, measurement, risk mitigation, and professionalism, there's no reason to have any doubt. Adaptability is a high mark of professionalism in many organizations (the U.S. Marine Corps is one of these - "Adapt and Overcome" is one of the mantras they drill into you in basic training), and should be viewed as such in the software industry. "Working software is the principal measure of progress"; When one applies a professional mindset (and toolset) for testing and gauging the quality of one's own code, working software is a natural outcome, (and exercising them falls in line with "Continuous attention to technical excellence and good design"). Moreover, applying said disciplines can lead to seeking out more ways to automate existing processes, allowing one to "...maximize the amount of work not done".

So OpenStruct goes from being a best practice to something that's frowned upon as being not only un-performant, but relatively dangerous from a security point-of-view. Waterfall goes from being the only game in town, to being beat out by Agile, which in turn is challenged by the Software Craftsmanship crowd. There's a lesson that we can learn from this (aside from "not using OpenStruct, or Waterfall methodologies") The lesson is this:

>"The best way of doing something now is not necessarily the way it was best done yesterday, and almost certainly not the best way available in the future".

Change is the only constant. Best Practices are good rules to follow (and I'll never argue against them, on the whole) - they help us develop a sense of discipline and professionalism in our daily work, and most often do help us write better code. However, without the ability and willingness to learn new things and adapt to changes in the industry, you'll eventually find your "best practices" will have you practicing the wrong thing.

[best-practices-dont-matter]:      http://www.beckershospitalreview.com/healthcare-blog/best-practices-don-t-matter-here-s-what-does.html
[rbp-openstruct-2010]:   http://rails-bestpractices.com/posts/2010/08/25/use-openstruct-when-advance-search/
[hashie-considered-harmful]: http://www.schneems.com/2014/12/15/hashie-considered-harmful.html
[never-use-openstruct]: http://palexander.posthaven.com/ruby-data-object-comparison-or-why-you-should-never-ever-use-openstruct
[dont-pass-openstruct-to-controller]: http://rubyrailroad.com/2013/06/04/pass-openstruct-or-object-to-controller-from-view/
[software-craftsmanship]: https://en.wikipedia.org/wiki/Software_craftsmanship
[agile]: https://en.wikipedia.org/wiki/Agile_software_development
[waterfall]:https://en.wikipedia.org/wiki/Waterfall_model
