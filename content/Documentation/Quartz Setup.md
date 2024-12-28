---
title: Quartz Setup
share: true
date: 2024-12-23
date-modified: 2024-12-27
---

# Getting things set up

## Setup Docs
I followed the documentation on https://quartz.jzhao.xyz/ for getting started. I'll cover many of the steps but if you want to do this yourself you'd be better off following this guide as its probably more up to date.

## Quartz Setup
I cloned the repo and have it hosted at https://github.com/steven-smith-IT/quartz-ssmith. I was originally going to try to host this in my own self hosted git server but I realize that made administration extra difficult!
>[!tip]- Separation of Vaults
>I spent a great deal of time trying to figure out how many vaults I wanted. I use obsidian-git to back up my files and thought I would use that for automating the publishing of notes. This was great until I thought I might be having private information in this vault as well as public websites so I thought self hosting was the only way to avoid this leak!
>Well, that was incorrect. The easiest way to avoid this leak was to just keep the private information out of this vault.

## Hosting Setup
I decided to go with [Cloudflare for hosting](https://quartz.jzhao.xyz/hosting#cloudflare-page). This decision stems from the Separation of vaults callout. When I was self-hosting my git repo to avoid leaking private info it disqualified GitHub pages as the options. I've since changed my mind and had already set up cloud-flare pages so I decided to stick with it.

## Publishing Content
Quartz makes things super simple but Ideally I don't want to have to touch the quartz config after I get it set up. I've decided to start with [Obsidian Enveloppe](https://github.com/Enveloppe/obsidian-enveloppe). The only real change I've made to the default configs is to make sure notes are uploaded to the `content` folder. This means I can update my site just through obsidian without having to worry about keeping this obsidian vault symbolically linked, as a git sub-module, or contained entirely within the content directory of the quartz repo.

Using a plugin like this reduces my overall friction for writing notes and as someone who has wanted to do this for years and allowed myself to procrastinate and get discouraged I need a solution that reduces friction.

## DNS Settings
These settings were surprisingly difficult to figure out! I obviously own the domain stevensmith.me. I wanted this site to live at the root of the domain but that is surprisingly difficult. 
### Settling for www
www is one of those standardized prefixes that communicates that the website you are accessing should be reached using http. That worked well enough for me but I wanted folks who typed in the address without the www to be able to access my website as well.
### Proxying with DNS
You cant set a CNAME record for your root domain. Some registrars have different types of records that can emulate this behavior but you can't easily redirect or alias a root domain without the use of some sort of proxying behavior. I didn't want to transfer my domain to cloudflare so that it could correctly resolve the cloudflare page so I settled on [Forwarding my root record to my www record.](https://kb.porkbun.com/article/39-how-to-set-up-url-forwarding) Once this was set up everything has worked great. 

