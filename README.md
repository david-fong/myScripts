
# :womans_hat: Darcy

"darcy" is how I like to relax the pronunciation of `.*rc`- the [fileglob pattern](tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm) for typical standalone [run-configuration](wikipedia.org/wiki/Configuration_file) files. Most of the contents of this repo no longer follow that glob pattern ever since I moved everything to fall under one directory, but I decided to keep the name because I like how it sounds.

You will notice that I embed a lot of links in this readme- even ones that you may feel are redundant- and that I don't speak from a very technical point of view. This is mostly because I can only speak to the limits of my knowledge and understanding, but also because I write this in hopes to encourage some of my friends to warm up to the idea of working in a terminal. I want to demonstrate that a terminal can be made more liveable, and to share the steps of the journey I've taken in discovering how to do that.

<br>

## :briefcase: How to use it
As I said before, everything is under one directory, which means less clutter, and easier portability. All you need to do to mirror my environment is to:
1. Clone and copy the contents of this repo into the directory specified by the environment variable [`XGD_CONFIG_HOME`](standards.freedesktop.org/basedir-spec/basedir-spec-latest.html), which by convention is usually `~/.config/`, if set by default.
1. Source [`:/git/bashrc`](git/bashrc) in your `~/.bash_profile` file, or whatever is passed as the `--init-file` argument when invoking bash.
1. You can put a gitconfig-style file in [`:/git/config__local`](git) containing your name and email.
1. Similarly, you can put machine-local bash run-config comands in [`:/bash/aliases__local`](bash).

<br>

## :turtle: Why I do this
I like to poke around and explore things. To me, reading about different parts of the terminal environment is like going on a treasure hunt. And while half the time I don't even know what I'm looking for, I enjoy almost every minute of it. At first, the question that always came up in my mind was "why is *<thing that doesn't follow conventions of modern applications>* this way?". And as I explored and learned about different pieces of the bigger picture, I started to see connections and how the pieces build on top of, or around each other.

For example, I wondered why vim doesn't save buffers using ctrl+s by default. As I learned more about vim and started trying to write keymappings, I found out that ctrl+s is reserved for manual [XON/XOFF flow-control](wikipedia.org/wiki/Software_flow_control) in most terminals, which exists because before terminals were emulated by modern computers, which can scroll through scrollback buffers quite quickly, people needed a mechanism to pause a terminal's output so the operator could actually read it. Vim, for the most part, being a superset of VI, followed in VI's footsteps to honor the terminal's [default ownership](retrocomputing.stackexchange.com/questions/7263/history-of-ctrl-s-and-ctrl-q-for-flow-control) of that key-sequence. I found that this behaviour could be disabled using the stty (set teletype) command, which allowed me to map the update command in vim to ctrl+s. As an aside, if there are any hardcore vim users shaking their fists right now saying I'm using vim wrong, I disagree. I think that if you leverage the configurability of a tool to make it work better for yourself, you are doing it exactly right.

If you're wondering why I don't use WSL, it's because when I started using git-for-windows, I had absolutely no idea what was going on, and it was hard for me to do or find worthwhile pretty much anything I saw. I've come a long way since then, and I may look at switching to WSL in the future, but not until I feel like I'm being limited by MinGW.

<br>

## :balloon: A Bird's Eye View

This is a high level view of what I have learned about terminal-related facilities. I may have accidentally gotten something wrong, so if you notice a mistake or something that can be improved, please shoot me a message or email and correct me!

