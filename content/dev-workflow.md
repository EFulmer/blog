Title: How to Set Up Your Development Environment
Date: 2017-12-24
Category: Programming
Tags: Workflow, Terminal

One thing I've noticed is that a lot of people aren't taught how to set up a proper development environment. It's the case for both self taught folks and CS students. 

If you are taking CS 101, your instructor may give you instructions to set up Eclipse, Visual Studio, or maybe even Vim or Emacs. If you're using an IDE, you're probably overwhelmed by the dozens of options that don't really mean much, and stay away from anything but a small handful of buttons and menu options. There's a good chance you don't even know much about what other tools exist, and what they can do for you*.

If you're self-taught, you might see a lot of names thrown around which you don't know anything about. You might suffer analysis paralysis as a result. And if you don't have a structured curriculum, there's a lot of stuff that'd make your life easier, but you might not know about it. 

Basically, the most important thing is creating some consistent structure. When you sit down to, you don't want to have to think about what windows and applications you have to set up, because that doesn't get you anywhere interesting. Having that on autopilot makes it easier to get started and work on the stuff that'll really help you learn.

My point in writing this is to give you some advice, whichever camp you are in. To do this, I'll go through my own dev setup.

I use `tmux`. OS X and Ubuntu (the two OSes I use 99% of the time) have tabs for their terminal apps, but I like tmux due to the portability (if I'm remotely logged in to another computer) and ease of use. Switching tabs from iTerm requires three fingers but jumping tabs in tmux is two key presses. Find a good starter guide to tmux here.

For my editor, I like `vim`, but I think the arguments for `emacs` are solid. Personally, I'd recommend vim, but I'm not very zealous about it.

The way it ends up working for me is that I have 3-5 tabs open in tmux, following this format:

1. First tab is whatever I use to build the application/library. That could be `rustc` or a tab running the Flask application or anything similar.
2. Some sort of interactive session for whatever programming language I'm using so I can do some real-time experimentation and playing with concepts. Though I don't always have this (i.e. for Rust).
3. If applicable, an interactive session connected to the database I'm using.
4. Vim. I have my vim config on GitHub [right here](https://github.com/EFulmer/vim-cfg), but I'm looking ways to make my vim use more efficient.
5. A tab for file system and shell related tasks. Mostly `git` with a side of `ls` and `grep`. If you don't know git, there's a great book called Pro Git which is [free to read online!](https://git-scm.com/book/en/v2/)

When I'm working on an application with multiple components (like a React frontend talking to a Python API), I have multiple tabs at the terminal level open: one for each app. Each of those iTerm tabs has tmux open with the other tabs I described.

In fairness, I am primarily a Python and web developer. I think using a graphical IDE makes a lot more sense for Java or C# than it does for Python. Despite that, I'm still the kind of person who does Java stuff in vim.

* This ties into the big frustrating problem of lacking the vocabulary or knowledge to know what questions to ask. That's a *big* topic, though.
