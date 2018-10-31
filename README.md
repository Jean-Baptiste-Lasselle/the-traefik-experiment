# The Traefik Experiment
_Let's run witchcraft_

In this repository, I will test various tutorials found on the web, most referenced by Traefik's officiel website.

Each Release of the present repository, will match a tutorial found on the web

In my work, you find zero docker image reference, either in `Dockerfile`, or in `./docker-compose.yml` files. 
It does matter : 
* If I was to use `latest` tags, or any tag letting environement resolve to different versions, on differents days (What if you read this tutorial on 13 May 2020 ? And what will be tests results, if you run everything in here, on 13 May 2020? ...)
* So I reference EVERY single artifact with **explicit** full version numbers, leaving no choice to dependency resolvers in the dependency manageemnt toolchain. And leaving you with no doubt on : 
  * what I did, 
  * why  I did it,
  * what were my tests results,
  * understand how I build proof-backed analysis for my customers, to give them control on their IT strategy, instead of letting them understand it's just too complex, they just have to trust me, and if something wrong, you just fire the IT guy and pay the hard price for the mess.

## List of scanned tutorials

* [RELEASE `0.0.1`]https://www.digitalocean.com/community/tutorials/how-to-use-traefik-as-a-reverse-proxy-for-docker-containers-on-ubuntu-16-04


## Withcraft RELEASE `0.0.1`

So here I scan https://www.digitalocean.com/community/tutorials/how-to-use-traefik-as-a-reverse-proxy-for-docker-containers-on-ubuntu-16-04

Following this tutorial's instruction I :
* skipped the installing Traefik on bare Ubuntu, and chose to use Traefik's official image, in a simple docker-compose environment. I therefore started with setting up that environment, and then transposed every single [Digital Ocean's tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-traefik-as-a-reverse-proxy-for-docker-containers-on-ubuntu-16-04) steps to that docker-compose environment 


### Transposition of all tutorial's steps (Maestro, Let's start playing)

ccc

#### Step 1 — Configuring and Running Traefik

* To begin with, Digital Ocean's instructs us to secure Traefik's first user ' access. Here's how they propose doing that : 
  * We choose a password, learn it by heart (Is there any difference to writing donw on a paper, or worst, in file... ? :o ). 
  * Then use a software to encrypt it. Accurately, this encryption is a one-way cypher, called a HASH. One VERY important thing here, is : Whatever technical means Digital Ocean (or anyone else) will propose, it will have ZERO VALUE in terms of security. Because what matters in security, is how you manage security, not what you did on one given random day. For example, things that are very important to understand there, are :
  * What is hash / One way cyphering ?
  * What are the threats / attacks / vulnerabilites that are managed by this practice of using hashed password ?
  * And about Hashing passwords, Let me give the answers : 
    A - Hashing your passwords will protect you against the attacker that gets his hands on the database storing your customers usernames and password 
    B - It is very important, as of today (2018), to use Hash algorihtms that use SALT, because SALTED HASHED passwords, will protect you against a very well known, and harmful attack, called `Rainbow tables`. Especially in those Kubernetes days, where many more people have access to a scale out platforma freely available. Hackers able to spin up a proper Kubernetes and take advantage its scale out power, arelike 10 in the world today (o we know exactly who they are and they know we know), but that will drastically change in 4 to 5 years.

