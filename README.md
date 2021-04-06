
# David's Dotfiles

This is a collection of configuration files made for a Git For Windows + MinTTY environment.

```sh
# If you don't have XDG environment variables set up, you can do this:
# echo 'declare -rx XDG_CONFIG_HOME="$(cygpath "${XDG_CONFIG_HOME:-"${HOME}/.config"}")"' >> "$HOME/.bash_profile"
# echo 'declare -rx XDG_CACHE_HOME="$(cygpath "${XDG_CACHE_HOME:-"${HOME}/.cache"}")"' >> "$HOME/.bash_profile"
# echo 'declare -rx XDG_DATA_HOME="$(cygpath "${XDG_DATA_HOME:-"${HOME}/.local/share"}")"' >> "$HOME/.bash_profile"
# echo '[[ -f "${XDG_CONFIG_HOME}/bash/profile" ]] && source "${XDG_CONFIG_HOME}/bash/profile"' >> "$HOME/.bash_profile"

git clone https://github.com/david-fong/dotfiles.git "$XDG_CONFIG_HOME"
echo '[[ -f "${XDG_CONFIG_HOME}/bash/bashrc" ]] && source "${XDG_CONFIG_HOME}/bash/bashrc"' >> "$HOME/.bash_profile"
```

## Features of Interest

