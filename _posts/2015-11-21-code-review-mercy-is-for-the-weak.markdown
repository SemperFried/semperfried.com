---
layout: post
title:  "Peer Review: Mercy is for the weak!!!"
date:   2015-11-20 13:28:06
categories: best-practices code-review
---
Everyone hates to be criticized; this is human nature, and it goes double for developers. It takes a long time to gather the skill-sets required to be successful as a developer, and on the whole, knowing this tends to be quite an ego boost. It's when those egos get threatened and tempers flare out that code review practices can fall by the wayside, often to the detriment of the project. It's easy to want to go easy on the people you get along with the most, those who are like-minded individuals who agree with you on the 'right way of doing things', and be merciless with those you don't. This is an entirely wrong-headed way of going about it. We've all got this ego-monster living in our heads that screams out "WHAT THE F&#% DO YOU KNOW?" on every line of a peer review. Software development, unlike a lot of creative disciplines, is by nature a team effort - you have many devs with different skill-sets working towards the same goal: delivering working software that meets business expectations. If your project is big enough (and most are), chances are no matter how skilled a developer you are, you need everyone on your team to be able to complete your mission. Learning how to keep the ego-monster in check while your code is under review is probably one of the best skills a dev can acquire. Learning how to write a peer-review that's merciless while at the same time respecting your colleague as someone who is most likely your equal and quite possibly even your better at some aspects of programming, is another.

#### A brief divergence into personal history ####
It may surprise a lot of folks to learn that my first experiences with peer-review best-practices came not from software engineering, but from art class. During my Junior and Senior years, I was an A.P. Art student at a high-school that had a reputation for students placing in the highest tier in local, state, and national competitions (who new the art world was so cut-throat?). One of the reasons my schools' art program was so successful was that we had a system for peer-review which we implemented on a weekly basis. We called it 'critiquing', but essentially, it was the same thing; An open discussion on the merits and faults of each student's current project. Egotistical, self-absorbed punk that I was, I despised these things when we first started. No artist likes a critic, and we were no exception. To an artist, a critic is someone who can't do what you do, but gets to decide whether what you do is good or bad, and this is a horrible, horrible thing. As my grades were tied to how well I could give and deal with critiques, however, I was forced to play along. At first, we were apprehensive about hurting each other's feelings (we were artists, after all), and often blew off the critiques as meaningless...


> "I like how you made those happy little clouds look so fluffy."
> 
> _- a quote from one of my high-school art critiques_


... but as we grew more accustomed to the format, the critiques became more brutal, more demanding. We questioned each brushstroke, each line and choice of color. We demanded justification for every image, why we chose the symbols we chose, and why we chose to represent them in the way that we did. What were we trying to say with the piece. Whether or not it was successful in conveying it's message. Whether or not the work looked derivative of another artist, or whether the workmanship was not up to par, whether or not we were reaching above our skill-set, or whether we weren't reaching far enough. Art being a subjective medium, it's true that the critiques were solely opinion-based, and not really defined by a set of metrics, the true value of them wasn't in the critiques themselves, but in teaching us the ways that successful people deal with giving and receiving criticism. Like all the best teachers, my instructors were guiding us to think about our work (and the work of others), utilizing many different perspectives, with the ultimate goal of helping us mould each other into better artists. While professional software development is worlds away from being as subjective a discipline as oil-painting, sculpture, or mixed-media collage, the goals behind peer-reviews in both fields are strikingly similar. The methods for conducting a successful peer-review in both fields are also not as different as one might think.

#### 10 Best-Practices for a successful peer-review: ####

_1. First of all, decide with your team on what should matter._ 

