---
title: 'Un fichier hosts pour les bloquer tous'
i18n-key: hosts
date: '2018-09-07'
main_image: '/assets/images/2018-09-07/gollum.jpg'
type: post
tags:
    - WebPerf
    - 'Me, myself and I'
    - Outils
    - Productivité
locale: fr_FR
---


En tant qu'expert du domaine, les gens me demandent souvent comment améliorer la performance des sites Web. Parfois, ils me demandent aussi comment améliorer les performances du Web sur leur propre machine, pour leur propre expérience de navigation. Dans ce cas, ma réponse est toujours la même : commencer par le fichier **hosts**.

{% capture img_alt %}Gollum, tenant l'Anneau unique dans l'adaptation du Seigneur des Anneaux de Peter Jackson{% endcapture %}
{% capture img_caption %}Je manquais d'inspiration pour trouver une illustration plus sympa…{% endcapture %}
{% include rwd-image.html.liquid
path="/assets/images/2018-09-07/gollum.jpg"
alt=img_alt
caption=img_caption
%}

<!-- more -->

## Keeping the dirt away

Le Web d'aujourd'hui est blindé de saletés. La plupart des sites sont bourrés de traqueurs, de publicités et de beaucoup d'autres choses désagréables qui pénalisent le chargement des sites Web. Pour éviter cela, les gens utilisent de plus en plus d'AdBlockers[^pr]. Ils offrent une solution simple et rapide (la plupart du temps, une extension de navigateur) qui bloque la plupart des contenus indésirables.

