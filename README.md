# The Traefik Experiment
_Let's run withcraft_

In this repository, I will test various tutorials found on the web, most referenced by Traefik'officiel site.

Each Release of the present repository, will match a tutorial found on the web

In my work, you find zero docker image reference, either in `Dockerfile`, or in `./dokcer-compose.yml` files. 
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
  * We choose a password, learn it by heart (Is there any difference to writing donw on a paper, or worst, in file... ? :o ). Then use a software to encrypt it. Accurately, this encryption is a one-way cypher, called a HASH. One VERY important thing here, is this : Whatever technical means Digital Ocean will propose, it will have ZERO VALUE in terms of security. Because what matters in security, is how you manage security, not what you did on one given aandom day. For exemple, things that are very important to understand there are :
  * What is hash / One way cyphering ?
  * What are the threats / attacks / vulnerabilites that are managed by this practice of using hashed password ?
  * And about Hashing passwords, I give the answer : A/ Hashing your passwords will protect you against the attacker that gets his hands on the database storing your customers usernames and password B/ It is very important, as of today, to use Hash algorihtm that use SALT, because SALTED HASHED passwords, will protect you against a very well known, and harmful attack, called `Rainbow tables`. Especially in those Kubernetes days, where many more people ahve a scale out platforma freely available.
  
  Managin threats, is what Greatest Generals do. Saying that you will destroy every existing threat around you  is singing ["M-i-c-k-e-y M-o-u-s-e"](https://www.youtube.com/watch?v=PmILOL55xP0)

Okay, now with that we share a more consistent view, let me give you my executive councelor's report : 
Your oprgansiation must have at least one perso, responible of : 
* Writing a first version a table, with two columns, looking like that : 
| Threat Short name & Description | CVE MITRE Threat Reference | What you guys in security did, to protect us agnaist that |
| - | - | - |
| Rainbow tables, attacker able to retrieve our customers' passwords, though there're HASHED, but with no salt |  `75-BAD-0x-4558` | `Tue Oct 30 13:15:09 EDT 2018` => we applied [counter-measure 1](cccc) |



* ccc