Before diving into Bourne again shell, and for the reader who really needs to know what he is doing, and why, I want to invite you to the [ANNEX A. Security: one step higher](#security-one-step-higher) section, a the bootom of the present `README.md` . And also because I like to think that Great Ideas directly come from the very earth ground (Remember what they told Einstein? "You bro really a bit of a dim wit, just take care of the clocks and be a goodboy, okay?" Albert : "Okay."). 

Now Let's work with Jason legacy.

_CHOOSING A PASSWORD_

I'll choose `mickeymouse`, a very bad security choice, for the sake of this example

_CHOOSING A HASH ALGORITHM_

There it's just like at mall, you just have so many choice, it's dismaying... And that is where our one step higher discussion is useful (or merely saving our asses) :  We know how to choose it, it must be a salted one. Plus we will choose a refrence, meaning if SSL/TLS considers a HASH Algorithm seciure enough, I will consider that HASH algorithm secure enough. Actually, I'll push just a bit ahead: I'll alaways choose a HAS Algorithm STRICTLY STRONGER, than the weakest considered secure by SSL/TLS standard. I chose the SSL/TLS protocol as a reference, because SSL/TLS is mmassibvely use, so i trust it is massively tested (plus I checked that it is).
Okay, today, recommended SSL/TLS version is TLS v1.2. And TLS v1.2 requires at least SHA256 (meaning SHA 128 => no way, in your dreams), so I'll choose SHA 512, with SALT.
And this choice wil have to be reviewed once a month at least (if th he SecOps are not happy with that: Hey , guys, it just means checking if SSL/TLS standard has released a new version, and if so, finding in the docuement, which  is the weakest Algorithm considered secure... 2 hours a month on worst case, including updating ISO 27 000 reports that I automated in the SecOps Framework...!)













# ANNEX A. Security: one step higher

## A 4 lines sum-up of how leaders deal with security risks 

  Managing threats, is what Greatest Generals do. Saying that you will destroy every existing threat around you  is singing ["M-i-c-k-e-y M-o-u-s-e"](https://www.youtube.com/watch?v=PmILOL55xP0) :
  Come to terms with it, there is no zero threats security zone anywhere in the world, shoudl it be in your President's office, or in your Queen's Bed. [Managing Threats is wise](https://en.wikipedia.org/wiki/ISO/IEC_27001), and wise Generals get Victory.

## A peek on what I concretely deliver to my customers when it comes to global security strategy


> Your organisation must have at least one person, responible of : 
>
> * Every day try and find a match between [entries in a Security Risk Registry related to Rainbow tables](https://github.com/Jean-Baptiste-Lasselle/the-traefik-experiment/tree/master/counter-measure-1), and a pair `{A, B}`, where :
>   * `A` is a software or software dependency. Like a plugin a library, all kinds of vocabulary varying from one software to the other. Pretty much anything that has a source code. 
>   * `B` is a version number of `A`, and `A` is deployed to production (inside your Information System) in version `B`.
> 
> Bear in mind here, that I do recommend that your Security guys do that work, not only on things that are TODAY delivered to customers, or deployed to production, but to things that WILL be delivered to your customers, or deployed to production, as well. 
> 
> Make them do that work on software at the earliest stage: when developers start commit & push source code to Git. There are plenty of tools making that possible today. New security risk related to Rainbow Tables thrreatening the company Information System: Security Risk identification. Security Team members will use every single methodology they have learned atschool and at work, same with tools, to do dig up security risks everyday. 
> * Every week review the tables, and assess Risk Management **improvement**, regarding Rainbow tables Security Risk. The per-week frequency HAS to be changed, so your company constantly adapt, like species do (Darwin).
> > Again, what is important is not Assessing Risk Management on any given particular day. No, what is important is assessing Risk Management improvement, just like a physics scholar will explain you, that at any given instant, it does not matter what your speed value is, what does matter is its derivative, the acceleration. In IT, what matter far above **anything**, is time. Nothing else, but time. And acceleration makes you earn time over your conccurrent. 
> * Eventually, you will demand Security team to comply with an ISO 27 000 kind of review cycle on every identified risk, using [Security Risks Registries], and devops-like systematic practices ([SecOps](https://github.com/Jean-Baptiste-Lasselle/the-traefik-experiment/tree/master/counter-measure-1) ). Then you will unleash ISO 27 000 auditors on them.

Just between the two of us (you, dear reader), I'll add :
Time, is what matters, remember that (of course I alsothought of good old [computability theorems], along with so many other things).