program                 | description
:----------------------:| -------------------------
:shell:<br>bash         | <b>messenger between you and your computer</b><br>A shell based on sh with features from other shells like csh and ksh. Shells allow you to interact with your operating system's kernel by providing certain services, and making those callable through a command-line interface (you type words that tell your computer to do things). Those services include creating and destroying files and directories, writing to and reading from files, performing file processing, and navigating directories, job / process management, and running executable files.<br><br>See [bash variable primer](compciv.org/topics/bash/variables-and-substitution/), [bash environment variables](gnu.org/software/bash/manual/html_node/Bash-Variables.html), [bash builtin commands](tldp.org/LDP/abs/html/internal.html), and the [shell reference manual](tldp.org/LDP/abs/html/refcards.html). Bash (as well as readline) was originally developed by [Brian Fox](wikipedia.org/wiki/Brian_Fox_(computer_programmer)), and then passed to [Chet Ramey](tiswww.case.edu/php/chet/).
:tv:<br>mintty          | <b>displays text generated by everything else</b><br>A terminal emulator that ships with git-for-windows. A terminal emulator is basically a window that displays text and adheres to standards on interpreting standardized [control-sequences](xfree86.org/current/ctlseqs.html) that include basic text-styling and mouse integration, "tty" is short for ["teletype"](wikipedia.org/wiki/Teleprinter). The one thing I feel is lacking in mintty is support for window tabbing.<br><br>see ["tips on using mintty"](github.com/mintty/mintty/wiki/Tips) and [`.minttyrc`](mintty.github.io/mintty.1.html).
:train:<br>readline     | <b>helps you write and repeat commands</b><br>A program that binds command-line-manipulating actions to key-sequences, such as moving the caret to the beginning of the line (ctrl+a), to the end of the line (ctrl+e), deleting a word (ctrl+w), deleting everything before the caret (ctrl+u), and more, other actions include command-history recall and searching, as well as structured and [composable auto-completion](gnu.org/software/bash/manual/html_node/Programmable-Completion.html).<br><br>I have gotten so used to readline key-bindings that I sometimes absent-mindedly close browser tabs while trying to delete a word in the search bar, or open the page's html source trying to delete the search line.<br><br>bindings can be set on the spot using the `bind` command, and defaults can be setup in an [`.inputrc`](gnu.org/software/bash/manual/html_node/Readline-Init-File.html) file. You can find a full description of default bindings and actions [here](gnu.org/software/bash/manual/html_node/Bindable-Readline-Commands.html).
:scroll:<br>less        | <b>use to scroll through lots of text</b><br>less is a "pager" program. It allows you to feed it input from a file or from the output of another command and to quickly scroll through it using mappable key-bindings.<br><br>You can view its help page with the command `less --help`. To quit the pager, press `q`. User configurations can be specified in a [`.lesskey`](linux.die.net/man/1/lesskey) file.
:pencil2:<br>vim        | <b>light and powerful text editor with no gui</b><br>Vim is a text editor that displays in your terminal window. It has little to no user interface, and leaves all actions to short key-sequences. It is known for having a sharp learning curve (like a wall ([or maybe not](thoughtbot.com/blog/the-vim-learning-curve-is-a-myth))), but having that when-your-scissors-start-gliding feeling after you climb over it (or maybe we [never can](stackoverflow.com/a/1220118/11107541) completely climb over it and we are just gliding as we climb). Here's a [good read](csswizardry.com/2014/06/vim-for-people-who-think-things-like-vim-are-weird-and-hard/) advocating for vim.<br><br>I had a lightbulb moment about vim after learning about keybindings in readline and less: in normal mode, vim uses paging key-bindings identical to those in the less pager (usually with the `ctrl` key prepended). That includes ctrl+d, ctrl+u, ctrl+f, ctrl+b, g, G, j, k, ctrl+y, and ctrl+e. It also uses the same mappings to set and jump to (book)marks, and to perform searching (/, n, and N) and file opening (:e). In insert mode, vim follows some movement key-bindings from readline, such as ctrl+w and ctrl+u.<br><br>I think the most important command in vim for a beginner is not that to quit vim, but that to open the help menu, which you can do by going to normal mode (ctrl+c), and then typing `:help`, optionally followed by a search topic. Also see the [vim cheatsheet](www.fprintf.net/vimCheatSheet.html), and [tips on vim](moolenaar.net/habits.html) written by the person who wrote it, [Bram Moolenaar](wikipedia.org/wiki/Bram_Moolenaar).
:camera:<br>git         | <b>google drive but for code projects</b><br>A version control system that saves incremental changes as snapshots of changed files in their entirety in a local hidden directory as a tree-like structure. One of the nicest things about git is that you can make commits without an internet connection.<br><br>I have found git's tutorial-style documentation on [branching](git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) and on [demystifying the reset command](git-scm.com/book/en/v2/Git-Tools-Reset-Demystified) to be incredibly helpful.

<br>
<br>

## How it looks when I start bash:
![startup](images/startup.PNG)

<br>

## How my vim looks:
![vimrc](images/vimrc.PNG)

<br>

## My modified "ls -la":
![lsa](images/lsa.PNG)