It goes without saying that developers can be a very opinionated bunch. I've had long and heated discussions on whether or not to document one's code; whether commenting helped make the codebase more understandable, or if it cluttered the code and should be scrapped in favor of 'letting the tests be the documentation' (more on that in another post). Before any peer-review takes place, developers should decide on which metrics should be used to gauge code-quality and style; Otherwise, you're just setting yourself up for hours and hours of bickering and in-fighting (none of which will be very productive). Metrics for code-style should be based on what your team is most comfortable with - while there are scientific reasons for keeping your line-length to a certain number of characters, the best-practices advised length of 80 characters may not suit the reality of your team's overall coding style (in PAM/SMS, we compromised at 100 characters, your team's comfort zone may vary). Other metrics, such as those for code-quality and security, may be more strict ([Law of Demeter][law-of-demeter] violations, [Separation of Concerns][separation-of-concerns], [Cyclomatic Complexity][cyclomatic-complexity], [Assignment/Branch/Conditional][a-b-c] ratios, etc..), as these can affect not only the readability and maintainability of the codebase, but can also introduce harmful side-effects. Inclusion of relevant tests (or updating existing tests), should be a requirement, and a show-stopper for any peer-review. Anti-patterns should also be checked for, and rigorously wiped out.
![Peaceful Discourse](/assets/peaceful-discourse.jpg {{| medium}})

_2. Actually pull and run the code._ 

I didn't include this point when I originally wrote this post, but you'd be surprised how many devs will just scan a pr and leave their two cents without ever downloading the branch to run the code locally and make sure it actually does what it says it can. Use your heads, people.

_3. You have the tools, use them!_ 

Code metric tools, such as [RuboCop][rubocop], [RubyCritic][rubycritic], and [Rails-Best-Practices][rails-best-practices], security scanners such as [Brakeman][brakeman] and test-coverage tools like [SimpleCov][simplecov], are an invaluable resource to any reviewer. Most of these tools can be tweaked to your team's specifications for acceptable tolerances, an chances are, you're even using some, if not all, of these sorts of tool in some capacity as part of your continuous integration strategy (we utilize all of the above-referenced tools on our CI server on PAM/SMS). That being the case, it makes perfect sense to run them against code before it's been merged into develop, to avoid running into issues down the line. Using a code-metric tool in the process of a peer-review can also take a little bit of the personal sting out of a review - it's a lot easier to take criticism from a tool that uses a set of rules defined by the team than from one of your co-workers. Best of all, once your team has laid out the foundation for what they expect your code to look like, many of these tools can be automated with a tool like [Pronto][pronto], which can run several different code-metric tools against a pull-request before it's even been read by another set of human eyes. Automated tools should never entirely take the place of human review, however; You or your peer may have a very good reason for doing things the way they did, and the automated tool isn't going to give the a chance to state their case. They may be entirely wrong about that very good reason, but that should be decided by reasonable discussion, and not by rigid adherence to a standard set of rules (see my previous post, [Adaptive Best Practices]({% post_url 2015-11-20-adaptive-best-practices %}) ).

_4. Be merciless and consistent._ 

Don't be afraid to call your colleagues out on something you think is wrong, or if they've violated the code-quality standards, if you find fault, list it - that's the entire purpose of doing a pull-request, to get that sort of information. Peer review that isn't merciless doesn't really help anyone learn all that much, and sparing someone's feelings isn't worth letting bad code-smells into the source. Just as important, though, is to be consistent. If you're going to call someone out on 'method too long', don't call them out on a fifteen-line block and ignore a twenty-line block elsewhere. Be consistent in how you review your peers on the whole, rather than changing up your review-style for folks you get along with, and especially not for those you don't.
This is where automation in the peer-review process can truly shine. Nothing is more merciless and consistent than a well-written linter or code-metric scanner.

_5. Expect/Demand that others do the same to you._ 

Hey, you're not perfect either, and deep down you know it. I know as well as anyone that I'm capable of making mistakes. If I wasn't, I'd have no reason to make a pull-request. They're not for showing off perfect code, they're for correcting and learning from your errors, and using what you've learned to become a better developer. As fast as the software development industry changes, we can all stand to learn something new on a regular basis, so insist that your colleagues have a go at your code with the same merciless attitude as you exhibit in your own reviews. Mercy is for the weak... you're not weak, are you?

_6. Be relevant, be polite, and back up your arguments._ 

This is a best-practice that's useful in any type of discussion, really. I have an old friend who's an astro-physicist, and who sits on the opposite side of the political fence from me (I won't go into details). I cut my teeth on fact-checking and relevance while engaging in lengthy political discussions over social media, as she'd hold my feet to the fire whenever I didn't provide credible research to back up any claims I'd make. It infuriated me plenty, but it also taught me a valuable lesson that I've carried with me into my professional life. The other half of the lesson was keeping in mind that no matter how much we disagreed on something, this was a person I liked, personally, and respected as a highly intelligent individual. The same should hold true in your interactions with your colleagues, while discussing code. Remember, your colleague is not 'as bad as Hitler' for wanting to use a design pattern you disagree with, or leaving a `binding.pry` in their source code, don't treat them as such.
 
 
 
> "Christ people. This is just sh*t.."
> 
> _Don't start a review like this. We can't all be [Linus Torvalds][linus-rant]._
 



In a peer-review, backing up your arguments can take several forms, such as providing links to StackOverflow articles or api references, or running performance tests to compare the old and new versions of the code. Providing evidence that validates your argument is always preferable to providing your opinion.
![The Credible Hulk](/assets/credible-hulk.jpg {{| medium}})

_7. Remember, thou art human..._

We all tend to think we know what's best when it comes to the codebase on our projects, so it's difficult, sometimes, to accept the fact that we might be on the losing side of an argument, that our perception of the right way of doing something may be flawed. This swings both ways in a peer-review session - your review may be based on an old notion of best-practices that may be outdated, and the same might be said for code you've written. It's easy to fall into habits, once you've found something that works, and it can be hard to let go of those habits. Never let your pre-conceived notions stop you from learning from your peers; Remember, these people, in most cases, passed the same vetting process you had to go through to get your job. They're most likely not stupid, and you need to respect that. We should all take the discussions in peer-review sessions as an opportunity to learn and grow as developers, no matter which side of the review that we're on.

_8. Wait for at least two devs to approve your pull-request before merging your code._

Waiting for two or more developers on your team review your code not only gives everyone on your team the chance to go over and familiarize themselves with your changes (thus allowing everyone to better understand the system), but also may provide valuable insight that the first dev who reviewed your code may not possess. Everyone tends to specialize in different areas, and may be better at seeing the strengths and weaknesses of a certain piece of code than others.

_9. Be timely in responding to pull-requests and peer-reviews._

Pull-Requests and peer-reviews only provide value so long as they're responded to shortly after being posted - no matter how good the code is that results from a peer-review, business isn't going to like it if the review process ends up slowing your sprint-cycle down to a crawl. If you're not punctual in both reviewing and responding to review, you're not only holding up the process and annoying folks (not to mention needlessly costing business money, which, as I stated before, they won't be happy with), you're likely allowing the un-merged code to grow stale, as more and more pull-requests are approved and merged into the codebase.

_10. Follow through._

Peer reviews can be a valuable resource for learning, but dissemination of knowledge gained from the peer-review process is important as well. Not all of your team may have participated in any given review due to time-constraints, and valuable information could be slipping through their fingers. Such a loss can lead to other devs making the same mistakes you just corrected through the peer-review process (whichever side you were on). Share the key points of interest in discussions with the rest of your team, and invite others to chime in with any insight they might have, even after the issue is resolved. Chances are you might uncover something that's been affecting some other part of your application, or insights from other team members that may make you reverse decisions made in peer review. Sharing the info, at the very least, can save everyone valuable time by not having to correct the same mistakes over and over again. Following through also means accepting the value given from the criticism and learning from it, by not making the same mistakes in your own code. There's no sin in making a mistake, everyone's capable of that; it's not learning and adapting from those mistakes that's a mortal sin for a developer.

So, just as the goal of our critiques in high-school art class were geared towards making us better artists and improving the quality of our work as a whole, the goal of any peer-review session should be the improvement of the codebase as a whole, and the refinement of all involved into better developers. Big thanks to Karen Fearon-Barr, Susan Sheets, Kathleen Davis, and Dr. Elizabeth Jensen, for lessons learned over the years that I'm still finding value in today.

[law-of-demeter]: https://en.wikipedia.org/wiki/Law_of_Demeter
[separation-of-concerns]: https://en.wikipedia.org/wiki/Separation_of_concerns
[cyclomatic-complexity]: https://en.wikipedia.org/wiki/Cyclomatic_complexity
[a-b-c]: http://c2.com/cgi/wiki?AbcMetric
[rubocop]: https://github.com/bbatsov/rubocop
[rubycritic]: https://github.com/whitesmith/rubycritic
[brakeman]: http://brakemanscanner.org/
[simplecov]: https://github.com/colszowka/simplecov
[pronto]: https://github.com/mmozuras/pronto
[rails-best-practices]: https://github.com/railsbp/rails_best_practices
[linus-rant]: http://lkml.iu.edu/hypermail/linux/kernel/1510.3/02866.html