- Keybindings are based around `iokl,.`, which are mapped to left, right, down, up, home, and end, respectively.
- Via AutoHotKey, the Caps-Lock is an alias for the Ctrl key, alt-m for enter, alt-; for backspace, alt-d for delete, and alt-e for escape.
- Fast prompt (by taking out the parts that make calls to git).
- Nice scrolling behaviour inside less [(see this)](https://github.com/gwsw/less/issues/111).

## :balloon: A Bird's Eye View

Below is my attempt to describe some common MSYS2-bundled facilities in a non-technical way. I may have accidentally gotten something wrong, so if you notice a mistake or something that can be improved, please create an issue in this repo!

For more information about what Git For Windows, MSYS2, Cygwin, MinGW-64, and MinTTY are, see the following helpful links: [MSYS2's history](https://www.msys2.org/wiki/History/), [MSYS2 vs Cygwin](https://www.msys2.org/wiki/How-does-MSYS2-differ-from-Cygwin/), [MSYS2 explains terminals](https://www.msys2.org/wiki/Terminals/).

program                 | description
:----------------------:| -------------------------
🥥<br>bash | <b>messenger between you and your computer</b><br>A shell based on sh with features from other shells like csh and ksh. Shells allow you to interact with your operating system's kernel by providing certain services, and making those callable through a command-line interface (you type words that tell your computer to do things). Those services include creating and destroying files and directories, writing to and reading from files, performing file processing, navigating directories, job / process management, and very importantly, running executable files. Bash (as well as readline) was originally developed by [Brian Fox](https://wikipedia.org/wiki/Brian_Fox_(computer_programmer)), and then passed to [Chet Ramey](https://tiswww.case.edu/php/chet/).<br><br>When I started learning about bash (coming from C and Java), the thing that boggled my mind the most was that you could [create and destroy variables on the spot](https://digitalocean.com/community/tutorials/how-to-read-and-set-environmental-and-shell-variables-on-a-linux-vps#setting-shell-and-environmental-variables), and that [spaces and quotes](https://wikipedia.org/wiki/Internal_field_separator) were somehow super important. Here are other pages from helpful resources and sites:<ul><li>[variables and substitution](https://compciv.org/topics/bash/variables-and-substitution/)</li><li>[environment variables](https://gnu.org/software/bash/manual/html_node/Bash-Variables.html)</li><li>[builtin commands](https://tldp.org/LDP/abs/html/internal.html)</li><li>[shell reference manual](https://tldp.org/LDP/abs/html/refcards.html)</li></ul>
📺<br>mintty | <b>displays text generated by everything else</b><br>A terminal emulator that ships with git-for-windows. A terminal emulator is basically a window that displays text and adheres to standards on interpreting standardized [control-sequences](https://xfree86.org/current/ctlseqs.html) that include basic text-styling and mouse integration. "tty" is short for ["teletype"](https://wikipedia.org/wiki/Teleprinter). The one thing I feel is lacking in mintty is support for window tabbing.<br><br>See ["tips on using mintty"](https://github.com/mintty/mintty/wiki/Tips) and [`.minttyrc`](https://mintty.github.io/mintty.1.html).
🚋<br>readline | <b>helps you write and repeat commands</b><br>A program that binds command-line-manipulating actions to key-sequences, such as moving the caret to the beginning of the line (ctrl+a), to the end of the line (ctrl+e), deleting a word (ctrl+w), deleting everything before the caret (ctrl+u), and more. Other actions include command-history recall and searching, as well as structured and [composable auto-completion](https://gnu.org/software/bash/manual/html_node/Programmable-Completion.html).<br><br>I have gotten so used to readline key-bindings that I sometimes absent-mindedly close browser tabs while trying to delete a word in the search bar, or open the page's html source trying to delete the search line.<br><br>Bindings can be set on the spot using the `bind` command, and defaults can be setup in an [`.inputrc`](https://gnu.org/software/bash/manual/html_node/Readline-Init-File.html) file. You can find a full description of default bindings and actions [here](https://gnu.org/software/bash/manual/html_node/Bindable-Readline-Commands.html).
📜<br>less | <b>use to scroll through lots of text</b><br>A [terminal pager](https://wikipedia.org/wiki/Terminal_pager). It allows you to feed it input from a file or the output of another command, and then to quickly scroll through that text using mappable key-bindings.<br><br>You can view its help page with the command `less --help` (which it will- somewhat cheekily- display to you using itself). To quit the pager, press `q`. User configurations can be specified in a [`.lesskey`](https://linux.die.net/man/1/lesskey) file.
📝<br>vim | <b>light and powerful text editor with no gui</b><br>Vim is a text editor that displays in your terminal window. It has little to no user interface, and leaves all actions to short key-sequences. It is known for having a sharp learning curve (like a wall ([or maybe not](https://thoughtbot.com/blog/the-vim-learning-curve-is-a-myth))), but having that when-your-scissors-start-gliding feeling after you climb over it (or maybe we [never can](https://stackoverflow.com/a/1220118/11107541) completely climb over it and we are just gliding as we climb). Here's a [good read](https://csswizardry.com/2014/06/vim-for-people-who-think-things-like-vim-are-weird-and-hard/) advocating for vim.<br><br>I had a lightbulb moment about vim after learning about keybindings in readline and less: in normal mode, vim uses paging key-bindings identical to those in the less pager (usually with the `ctrl` key prepended). That includes ctrl+d, ctrl+u, ctrl+f, ctrl+b, g, G, j, k, ctrl+y, and ctrl+e. It also uses the same mappings to set and jump to (book)marks, and to perform searching (/, n, and N) and file opening (:e). In insert mode, vim follows some movement key-bindings from readline, such as ctrl+w and ctrl+u.<br><br>I think the most important command in vim for a beginner is not that to quit vim, but that to open the help menu, which you can do by going to normal mode (ctrl+c), and then typing `:help`, optionally followed by a search topic. Also see the [vim cheatsheet](https://www.fprintf.net/vimCheatSheet.html), and [tips on vim](https://moolenaar.net/habits.html) written by the person who wrote it, [Bram Moolenaar](https://wikipedia.org/wiki/Bram_Moolenaar).
💾<br>git | <b>google drive but for code projects</b><br>A version control system that saves incremental changes as snapshots of changed files in their entirety in a local hidden directory as a tree-like structure. Made to allow you to save incremental changes to your project, and work collaboratively using operations to sync up changes made by you and possible partners.<br><br>I have found git's tutorial-style documentation on [branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) and on [demystifying the reset command](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified) to be incredibly helpful.<br><br>Two other great commandline tools for git are: `tig`, which ships with Git For Windows, and lazygit. Both of these are Text-User-Interfaces to git that follow terminal keybinding patterns.
