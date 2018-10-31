# Our Security Management history Against Rainbow Tables Attacks

IAAC Recipe : Infrastructure as code is mandatory to evry single opertion on our infrastructure, So any change required by Our Security Policy, Will be waged with using a software, written with a programming language by our security  team ( So they are  `SecOps`, like there are `Devops` ) .
Our Security Team chose `Golang` language.

To tell you all the truth, the present README.md, was generated, commited and pushed by Our SecOps toolchain.
After our SecOps toolchain generated, commited and pushed this `README.md`, our SecOps guys added a few more commits, to include miscellaneous complementary information, like Comments in the table below.
But essentially, they  gety their hands on their Recipe's Git repos.

SecOps are monitored By  Chief Devops Officer (me) : Chief Devops Officer (CDO) make them comply with rules, using good old CI/CD and user permissions classics. The rules he makes them comply with, are classic coding style, exapmple mandatory unit tests mapped to repo issues, plus architecture evolution monitoring involving CDO breaking down code and re-design deep architecture, propagated with SecOps framework updates.


| Security Risk ID | Security Risk Registry ID |  Date team applied recipe (When was executed that Recipe) | IAAC Recipe | Release TAG of Recipe (Which version was executed ?) | hyperlink to Tests results of Recipe's execution | Comments |
| - | - | - | - | - | - | - |
| [`CVE-2006-1058`](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2006-1058) | [`CVE-MITRE`](https://cve.mitre.org) | `Tue Oct 12 13:19:37 EDT 2018` | [A working hyperlink to to your Recipe's URI (Not to Awesome Traefik's github repo :100: )](https://github.com/containous/traefik/wiki/Awesome-Traefik)  | [`0.2.1`](#our-security-management-history-against-rainbow-tables-attacks) | [Tests results](#our-security-management-history-against-rainbow-tables-attacks) of Recipe's execution | We applied on our busybox docker images distribution inside our datacenter's marketplace |
| [`DWF-2012-4284`](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2006-1058) | [`Distributed Weakness Filing`](https://github.com/distributedweaknessfiling/DWF-Documentation) | `Tue Oct 30 14:31:27 EDT 2018` | [A working hyperlink to to your Recipe's URI (Not to Awesome Traefik's github repo :100: )](https://github.com/containous/traefik/wiki/Awesome-Traefik)  | [`0.3.7`](#our-security-management-history-against-rainbow-tables-attacks) | [Tests results](#our-security-management-history-against-rainbow-tables-attacks) of Recipe's execution | blabla quickly describing what we did here  + We love [Kurt Seifried initiave with DWF's](https://github.com/distributedweaknessfiling/) , and his idea of A Risk Regisry conlidation with blockchain techniques, [it's AWESOME!! :D ](https://lwn.net/Articles/679315/) )  |
| [`CVE-2012-2565`](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-2565) | [`CVE-MITRE`](https://cve.mitre.org) | `Tue Nov 17 10:22:02 EDT 2018` | [A working hyperlink to to your Recipe's URI (Not to Awesome Traefik's github repo :100: )](https://github.com/containous/traefik/wiki/Awesome-Traefik)  | [`0.8.1`](#our-security-management-history-against-rainbow-tables-attacks) | [Tests results](#our-security-management-history-against-rainbow-tables-attacks) of Recipe's execution | We upgraded our Bloxx Web Filtering Apppliances to 6.0.x , and  we made it forbidden to any dependency resolver (starting with docker and docker registries) to resolve Bloxx Web Filtering version to less or equal to `5.0.14`) | 

Such a table acts, in our Information System, as a primary key to retrieve all management history, related to a wll identified Risk.

Many more information may be then attached to each primary key, such as those you may read in see this sample [Risk Management table](https://github.com/Jean-Baptiste-Lasselle/the-traefik-experiment/raw/master/counter-measure-1/Sample-ISMS-Risk-Register.xlsx) I downloaded it on October 30 2018) 

For that Sample Risk Management `xlsx` table (oh common, use Linux, please, as A CIO :o ... ), I must tell you that the Queenland's CIO did work on that xslx file, with a very clear goal : HE wants his service, Queenland's Information System, to be ISO 27000 - certified. That xlsx is what he will produce to certification auditors, among other things, so that they decide whether or not, they say OK, you are now officially certified, as a ISO-27 000 compliant Information System.
Or its Queenland's CIO giving every Queenland's entrepreneur help to encourage them toxards ISO - 27 000 certification.



# The final Countdown

Apart from a song I always found ridiculous, but in a sweet fashion, here is on image to make your Boss tell you "do it, NOW"  :

![Do it Now](https://github.com/Jean-Baptiste-Lasselle/the-traefik-experiment/raw/master/counter-measure-1/Clipboard%20-%20October%2030%2C%202018%204_55%20PM.png)

So yeah, It's just right here, Directly on Github, behind your door.
You just never knew.


# Other Risk Registries

(Because one organization alone, cannot be a self sufficent reference, whoever runs it. Or especially thinking about who runs it, and why)

* NIST (National Vulnerability Database) https://nvd.nist.gov/config/cce/index
* And many more : Choose them in the list of country as long as possible, and choose a combination of countries that really can't get along with each other. In those countries, find Security Risk Registries. These will reference different attacks, if you look at Secruity Risk Registries like governements do. Add 7 more countries (sec risk registries), and you're pretty sure you'll end up with something like what we have got in Europe, which some people put in place, against the vote of majority (known as "European Union")  : Something really easy to manage, like sheeps with dogs.
* And many, many more : there exists today, great things, called "Risk Registries Wrappers", such as https://github.com/toolswatch/vFeed . Check that repo, you'll immediatly understand what it consists in. If you need it, know that I am not the only IT guy in the world, automating security updates, based on registry entries (meaning I dont browse or any of my engineers, those registries. Our robots do that for us, and we human, monitor our robots with sweet care).


#### Post Scriptum

As to politics, I want to make it clear to every women and men I will work in the Future : 

A - I will not, under any circumstances, discuss politics at work, and if it is not work, even then I'll just discuss about French politics, and feel  not legitimate to discuss any other countries' politics. I'll do that with French Curtesy, using a refined french chef recipe, should it take a bottle of Taittinger Champagne.  

B - With that Taittinger Bottle, I'll sweetly explain France is my country, so I freely say anything about France, just as much as I do think, that if I travel, work, and live in any foreign country, I will not explain to people there how they should live. I will rather learn, how they live. Then after a cup or two, I'll make my new friends laugh, saying that anyway, if a customer that is not French, cares more about my personal opinions (about France) discussed at the pub, more than about his Kubernetes Clusters, then I seriously doubt he/she has serious IT projects. 

C - All in all, that leaves me with 324 minus one country, so 323 countries. Very much enough to me for IT work. Plus I love foreign languages, learning, and getting to know completely different people! :) 

As simple as DO-RE-MI, remember? 

Not to mention, I have learned pure Mathematics in France, very young, and in a very special context. But I learned everything I know about computer sciences, thanks to those 323 countries. Compared to Mathematics courses I attended very young, French Computer Sciences teaching was very boring, and it's always fun to see those French IT guys faces, when they find out that I learned all they know, plus much more, while they spent their lives saying they don't understand the math I do, and anyway those math are worthless in real life to society.
Too bad, Now I learned what you know, plus much more, and you still will never learn what I know. 
So See u back in France.

As a ground example, I learned everything about PXE booting, out of a 6 hours youtube video from an Indian man. The sound was so low quality, I had to first spend 3 days transcripting every single word he said, pausing the video every 2 minutes, eventually rewinding it back. But that was not enoguh, I had to cross-check all what I thought I had understood in English, with a series of scrennshots of all displayed files in a 6 hours video. 
Then I started to understand redhat's docuementation, could setup some tests, and go fruther with much more Linux knowledge. I ended up understanding jumping to studying what is U-boot, GRUB, LILO, and the conept of a bootloader.

Believe it or not, derypting a secret from a dark Indian video, is much more exicting than expected: I learned that I love being there, where almost no one can help you, and you have to invoke the power of Human Mind, pour [l'honneur de l'esprit humain](https://unspod.unice.fr/video/4799-ja-dieudonne-pour-lhonneur-de-lesprit-humain-les-mathematiques-aujourdhui-apostrophe/).