[^pr]: Le taux de pénétration des bloqueurs publicitaires aux États-Unis est d'environ 30 % sur les ordinateurs de bureau, et d'environ 12 % sur les téléphones mobiles, selon cette [étude eMaketer sur le blocage des publicités à partir de mars 2017].(https://www.statista.com/statistics/351862/adblocking-usage/).

Malheureusement, au niveau de l'UX, les AdBlockers ne font pas toujours l'affaire. Ils augmentent souvent la quantité de mémoire vive et de cycles CPU utilisés par votre navigateur Web, ce qui ralentit votre expérience de navigation au lieu de l'améliorer. Certains font mieux que d'autres, et des navigateurs entiers[^brave] ont été conçus pour bloquer les contenus indésirables, et font en cela un travail incroyable. Mais le web ne se limite pas à votre navigateur, n'est-ce pas ?

[^brave]: If you've never tested [Brave Browser](https://brave.com/), I can only encourage you to do so, and join the 4 million people that trust it to fix the web.

The Web is requested from everywhere in your computer. Most mainstream applications are as crammed with trackers as your next media website. Sometimes, you can even see the ads displayed in your UI (_Hello, Skype. Yes, I'm talking about you, you naughty boy_).

The AdBlockers can't do anything about that. But a simple hosts file does.

## Hosts… what?

> The computer file **hosts** is an operating system file that maps hostnames to IP addresses. It is a plain text file.
> <cite>"[hosts (file)](https://en.wikipedia.org/wiki/Hosts_%28file%29)", on Wikipedia</cite>

Whenever your browser interacts with a website, it actually requests a server, located through its IP address, like 185.31.40.11 (IPv4) or 2a00:b6e0:1:20:2::1 (IPv6). It's pretty similar to a postal address.

Now think about accessing a webpage, like <https://borisschapira.com>. How does your browser know which IP address to contact? Well, the browser simply asks the Internet phone book. At least, one of them. And the phone book, called a <abbr title="Domain Name Server">DNS</abbr>, resolves the IP address for the browser.

I don’t know about you, but I never use a phone book. Most of the time, I’ve collected the address of the people to whom I want to write in my personal address book. That’s the **hosts file** for you. Every time a process on your computer needs to access a resource on the Internet, it first goes through the hosts file to find out where to find it.

Now, let’s say that you don’t want this process to find the resource on the badthings.com domain. _Easy peasy_, throw it on the wrong track by associating the badthings.com domain to an unspecified address like 0.0.0.0.

So basically, if someone makes a list of all the domains where bad things happen, we can redirect them all to 0.0.0.0 in our hosts file, and make **our own Web** a much cooler place.

## One project to gather them all

There is nothing new in what I am describing here. Cool people have been doing this for years, sharing their host files. Fake news websites, gaming platforms, pornographic hubs, encryption pages, fraud attempts, and scams are all patiently identified and listed in open access files.

I use [Steven Black's "hosts" project](https://github.com/StevenBlack/hosts), a python script, to cram them into [a single 2MB hosts file](https://raw.githubusercontent.com/borisschapira/hosts/master/hosts) containing more than 70k domains. In case you're wondering, I can and do alter the result with my own whitelist (otherwise blocked domains whose requests I don't want to prevent) and redirections (which allows me to write this article and check the result on https://borisschapira-dev.com:10443/, which actually points to my own machine).

If you're not familiar with the command line and use Windows 10, the [hostsman](http://www.abelhadigital.com/hostsman/) app will help you achieve the same goal. I will not recommend modifying your host file on previous versions of Windows even if [I did it, before 2015 (FR)](https://borisschapira.com/2015/08/de-windows-a-mac/), unless you like to run `ipconfig /flushdns' every 30 minutes. On Linux, I've heard people talk about using [dnscrypt-proxy](https://github.com/jedisct1/dnscrypt-proxy)… but I've never tried myself.

{% capture img_alt %}A screencapture from hostsman sources manager{% endcapture %}
{% capture img_caption %}You can manage Update Sources in hostsman{% endcapture %}
{% include rwd-image.html.liquid
path="/assets/images/2018-09-07/hostsman.png"
alt=img_alt
caption=img_caption
%}

## Some tips from my daily life

Sometimes, I need to temporaly disable this hosts file. For example, when I need to help [Dareboost](https://www.dareboost.com/) clients understand the impact of third-party scripts on their pages (thus, I need to load these 3ps myself).

To enable or disable my hosts file, I use a command line function that I've develop and put in my `~/.profile` file[^ozsh]:

[^ozsh]: Actually, I put this function in my `~/.zprofile`, as I use [Oh My ZSH](https://ohmyz.sh/).

```bash
function togglehost() {
    if [ -e /etc/host.bak ]
    then
        sudo mv /etc/host.bak /etc/hosts
        echo "Hosts file is active again"
    else
        sudo mv /etc/hosts /etc/host.bak
        echo "Hosts file is set aside"
    fi
}
```

Once this function is loaded, activating or deactivating my hosts file is very simple:

```terminal
$ togglehost
Hosts file is set aside
$ togglehost
Hosts file is active again
```

But as I sometimes forget to put it back in place, I have set up a routine that checks every minute that the file is in place and, if it is not the case, warns me by using Jaime Piña's [noti](https://github.com/variadico/noti) to trigger a notification. To perform this regular check, I use `crontab`.


```
* * * * * if [ ! -e /etc/hosts ]; then /usr/local/bin/noti -t "Host file" -m "does not exists"; fi
```

I have been using this technique for years now and, sometimes, I forget that my hosts file protects me so much. Whenever I need to use someone else's computer, or temporarily disable my hosts file, I realize the level of comfort it provides me.

I'm well aware that tweaking its own hosts file is a good but technical solution. It doesn't completely replace an AdBlocker (or I haven't aggregated enough files yet) but it's an incredible performance gain, which I highly recommend for everyday browsing.

Try it for yourself, and tell me what you think!

***

## Summary

Hosts files are your computer internal address books that guide Web requests to the right servers. Fill your hosts file with domains pointing to nothingness, and those requests will quickly and surely fail. People are sharing their hosts file for years. Solutions now exist to concatenate them, and crowdsource a solution to the dirty Web we've to deal with everyday.

***