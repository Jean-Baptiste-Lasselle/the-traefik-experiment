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

Now Let's work with The Jason Legacy.

_CHOOSING A PASSWORD_

I'll choose `mickeymouse`, a very bad security choice, for the sake of this example

_CHOOSING A HASH ALGORITHM_

There it's just like at mall, you just have so many choice, it's dismaying... And that is where our one step higher discussion is useful (or merely saving our asses) :  We know how to choose it, it must be a salted one. Plus we will choose a reference, which will provide us with a reference over time. The refrence I'll choose is a standard, SSL/TLS's. We ARE NOT setting up SSL/TLS for Traefik provisioning, we are using a standard, to assess how strong our HASH algotrihtm is, compared to what is standard to some people (a few). 

Meaning if SSL/TLS considers a HASH Algorithm secure enough, I will consider that HASH algorithm secure enough for my customer. Actually, I'll push just a bit ahead: I'll alaways choose a HASH Algorithm STRICTLY STRONGER, than the weakest considered secure by SSL/TLS standard. I chose the SSL/TLS protocol as a reference, because SSL/TLS is massively used, so i trust it is massively tested (plus I checked that it is) and approved de facto.
Today, recommended SSL/TLS version is TLS v1.2. And TLS v1.2 requires at least SHA256 (meaning SHA 128 => no way, in your dreams), so I'll choose SHA 512, with SALT.

This choice wil have to be reviewed once a month at least (if th he SecOps are not happy with that: Hey , guys, it just means checking if SSL/TLS standard has released a new version, and if so, finding in the docuement, which  is the weakest Algorithm considered secure... 2 hours a month on worst case, including updating ISO 27 000 reports that I automated in the SecOps Framework...!)
Now, let's check if Digital Ocean's suggestion complies with my requirements.

```bash
# 1. Digital Ocean advises use the htpasswd utility to create this encrypted password
# `htpasswd` is in apache2-utils package
sudo apt-get install apache2-utils

# 2. et voici comment Digital Ocean propose de crypter notre mot de passe
# Here is hwow Digital Ocean advises you to hash your paswords
export VOTRE_CHOIX_DE_MOT_DE_PASSE=mickeymouse
htpasswd -nb admin $VOTRE_CHOIX_DE_MOT_DE_PASSE

# 3. 
```
Okay, let's google, `How to SHA-512 with htpasswd` ... Ouch, I am afraid htpasswd does not support SHA-512, even worst, it does not even support SHA-256... Meaning idf Digital Ocean 's customer folow their instructions, well, let's say they are sheeps swiming in a room full of wolves.
Let Digital Ocean deal with their customers, and get back to our customer.Right, So dgitial Ocean's htpasswd suggestion for securing Traefik: forget aboput it, let's find somethign better.
Google again, and soon, you find Most Llinux distribution include utilities such as `sha512sum` , or `sha394sum` ... And there, we're talking about packages include in most respected Linux distributions, like Redhat's or OpenSUSE. And believe me, Redhat guys' tests are rock solid. Actually, Linux is Rock Solid.
Those utilities are there because Redhat guys did the same security analysis as I just did, leading to the exact same unavoidable conclusion. You've ever heard about the `KISS` principle (I am think about coming out with a French KISS principle)? Well if you've never heard about it, just see it in action :

```bash
# 1. Digital Ocean advises use the htpasswd utility to create this encrypted password
# `htpasswd` is in apache2-utils package
sudo apt-get install apache2-utils

# 2. et voici comment je recommanderai à mon client de hacher ses mots de passe.
#     And here is how I recommend my customer to HASH his Traefik users passwords : 
export VOTRE_CHOIX_DE_MOT_DE_PASSE=mickeymouse
sha512sum $VOTRE_CHOIX_DE_MOT_DE_PASSE
```
Guess what, ever came across an ISO file ? Well here is how you check an ISO's integrity, using its "footprint"  :
* First you download the ISO file, say `your-iso-file.iso`, plus another small text file that extension like `*.SHA512`, say `your-iso-file.iso.sha512.sum` etc..

