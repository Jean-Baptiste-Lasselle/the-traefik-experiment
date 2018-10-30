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
