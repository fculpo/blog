---
title:  "My personnal shell environment and dotfiles"
categories: dotfiles shell fish
toc: true
---
# My favourite shell

TL;DR: **[Fish][fish]**

## Bash

As many, I started learning IT with classic Bash. Not much to say here, this is the default shell for most of Linux distributions out there.

## ZSH
I then heard of [ZSH][zsh], and used it quite a lot for its out of the box friendliness over Bash.
Lots of frameworks were created for Zsh, such as [Oh My ZSH][oh-my-zsh] and [Prezto][prezto] that I both extensively tried. Most useful features provoded by these framework are prompt configuration and added functionnalities, like git integration (showing current branch, status, etc.), syntax highlighting, interactive history searching...

However, the more plugins I added, the slower my prompt was, forcing me to sometimes wait 1-2 seconds between each Enter keypress.

## Fish

Finally, I recently settled with the **[Fish][fish]** shell.

Out of the box, you get:
  - Auto suggestions, based on your history, allowing you to quickly reenter a reviously typed command
  - Auto completion of most commands (fish knows how to parse man pages and automatically build autocomplete suggestions)
  - Syntax highlighting (valid commands turn blue, invalid ones are red)

Some frameworks exist to enhance it further, especially [Oh my fish][omf].
I still prefer simplicitty and lightweigth when it come to my shell, so I currently use **[Fisher][fisher]** which is a simple package manager for Fish, based on a special file called fishfile, containing the list of plugins you want to install.

### The alias vs abbr matchup

One other thing that I particularly enjoy with fish is its abbreviation mechanism. You probably all know the ```alias``` command which allows to create, well, aliases, like this one: ```alias k=kubectl```

When having this alias defined in your bash or zsh, every time you want to use ```kubectl``` you can simply type ```k``` instead, and ```k get all``` is now equivalent to ```kubectl get all```, since your shell knows about the alias.

However, there is a catch: let's say that you want to share your wonderful kubectl command to others, via slack, irc, you name it. So you send them ```k get all```, and when they paste and execute it in their own shell...

```Unknown command: k```

This is because they probably don't have ```k``` aliased as ```kubectl```as you do.

In order to address this, fish allows you to define abbreviations (this is still a quite decent functionnality), like this: 

```abbr -a k kubectl```.

Now when you type ```k```in fish and either press ```space```or ```Enter```, fish will automatically *expand* ```k```to ```kubectl```.

So wheter you use ```k```or ```kubectl```your fish shell history will **always** shows ```kubectl```, allowing consistency and reproductibility, but also eases sharing between coworkers, because they don't have to deal with your powerful aliases that they don't have.

I found this blog post to be interesting about alias vs abbr vs functions: [https://www.sean.sh/log/when-an-alias-should-actually-be-an-abbr/](https://www.sean.sh/log/when-an-alias-should-actually-be-an-abbr/)

### Drawbacks ?

While fish is perfect for my use, it is not fully POSIX compliant and some scripts or command you copy paste from the internets, may or may not execute successfully due to some syntax error detected by fish.

Until recently, you could not use ```&&``` to chain two subsequent commands in fish, you had to separate them with ```;```instead. 
This is now possible sinche Fish 3.0, see this [Github issue](https://github.com/fish-shell/fish-shell/issues/4620).

# The prompt

Although the default fish prompt is fine, I found that adding lots of information to it via plugins still got the prompt quite slow to return, but I can't afford to lose such precious information, like:
  - Git branch/status
  - AWS current profile
  - Kubernetes current context
  - Ruby version
  - Go version
  - Python environment
  - etc.

Upon browsing through others dotfiles repositories, I came across **[starship.rs][starship]**, which is a cross-platform prompt, written in [Rust][rust].

Starship promises are simple: a fast and powerful prompt, and to this day, all I can say is that these promises are delivered. Even with lots of information on my prompt, each press on Enter feels way more faster than any default shell prompt with the same level of details. I won't lie by saying it's ultra fast when dealing with 10 plugins on your prompt, but it is definitely faster.

An added advantage is the cross-platform thing, you can indeed use the same configuration for bash, zsh, fish, even powershell, and get the same prompt output.

So, yes, it is indeed likely that both Bash, ZSH and fish prompts would perform the same with the same Starship config.

# Dotfiles

TL;DR: You can find them [here][dotfiles]


[omf]: https://github.com/oh-my-fish/oh-my-fish
[fisher]: https://github.com/jorgebucaran/fisher
[rust]: https://www.rust-lang.org/
[starship]: https://starship.rs
[fish]: https://fishshell.com/
[zsh]: https://www.zsh.org/
[oh-my-zsh]: https://github.com/ohmyzsh/ohmyzsh
[prezto]: https://github.com/sorin-ionescu/prezto
[dotfiles]: https://github.com/fculpo/dotfiles

