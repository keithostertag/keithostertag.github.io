---
layout: post
title: "Installing Simplenote in Debian"
date: 2017-08-17
tags: debian simplenote
---

 On a suggestion by Ukiah Smith in an interesting thread about [Note taking tools and workflow](https://community.louisville.io/t/note-taking-tools-and-workflow/722/11) I decided to install Simplenote on my Debian system. I have been using zim, but zim  isn't easily configured to access globally. Simplenote uses a cloud service so that I would be able to sync all of my devices, and has some nice features like the ability to use Markdown.

The Simplenote website has (conveniently) a .deb file, so I downloaded that and installed with dpkg (Simplenote is not on the Debian repository).

Yet after installing successfully I wasn't able to invoke the executable.... couldn't find it! Turns out it installs into /usr/share/simplenote/. I added that to my path in my .bashrc file but still no joy!

Hmm... off to Google to find a solution. I'm using dmenu with my i3 window manager, so I began by searching about how dmenu finds executables. There's a fair amount of Internet discussion around using the XDG Base directory specification with dmenu, but my system doesn't utilize that currently and I did not want to get into that can of worms just for this one program that I'm just trying out.

Eventually I was lucky to find an old [from 2008!](https://crunchbang.org/forums/viewtopic.php?id=93) post that solved this problem this way:

> I learned a bit about interactive and non-interactive shells and which profile is used for which. The $PATH for interactive shells is derived from ~/$HOME/.bashrc and for non-interactive shells /etc/environment. So I added the path to the OpenOffice programs to /etc/environment and both dmenu and  gmrun started working.

Trying this advice, I edited my /etc/environment file (which was empty) to include the path to the simplenote executable, and after logging out and back into my system, voila! Now I can invoke Simplenote using my regular dmenu hot-key.

Now, on to trying out the Simplenote program...