```bash
sha512sum your-iso-file.iso
```
Then the integrity test is OK iff the big string output by the above command, is exactly equal to the string in `your-iso-file.iso.sha512.sum`. Just a simple as that. And that a one way cyphering => you can't retrieve the actual `your-iso-file.iso`, neither from the string in `your-iso-file.iso.sha512.sum`, nor from the ouput string of the `sha512sum your-iso-file.iso`. Well you 'll tell me given file size, it wouldn't occu to your mind, totry and retrieve a full iso from a 3Ko texte file. Well I'll answer you that is just a size matter, and if yo had used RSA intead of SHA512, then yeah, you would have been able too, only difference would then be text file size, and complexity of converting text to binary (isn't that what constantly do with HTTP??).

.. Or just let me quote CentoOS project's official documentation : 

> Go to the directory where you downloaded the ISO in a command prompt and type:
> 
> sha256sum <name>.iso
> 
> Where <name> is the specific ISO you downloaded. For example in CentOS 6.5, for the minimal iso, it would be:
> 
> ```bash
> [jhughes@jhughes x86_64]$ sha256sum CentOS-6.5-x86_64-minimal.iso
> f9d84907d77df62017944cb23cab66305e94ee6ae6c1126415b81cc5e999bdd0  CentOS-6.5-x86_64-minimal.iso
> ```
> You would compare the hash received, in this case f9d84907d77df62017944cb23cab66305e94ee6ae6c1126415b81cc5e999bdd0, with the value in the file sha256sum.txt.asc. If it matches for CentOS-6.5-x86_64-minimal.iso, your iso download is good. 
> 

KISS => "Keep it simple and stupid".
Oh, switching from htpsswd Apache utility made us grab two additional wins for our customer : 
* WIN 1 Apache License is crap, Linux' is GNU GPL v2 licence, and so is `sha512sum`;
* WIN 2 we have one less dependency in our infrastructure (the less, the better)
Thank you All Linux/UNIX Community around the world for 60 years!

Alright, lets Bourne back:

```bourne
[jbl@pc-100 ~]$ sha512sum mickeymouse
sha512sum: mickeymouse: No such file or directory
[jbl@pc-100 ~]$ 

```

Hum? `no such file or directory?` Oh yeah, I understand : the `sha512sum` software is expecting a file, not a text stream from the standard input... How are we gong to ask `sha512sum` we're not giving him a file path, but the string to hash, on its standard input? Lets' `--help` :

```bash
[jbl@pc-100 ~]$ sha512sum --help
Usage: sha512sum [OPTION]... [FILE]...
Print or check SHA512 (512-bit) checksums.
With no FILE, or when FILE is -, read standard input.

  -b, --binary         read in binary mode
  -c, --check          read SHA512 sums from the FILEs and check them
      --tag            create a BSD-style checksum
  -t, --text           read in text mode (default)
  Note: There is no difference between binary and text mode option on GNU system.

The following four options are useful only when verifying checksums:
      --quiet          don't print OK for each successfully verified file
      --status         don't output anything, status code shows success
      --strict         exit non-zero for improperly formatted checksum lines
  -w, --warn           warn about improperly formatted checksum lines

      --help     display this help and exit
      --version  output version information and exit

The sums are computed as described in FIPS-180-2.  When checking, the input
should be a former output of this program.  The default mode is to print
a line with checksum, a character indicating input mode ('*' for binary,
space for text), and name for each FILE.

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
For complete documentation, run: info coreutils 'sha512sum invocation'

```
There we are : we must use the `--text` option, or `-t` for short :
```bourne
[jbl@pc-100 ~]$ sha512sum -t mickeymouse
sha512sum: mickeymouse: No such file or directory
[jbl@pc-100 ~]$ 

```
Humpf? => Ah, I understand now : `sha512sum` will accept text to HASH, but only from a file. 
K, let's try that :
```bourne
export VOTRE_CHOIX_DE_MOT_DE_PASSE=mickeymouse
echo "$VOTRE_CHOIX_DE_MOT_DE_PASSE"^>> ./please-sha512sum-software-hash-my-mickey.txt
sha512sum -t ./please-sha512sum-software-hash-my-mickey.txt
```
Yeaaaah! [ We win!](https://www.youtube.com/watch?v=B_dX0Nei538) (:Full Matel Jacket-Soundtrack - Surfin' Bird:)
```bourne
[jbl@pc-100 ~]$ export VOTRE_CHOIX_DE_MOT_DE_PASSE=mickeymouse
[jbl@pc-100 ~]$ echo "$VOTRE_CHOIX_DE_MOT_DE_PASSE"^>> ./please-sha512sum-software-hash-my-mickey.txt
[jbl@pc-100 ~]$ sha512sum -t ./please-sha512sum-software-hash-my-mickey.txt
eac315c3e0519f89b8ca39917f4a8ad3ad3380daf8173c9726d450c65d48bf9b85a3ddebf6c10aae32e8aba5a3b6ec6dcfe9bf33ca09a0904e875d4d10274ec0  ./please-sha512sum-software-hash-my-mickey.txt
[jbl@pc-100 ~]$ 
```
(=> Ouh, and isn't that code we can write in a file, and .. version?? :) )
Alright, now let's just be clear about what's gonna happen to that hash : 

Its gonna be stored in Traefik user DAtabase, and when I will try and login with my username, to Traefik, then i'll type `mickeymouse`. Then traefik will HASH the string I typed, `mickeymouse`, using the SHA-512 algorithm. Finally, Traefik will compare the result with the hash previously stored in database: if they are equal, Traefik lets me in, if not, Traefik leaves me sorry wtaring at home page. Just for the record, let's see how to check our SHA-512 hash : 
```bourne
[jbl@pc-100 ~]$ sha512sum -t ./please-sha512sum-software-hash-my-mickey.txt 
eac315c3e0519f89b8ca39917f4a8ad3ad3380daf8173c9726d450c65d48bf9b85a3ddebf6c10aae32e8aba5a3b6ec6dcfe9bf33ca09a0904e875d4d10274ec0  ./please-sha512sum-software-hash-my-mickey.txt
[jbl@pc-100 ~]$ sha512sum -c sha521sum-i-like-you-beinformed-mychecksum-is-inthisfile.sum
./please-sha512sum-software-hash-my-mickey.txt: OK
./please-sha512sum-software-hash-my-mickey.txt: OK
[jbl@pc-100 ~]$ 
```

:)







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








