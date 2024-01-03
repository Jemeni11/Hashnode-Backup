---
title: "Boost Your Productivity with Shell Commands"
datePublished: Wed Jan 03 2024 21:37:42 GMT+0000 (Coordinated Universal Time)
cuid: clqyaun8c000608jpb03d6q6o
slug: boost-your-productivity-with-shell-commands
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704317701835/bda3eb6b-6089-41eb-a357-99d343212e4f.png
tags: functions, productivity, bash, beginner, shell, alias

---

## Introduction

If you're familiar with working in a terminal, you've likely encountered various shell commands like `ls`, `cd`, and `grep`.

Whether you want to create a new file, change your system settings or just check the current time, you can do all this with shell commands in your terminal.

However, there's always room for optimization, especially since commands can get overly wordy. When it comes to reducing the number of words or commands you need to type, creating your own commands might be the solution.

In this guide, I'll walk you through the process of crafting your custom shell commands. This tutorial assumes that you've had prior experience using a terminal and are comfortable with basic commands. Let's dive in and enhance your command-line skills!

## What you need to know

Fundamental commands like:

* ls
    
* cd
    
* grep
    

## Scenario One: Creating and Navigating to a new directory

Suppose you want to create a new folder and navigate to it. You can achieve this with the following commands:

```bash
nonso@HPEnvy:~$ mkdir myArticles
nonso@HPEnvy:~$ cd myArticles/
nonso@HPEnvy:~/myArticles$
```

You could even do it in one line:

```bash
nonso@HPEnvy:~$ mkdir myArticles && cd myArticles/
nonso@HPEnvy:~/myArticles$
```

How about with one command? Something like

```bash
nonso@HPEnvy:~$ mkdirandcd myArticles
nonso@HPEnvy:~/myArticles$
```

`mkdirandcd` is what we call a function. Behind the scenes, `mkdirandcd` executes this command we saw earlier: `mkdir myArticles && cd myArticles`.

How do we make this?

In your home directory, there should be a file called `.bashrc`.

Open the file with any text editor of your choice. Then scroll to the end and paste the following:

```bash
mkdirandcd() {
  mkdir -p "$1" && cd "$1"
}
```

* `mkdir -p "$1"`: This command creates a directory with the name provided as the first argument to the function ($1). The `-p` flag ensures that the command creates parent directories if they don't exist.
    
* `cd "$1"`: If the directory creation is successful, the function changes the current directory to the newly created directory.
    

Now, save the file and run `source .bashrc`.

Running the command again should produce this:

```bash
nonso@HPEnvy:~$ mkdirandcd myArticles
nonso@HPEnvy:~/myArticles$
```

## Scenario Two: Running a virtual environment in Python

If you're not familiar with virtual environments in Python or Python itself, no worries! In the Python world, a virtual environment (often abbreviated as virtualenv or venv) is a tool for managing dependencies.

