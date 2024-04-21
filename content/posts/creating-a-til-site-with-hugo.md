+++
title = 'Creating a TIL site with Hugo'
date = 2024-01-13T18:05:57-08:00
+++

What this site is and my reasons for creating it are on [the about page](/about). Although this is the first post intended for this site, til.chriswheeler.dev, I will probably add some older notes with their original dates. This is my first time using [Hugo](https://gohugo.io) and I am very impressed. I used Jekyll once a long time ago and the experience convinced me to make [my own static site generator](https://github.com/wheelercj/Aurora). Now it's been a few years, and I'm going to stop using it because it runs a little slow and is annoying to maintain since it's written in Python. In hindsight, I also made many mistakes on that project and didn't get around to fixing them, but at least I learned a lot from that project and since then.

I'm using Hugo v0.121.2 and probably won't update to newer versions of Hugo until I have a clear reason to.

## Hugo themes

There are many Hugo themes to choose from. While quickly scrolling through [the site listing them](https://themes.gohugo.io/), here are the ones that caught my eye for my purposes:

* [etch](https://themes.gohugo.io/themes/etch/)
* [tailwind](https://themes.gohugo.io/themes/hugo-theme-tailwind/)
* [blog-awesome](https://themes.gohugo.io/themes/hugo-blog-awesome/)
* [compost](https://themes.gohugo.io/themes/compost/)
* [bearcub](https://themes.gohugo.io/themes/hugo-bearcub/)
* [anubis](https://themes.gohugo.io/themes/hugo-theme-anubis/)
* [flat](https://themes.gohugo.io/themes/hugo-theme-flat/)
* [lekh](https://themes.gohugo.io/themes/lekh/)
* [salinger](https://themes.gohugo.io/themes/salinger-theme/)
* [cupper](https://themes.gohugo.io/themes/cupper-hugo-theme/)
* [bare](https://themes.gohugo.io/themes/bare-hugo-theme/)

I've decided to use Etch for now, but I might modify it later to also show each post's tags on the index page. The site looks a little better when [Dark Reader](https://github.com/darkreader/darkreader) is disabled. Maybe I'll change that later too.

## guides

I'm following Hugo's guide for how to [Host on GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/) and GitHub's guide for [Configuring a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site). Although I happen to have GitHub Pro which lets me publish sites from private repos, I think I'll keep all of my site repos public because I might not always want Pro and, from what is explained on [this page](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages), I could see myself accidentally letting my domain get taken over with how GitHub works if I don't keep the repos public. The next page says I have to install BIND, but I'm just going to use the `dig` command in WSL instead. The [Verify a custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages) page says the `til.chriswheeler.dev` domain is already verified because I verified `chriswheeler.dev`.

## troubleshooting

For a while, GitHub said I had not set up DNS correctly, and eventually changed the error message on its own to "Domain does not resolve to the GitHub Pages server . . . (NotServedByPagesError)" while also saying "TLS certificate is being provisioned". I just had to wait a while and the second error message disappeared too. The site was running, but all the generated links were broken and so my chosen theme had not been applied. Somehow the links had the name of the GitHub repo as a folder (such as `til.chriswheeler.dev/til/about` instead of `til.chriswheeler.dev/about`). Also, some of the links still directed to `wheelercj.github.io/til` instead of my custom domain. I double checked everything, ran the GitHub Action to build the site again with no significant changes (I only added an `echo` statement to the action file to get info for debugging), and suddenly all the links and the theme were fixed. My guess is the DNS settings had not finished being applied yet.