Imagine you have two projects, Project Alpha and Project Beta, where Alpha requires version [3.0.0](https://pypi.org/project/FicImageScript/3.0.0/) of a package called [FicImage](https://pypi.org/project/FicImageScript/), while Beta needs version [2.1.0](https://pypi.org/project/FicImageScript/2.1.0/). A virtual environment is a way of ensuring that the specific versions of packages needed for one project don't clash with those of another.

Now, let's dive into the activation process.

To activate a virtual environment, we need to run:

```bash
nonso@HPEnvy:~$ source venv/bin/activate
```

The command line should look something like this, showing the venv is active.

```bash
(venv) nonso@HPEnvy:~$
```

But what if our venv was not in the home directory? Then we would have to do something like this:

```bash
nonso@HPEnvy:~$ cd Documents/FicImage/
nonso@HPEnvy:~/Documents/FicImage$ source venv/bin/activate
(venv) nonso@HPEnvy:~/Documents/FicImage$
```

"But it's only two lines!"

Well yes, but that's one line too many. Let's see how we can knock it down to one line.

Once again, we could do this:

```bash
nonso@HPEnvy:~$ cd Documents/FicImage/ && source venv/bin/activate
(venv) nonso@HPEnvy:~/Documents/FicImage$
```

And this would work but we want to use one command.

So open up `.bashrc` with any text editor of your choice, scroll to the end and type the following:

```bash
# An alias to change directories and run a venv
alias cdFIvenv='cd /home/nonso/Documents/FicImage && source venv/bin/activate'
```

Unlike our first scenario, `cdFIvenv` is an alias and it does not take arguments.

Now save the file and run `source .bashrc`.

We used the absolute path of the FicImage directory to make sure the command could be run from anywhere.

Now, whenever you type `cdFIvenv`, magic happens: you jump to the FicImage directory and activate the virtual environment, no matter where you are!

```bash
nonso@HPEnvy:~$ cd ..
nonso@HPEnvy:/home$ cd ..
nonso@HPEnvy:/$ cd media/nonso/562E4C252E4BFD0D/Users/HP/Documents/
nonso@HPEnvy:/media/nonso/562E4C252E4BFD0D/Users/HP/Documents$ cdFIvenv 
(venv) nonso@HPEnvy:~/Documents/FicImage$
```

## (Extra) Beyond the Basics

The first two scenarios are pretty well rounded but if you want something more complex, come along!

I'm using a touchscreen laptop and I occasionally decide to turn off the touch capability. I do this by using the tool `xinput`.

```bash
nonso@HPEnvy:~$ xinput
⎡ Virtual core pointer                     id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer           id=4    [slave  pointer  (2)]
⎜   ↳ 2.4G Mouse                           id=9    [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad           id=13   [slave  pointer  (2)]
⎜   ↳ ELAN2097:00 04F3:2331                id=11   [slave  pointer  (2)]
⎣ Virtual core keyboard                    id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard          id=5    [slave  keyboard (3)]
    ↳ Power Button                         id=6    [slave  keyboard (3)]
    ↳ Video Bus                            id=7    [slave  keyboard (3)]
    ↳ Power Button                         id=8    [slave  keyboard (3)]
    ↳ HP Wide Vision HD: HP Wide Visi      id=10   [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard         id=12   [slave  keyboard (3)]
    ↳ Wireless hotkeys                     id=14   [slave  keyboard (3)]
    ↳ HP WMI hotkeys                       id=15   [slave  keyboard (3)]
nonso@HPEnvy:~$
```

To disable my touchscreen, I use the id provided like this:

```bash
nonso@HPEnvy:~$ xinput disable <id>
```

My screen's name is "ELAN2097:00 04F3:2331" so the id is 11.

```bash
nonso@HPEnvy:~$ xinput disable 11
```

And that disables it. Now you might be wondering, why don't I simply create an alias that runs `xinput disable 11`? It's because the ids can change. I accidentally disabled my keyboard once because I didn't know the ids had changed. So what's the solution?

Well, I can use grep on the output from xinput like this:

```bash
nonso@HPEnvy:~$ xinput | grep "ELAN"
⎜   ↳ ELAN2097:00 04F3:2331                id=11   [slave  pointer  (2)]
```

And if I take the string I get as output and use grep again:

```bash
nonso@HPEnvy:~$ echo "⎜   ↳ ELAN2097:00 04F3:2331                id=11   [slave  pointer  (2)]" | grep -oP 'id=\K\d+'
11
```

I get the id!

Let's break down the second grep command:

* `-o` : This flag shows only what matches, so instead of displaying the entire line containing the match, it only shows the actual part of the line that matches the pattern. Meaning, instead of `⎜ ↳ ELAN2097:00 04F3:2331 id=11 [slave pointer (2)]`, we only get `id=11`.
    
* `-P`: This option tells grep to use Perl-compatible regular expressions (PCRE), which are more advanced and flexible than basic regular expressions.
    
* `'id=\K\d+'`: The PCRE we're using here is looking for a string that starts with 'id='. The '\\K' tells grep to exclude the 'id=' part of the string, and '\\d+' matches all the digits after 'id='.
    

I could even make it a one-liner so it's more readable

```bash
nonso@HPEnvy:~$ xinput | grep "ELAN" | grep -oP 'id=\K\d+'
11
```

> I'm using "ELAN" instead of "ELAN2097:00 04F3:2331" because I'll get the same result anyway and typing the full name takes up space.

Since I have the ID, I can run `xinput disable id` to disable the touchscreen.

```bash
nonso@HPEnvy:~$ xinput disable $(xinput | grep "ELAN" | grep -oP 'id=\K\d+')
```

And this works! We can save this as an alias and we are done.

> If you're wondering why we don't just use `xinput disable (xinput | grep "ELAN" | grep -oP 'id=\K\d+')`, it's because it's not valid in bash. You'll get a syntax error.

## (Extra) .bash\_aliases

If you've explored your `.bashrc` file, you might have come across a section like this:

```bash
# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
```

> Just above this, you may have noticed some default aliases like `alias ll='ls -alF'` or `alias la='ls -A'`.

Please note that not all systems have this specific section in their `.bashrc` file.

This section informs us about another location where we can store our custom aliases: a file named `.bash_aliases`. It's recommended to save your aliases there to maintain a tidy `.bashrc`. However, this approach only works if the following code is included in your `.bashrc`:

```bash
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

If you don't have a `.bash_aliases` file, you can manually create one in the same directory as your `.bashrc`. Just remember to paste the code snippet above into your `.bashrc` for it to take effect.

## Conclusion

To summarise, creating your own shell commands is a game-changer for terminal tasks. From quick folder creation to efficient virtual environment activation, custom commands make the command line a breeze. Armed with the insights from this guide, you're ready to supercharge your command-line skills. Happy coding!

## Additional Resources

* ls - [Manpage](https://man7.org/linux/man-pages/man1/ls.1.html)
    
* cd - [Ubuntu manpage](https://manpages.ubuntu.com/manpages/xenial/en/man7/bash-builtins.7.html)
    
* grep - [Manpage](https://man7.org/linux/man-pages/man1/grep.1.html) or [MDN Web Docs](https://developer.mozilla.org/en-US/blog/searching-code-with-grep/)
    
* Why are we running `source .bashrc`? Here's a great answer from [AskUbuntu](https://askubuntu.com/a/1266282/1643195)!
    
* [Perl-compatible regular expressions(PCRE)](https://man7.org/linux/man-pages/man3/pcre2syntax.3.html).
    
* [Regex101](https://regex101.com/) - A great place for testing and learning about regular expressions.