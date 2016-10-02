# Vim

Accumulated from personal use and lots of other sources.

## Resources

* [Learn Vimscript the Hard Way](http://learnvimscriptthehardway.stevelosh.com/): Mostly about the scripting language, but the earlier chapters contain good `.vimrc` suggestions
* [Practical Vim](https://pragprog.com/book/dnvim2/practical-vim-second-edition), by Drew Neil
* [Vim Awesome](http://vimawesome.com/): Listing of popular Vim plugins
* [Vimcasts](http://vimcasts.org/), particularly the [Fugitive Series](http://vimcasts.org/blog/2011/05/the-fugitive-series/)
* [Vim subreddit](https://reddit.com/r/vim): Helpful resources in sidelink
* `:help <subject>` for the manual entry on subject (also tab-autocompletes)

## History

* Adapted from the [Vi](https://en.wikipedia.org/wiki/Vi) editor, started by [Bill Joy](https://en.wikipedia.org/wiki/Bill_Joy) in 1975
* Created by [Bram Moolenaar](https://en.wikipedia.org/wiki/Bram_Moolenaar) - first released in 1991

## Basics

* Check vim version with `:ve[rsion]`
* When in normal mode, can move the cursor using `h`, `j`, `k`, `l`
* Normal mode is sometimes known as the 'command mode'. This is the default mode; can go to this with `<Esc>` or `<C-c>`
* 'ex commands' are those prefixed with a `:`
* Pressing `:q!` in normal mode quits without saving the file
* `ZZ` saves and closes a buffer

## Normal Mode

Default mode of the Vi(m).

* `<C-g>` prints the location of your file, and also file status
* `g <C-g>` print cursor location, line, **word**, char and byte count
* Press `gg` to go to start of file, and `G` to go to end of file
* Type in `number` + `G` to move to that line number in the file. This is useful for when you want to select to a certain line number
* `.` (the 'dot' operator)  repeats the last normal operation made
    * Synergises well with a visual linewise highlight, then `norm .` as a lightweight macro

### Text Objects

Regions of characters can be categorised and selected as 'text objects'

* Text objects define regions of text by structure, i.e. pairs of `[],` `<>`, `<>` and `</>` etc. Made up of [ia], and `w`, `W`, `',` `"` etc.
* `w` is word, e.g. `cat`
* `W` is WORD (includes non-alphanumeric characters and some symbols), e.g. `1cat-dog2`
* `t` is tag, e.g. `<h1>Heading</h1>`
* `p` is a paragraph, a contiguous region of non-empty lines
* `s` is sentence, although if you want to use it as a motion, you'd use `)`
* `i` means inner, `a` means around
* `],` `},` `),` `t` goes around square brackets, braces, parenthesis and tags respectively
* **TIP**: `cit`, `cat`, `dit` and `dat` are very useful, as are `vi}`, `va}` etc.

### Editing

* `x` deletes the character under the cursor
* `X` deletes the character before the cursor
* `S` deletes the whole line
* `D` deletes until the cursor
* `C` deletes until the cursor, then enters insert mode
* To start appending to a line, press `A`
* `d` is the delete command. The motion that it takes are `w`, `e`, and `$`. `w` deletes to the start of the next word, whilst `e` deletes to the end of the current word, e.g. `d$` deletes from cursor to the end of the line
* `dd` deletes the entire line
* Typing in a number after an operator repeats it that many times, e.g. `d2d` will delete the next two lines
* Using `e` and `a` in conjunction with each other is pretty cool
* Use `I` to insert at the start of the line
* Use `gi` to insert where the cursor line was on previous insert
* Use `s` to delete the character, then enter insert mode there
* To decrement and increment numbers, use `<C-a>` and `<C-x>`. Can try this out here! 31
* Also if you are currently not on a number, `<C-a>` and `<C-x>` will bring you to a number. Also, can use `190<C-a>`, which would add 190 onto the first number it sees. Same with `<C-x>`, but it subtracts it away
* Use the tilde symbol `~` to toggle case
* Use `==` to autoindent. When in visual mode, use regular `=` to autoindent
* `J` merges the current line and the line below it
* Formal syntax for a change command is: `<operator>` (e.g. `d`), `[number]` (e.g. 2), `<text object>`
* `u` undos, `U` reverts line back to original state
* `p` puts, and `P` puts behind the cursor
* Also, if you want the cursor to move to the end part of where you pasted, use `gp`
* If you want the cursor to stay where it is when using `P`, use `gP` instead
* Yanking also takes actions, like `y5l` yanks 5 characters to the left of the cursor
* `y <space>` yanks the one character the cursor is on

The change operator `c` can be used to specify the number of words, or lines, to change. For example, `cw` while the cursor is on the start of a word will delete it and allow you to insert something there instead.

* `cc` will delete the whole line and then enter insert mode on that line
* `c$` does the same thing as `C` (deletes all from the right of the cursor)
 
### Navigation

* `0` moves cursor to start of line
* `w` moves the cursor forward a word
* `e` moves the cursor to the end of a word
* `^` moves to first non-blank character
* Prefix movements with a number (e.g. `20h` moves cursor 20 characters left)
* `10|` moves to the 10th column of the line 
* (Pressing `ea` appends to the end of the word. Could be pretty useful)
* Can be combined with the delete command, i.e. `de` will delete to from the cursor to the end of the word.
* `gj` and `gk` can be used to move up and down display lines (lines that aren't number but aren't numbered but are in new lines due to window constraints)
* Can use `f{char}` to find a character in a line. Use the `;` and `,` to move back and forth. `F{char}` will search for it backwards
* Can use `t` and `T` instead of `f` and `F` instead - this will move it to the character before the last occurrence.
* `H`, `M`, `L` moves to the first, middle and last line of the current screen
* `<C-f>` and `<C-b>` moves forward/back one full screen
* `Ctrl` + `u`/`d` moves up/down half a screen
* `Ctrl` + `e`/`y` moves screen up/down one line
* `%` goes between matching braces, or parenthesis inside code
* Use `:N` to move to line `N`
* Use `*` to highlight the word under the cursor, and then forward-search
* Use `#` to highlight the word under the cursor, and then backward-search
* `zz` moves cursor to the middle of the screen
* `zt` moves cursor to top of screen
* `zb` moves cursor to bottom of the screen
* `]}`, `[{` moves to next unmatched `}` and `{` - probably not that useful I'm thinking
* Use `<C-o>` to go forward a jump, and `<C-i>` to go back in the window. Like forward and back in the browser
* `<C-^>` toggles between current and last buffer in a window
* `-` and `+` seem to be equivalent `k` and `j`.
* To follow links in the help files, use `<C-]>` (jump to a subject)
* `K` looks up the current word under cursor in Vim help (nice!)

## Visual Mode

Enter basic selection with `v`.

* To insert at beginning or end of every line, use visual block mode `<C-v>`. Then, then use `I` or `A` to insert or append. Press `Esc` to finish
* Can be used to select text objects using `v[ia][>\]\}]`. See pg 122 of Practical Vim to get all of the text objects and how to select them
* To clarify the above, some examples are `va}` and `vi}` (or `]`, `>` and `)`)
* To copy a block of text, use visual line mode (`V`) and then press `y` to yank, and `p` to put (paste)
* To reuse the last visual selection, press `gv`
* Use `o` and `O` to change the end of the highlighted area

To convert all the visual selection into upper/lower case, use `U` and `u` respectively.

## Insert Mode

Enter insert mode (the only mode for most other text editors) with `i`.

* `<C-y>` inserts the character that's right above the cursor into the cursor, whilst `<C-u>` deletes the current line from the cursor
* `<C-w>` deletes a word
* Similar: Replace mode: press `R` - characters after cursor will be deleted
* `<C-o>` enters 'insert normal' mode - lets you do one normal command before moving back into insert mode
* `<C-r>{register}` pastes the contents of a register. Good for just a couple of characters
* Use `<C-n>` (then `<C-p>`) to show and choose between autocomplete options

## Registers

By default, when something is yanked or deleted, it is put into the unnamed register `"`.

There are other registers: the write/read ones are `a`-`z`. The yank register is `0`.

* The `"` indicates you are about to use a register.
* To put into one of those, use `"ay` or `"ap`
* Alternate registers are `"_`, the black hole register, `"*` and `"+`, the clipboard registers
* This is something called the expression register, `"=` . In insert mode, can do quick arithmetic using it
* `"%` - name of current file
* `"#` - name of alternate file (if you two open in a tab, or something)
* `".` - last inserted text
* `":` - last Ex command (or normal)
* `"/` - last search pattern
* Use `:reg [{register}]` to display the contents of all registers/a register
* To paste into insert or command mode, use `<C-r>`, `{register}`


## Macros

* Use `q{register}` to start recording the keystrokes of the macro into a register, i.e. `qa`
    * 'Recording' will appear on the status line
    * Press `q` again to stop the recording
    * Can then inspect the contents of the register with `:reg a` (if you see a `^`, that's the `<Esc>` key)
    * `@{register}` will then play back the contents of that register
* `@@` will replay the last invoked macro
* Can prefix the macro with a count, like `10@a`. This will preform the macro 10 times, in *series*
* To execute macros in *parallel*, visually select the lines, and then do `norm[al] @q`
* If macro aborts, it will abort the rest of the macros that were queued up (series macro)
* Can also use `:normal @a`, which will execute the macro on a visual selection
* Can append to a register, say, `a`, using `qA` (i.e. uppercase of the macro register). This won't override it
* Wow... macros use the same registers as those stored with yank and delete!

### Intraline Workflow

* Position cursor at beginning of a wave
* Start recording with `qq` (begin recording into register `q`)
* End adjustment at beginning of next wave, finish by pressing `q`
* Replay with `22@q`, where 22 is an arbitrarily large number. (`@q` plays back contents from register `q`)

### Linewise Workflow

* Position cursor at beginning of line (`0`)
* Start recording with `qq`
* Finish recording `q`, with cursor remaining anywhere on that line
* Visually select lines to operate on, then do `normal! @q`

## Folds

From [vimcasts](http://vimcasts.org/episodes/how-to-fold/):

|Command|Effect|
|:---:|:---:|
|`zi`|switch folding on or off|
|`za`|toggle current fold open/closed|
|`zc`|close current fold|
|`zR`|open all folds|
|`zM`|close all folds|
|`zv`|expand folds to reveal cursor|

* `set foldcolumn=1` to see the fold marks

## Search and Replace

* `/<search term>` finds a word. Use `n` and `N` to cycle through the search results
* To move to the next matching parenthesis, type in `%` when cursor is on a `(`,`[` or `{`. To get the pair of matching parenthesis.
* Searching can be done in conjunction to being in the visual mode. For example, enter visual mode on a position, then searching for the point where we want to highlight to using / will highlight up to that point
* Use `?` to search backward (`/` to search forward)
* `:noh` will remove the highlighting (short for nohlsearch)

### Search Shortcuts

* `*` searches for the word currently under cursor
* `#` searches for the word currently under cursor, backwards
* `gd` does the same as `*`, but goes to the first instance of that word (supposed to be in the local scope)
* `gD` is also there and is supposed to do it globally

### Search Patterns

* Vim uses its own regular expressions. Can disable this with very magic switch. (`\v`)
* To ignore case, can either `:set ignorecase` or use the escape sequence `\c`
* However, `\c` and `\C` can still be used to override the `ignorecase` setting
* setting `smartcase` may cancel out `ignorecase`. If you type in a lowercase word, it will assume case insensitive. If you include an uppercase, it will assume sensitive
* `\v` pattern switch - uses very magic search - same regex engine as perl, python, ruby. Treats all characters as special, except for `-`, letters and numbers. And `#`
* `\V` pattern switch - for verbatim searches.
* Can use parenthesis to capture submatches. Very useful in combination with the substitute command. (If you want to use parenthesis for grouping instead ( & or | operator) can prefix this with `%` - this means it won't be captured)
* `\_s` matches a whitespace or a linebreak
* `+` matches the preceding atom one or more times
* < > defines a word boundary symbol
* These regexes... if you store them as `\1` and `\2`, they are recallable? Yes, in the replacement of the last search.
* To stake the boundaries of a match, use `\zs` for the start and `\ze` for the end, i.e. `/\v"\zs[^"]+\ze"` to find everything enclosed in double quotes, but only match what's within it
* Whilst in command mode, `<C-R>`,`/` inserts the last search command

### Replacing

* Replacement syntax: `:range s[ubstitute]/pattern/replacement/cgiI`
* The substitute command is `:s/old/new`. Can follow this up with any flags
* Use `:%s` to operate on whole file
* Use flags `g` to substitute all matches, and `c` for a confirmation prompt for each substitute.
* If you want to make a substitutions in just the visual block, need to use `s/\%Vtobereplaced/replacement/flags` - the `\%V` atom restricts the pattern to only be applied in the visual block
* Use an empty pattern to use the last search pattern used.
* To search multiple files, make your search pattern, then populate your args list with args {arguments}. Set `:hidden` so you can navigate away from hidden files without saving them. Then, use `:argdo %s/replaced/replacement/g`. Can also use the `e` flag to suppress error messages
* Actually, there's an easier way to do this with vimgrep
* Helpful reminder: use `\r` to replace in a newline, but use `\n` to search for one
* To count the number of word matches, use `%s/pattern//gn`

### Regex Idioms

To remove carriage returns (these are those greyed out `^M` characters you see in the buffer), use `:s//^M$//` ([Source](http://unix.stackexchange.com/questions/32001/what-is-m-and-how-do-i-get-rid-of-it))

(To input `^M`, use `<C-V> <C-M>`)

Capitalise the first letter of every word, use `s/\<./\u&/g` ([Source](http://stackoverflow.com/questions/17440659/capitalize-first-letter-of-each-word-in-a-selection-using-vim))

* `\<` matches start of word
* `.` matches first character
* `\u` uppercases character in substitution string
* `&` substitute whatever's matched on LHS

Add a comma in front of every digit, turning `2 -2  0  0 -3  1 -1 -1 -1 -2 -1  0  1  0 -2  1  1  0 -6 -3` to `2, -2,  0,  0, -3,  1, -1, -1, -1, -2, -1,  0,  1,  0, -2,  1,  1,  0, -6, -3`, use `'<,'>s/\(\d\)\>/\1,/g`.

## Global Commands

* Can use this to do a Ex command on all lines that match the pattern with `:{range}global[!]/{pattern}/[cmd]`
* `!` inverts the selection, `cmd` is another Ex command. (e.g. `normal!`). If none specified, defaults to print
* Use `<C-d>` to see all the available commands

### External Commands

* Use `:!` to execute an external command
* e.g. use `!rm filename` to remove a file (in Linux)

## Tabs and Windows

* Use `:sb[buffer number]` to split that buffer into that window
* Use `:split [filename]` to split window with the filename specified
* `gt` or `<ctrl>+<pgup/down>` shifts between tabs in gvim. Have added in a custom binding, `tg`, which goes to the previous tab.
* `<C-w>w` shifts between two windows that are open in split screen
* `:tabn[ew] filename` opens up the file in a new tab.
* `:vs[plit] filename` splits the window vertically and opens up the filename for editing (`:vs` also works)
* `:sp filename` splits window horizontally and opens up the filename for editing
* `<C-w>v` splits current window vertically.
* `<C-w>s` splits current window horizontally.
* `:on[ly]` makes the current buffer the only one in the tab
* `<C-w>, T` moves the current buffer into a new tab (`:tabedit %<CR>` does the same thing)
* Relocate the current tab with `:tabmove 99` ([Source](http://stackoverflow.com/questions/7961581/is-there-a-vim-command-to-relocate-a-tab))

### Moving Windows

* `<C-w> r` rotates the windows clockwise
* `<C-w> R` rotates the windows anticlockwise
* `<C-w> x` exchanges windows with the next one
* `<C-w> T` moves the window to the next tab
* `<C-w> [HJKL]` moves the window the furthest left, bottom, top, right

### Resizing Windows

* `<C-w> =` makes current windows equally high and wide

## Marks

* Can use marks to jump around the buffer
* Marks are created using `m{a-zA-Z}`
* Global marks can actually be used as file bookmarks! How cool is that!?
* Use `:marks` to list the current marks
* Use `:marks N` to see what is currently marked at N
* Use `:delmarks N` to delete the mark set at `N`, or `:delm` for short

If you aren't fussy about the specific column - just line, use <code>`{mark}</code> instead.

Some special, useful marks:

* Position of last change: ``.`
* Position of last jump: <code>``</code>
* Start of visual selection: ``<`
* End of visual selection: ``>`

## Buffers

* Use `:bd` to close a buffer
* Use something like `:1,100bd` to mass-close buffer (useful for getting rid of `.swp` files when you want to copy some files)
* Use `:ls` to see all the listed buffers
* Use `:b5` to switch to buffer number 5
* `:sb5` will split the window, then switch the one of the split windows to buffer 5
* `:vs | b5` will split the window vertically, then switch one of the split windows to buffer 5
* `:bn` goes to the next buffer, `:bp` goes to the previous buffer.
* Can use `:b` and then tab to see the available buffers. Done by activating wildcard menu
* When using `:ls`, here are what the symbols mean:
    * `+` means changes to be made
    * `%` means active in current window
    * `#` means alternative buffer, reachable by `<C-S-6>` (`<C-^>`) or `:e #`
    * `a` means active and loaded (but not necessarily in the current window)
* To save the buffer as something else, use `:sav[eas] new_file_name.txt`
* To delete multiple buffers, use `:3,5bd`
* Create a new buffer with `:new`
* Refresh/reload current buffer with `:edit`
* Create a new vsplit buffer with `:vne[w]`

### Collections of Buffers

* Use `:args` to print out the list of buffers in the argument list
* Arguments are populated when vim is run with a collection of files
* Use `:argd *` to delete all the arguments, or `{range}:argd` to delete a range, numbered by the order they populate the argument list
* Use :arga to add the name to the argument list. Files may be added more than once into the argument list
* Start a new argument list with `:ar[gs]! {arglist}`
* Files can also be specified with 'glob'. These are partial filenames and folders that form patterns
* Can use wildcards, `*` to match zero or more, or `**` to match zero or more recursive (used for folders). (e.g. start an arglist with all `.css` and `.js` files in current and nested directories: `:args! **/*.*css **/*.js`
* About `**` wildcards - can give it a max number of levels to match by appending a number to `**`, e.g. `**2` will go 2 levels deep
* Can use 'backticks' to call an external command. (pg 82 of Practical Vim)
* Use `:argdo` to do a command on each buffer in the argument list

## Ex Mode

* Essentially a REPL for Vimscript
* Enter with `gQ`
* If unresponsive (i.e. in ex input mode), type in `.` on a single line to exit ex input mode ([Source](http://stackoverflow.com/questions/23491720/vi-on-freebsd-stuck-into-ex-input-mode))

## Command Line Mode

* When `:` or `/` is pressed, command line mode is entered, which allows us to enter an Ex command
* Use `@:` to repeat the last Ex command
* After that, can subsequently repeat it by using `@@`
* After pressing `:/s` to enter a command, use up and down to navigate through the history
* `:his` lists the command history, whilst `:his /` searches it
* `q:` and `q/` also work
* `<C-c><C-c>` exits the command line
* Can insert contents of register into the command line with `<C-r>`, `<register>`
* Can instantly jump to a line using `:line_num`
* Can print out contents of that line with `:p` (Can combine the two with `:np`)
* `:shell` opens a shell at the pwd of the current buffer

### Range

* Can specify a range of lines with `:n,m`
* The `.` is the address for the current line
* The `$` is the address for the end of the document. (Therefore, `:.$p` prints out the contents of the current line to the end of the document)
* The `%` sign is a special range - stands for all the lines in the file. (Can do something like `%p`)
* Range can also be selected by visual selection, or marks. When pressing :, prompt will be pre-populated with `'<,'>` - this stands for current visual selection.
* Can also take regular expressions as the ranges specified
* For specifying ranges, can also use +1 or -1 to exclude lines, e.g. `:.-1,/*/+1`

* The `:t` command copies lines. In form of `:{address/range}t{destination}`. If address isn't given, will use the current line. Note that `:t`. doesn't use the register, in contrast to normal mode
* Moving is done with `:m`, and its syntax is the same as `:t`
* *Holy mother of god...* command line is powerful. Can use `:{address/range}normal {normal command}` to totally do the command to the lines specified! By default, the normal command is executed, Vim will move the cursor to the beginning of the line
* `<C-d>` and tab both work for command completion
* `<C-r><C-w>` inserts the word the cursor is currently over into the command line
* `<C-r><C-a>` inserts the WORD the cursor is currently over into the command line

### List of Ex Commmands

(From pg52 of Practical Vim)

|Command|Effect|
|:---:|:---:|
|`:[range]d[elete] [x]`|deletes [range] lines [into register `x`]|
|`:[range]y[ank] [x]`|yanks [range] lines [into register `x`]
|`:[line]pu[t] [x]`|puts text from register `x` after specified line|
|`:[range]j[oin]`|joins specified lines
|`:[range]norm{commands}`|executes normal commands on specified range|
|`:[range]s[ubstitute]/{pattern}/{string}/[flags] [count]`||
|`:[range]g[lobal]/{pattern}\[cmd]`||
|`:[range]co[py] {address}`|(same as :[range]t {address})|
|`:[range]m[ove] {address}`||

* Can use contents of the buffer as stdin or stdout with `:r{cmd}` and `:w{cmd}` (less often used)

## File Explorer

The file explorer prebuilt into Vim. Tend to use NERDTree these days, but might come in useful in a pinch.

* Use `:e .` to open file explorer. This will open up a file explorer (in current window) at where you opened up gvim from
* Actually, proper way to do this is with `:Explore` (or `:Ex` for short) - this opens up the file explorer where the current window is
* `:Sex` splits the window and opens file explorer (this is short for `:Sexplore`)
* Use `:pwd` to print the working directory
* To make the location of the current editing file the working directory, use `:cd %:p:h`. Apparently... `%p` gives the path, `:h` gets the name of the head. Or something. [Read up on file modifiers](http://vimdoc.sourceforge.net/htmldoc/cmdline.html#filename-modifiers)

## Vimgrep

* The Ex command `:vim[grep][!] /{pattern}/[g][j] {file}` can be used to search for files you specify
* There's also grep, lgrep (external application) and lvimgrep
* The commands will fill a list with the results of the search. This list is shared between all windows if grep or vimgrep is called. Otherwise, only available to current window.
* This list is known as the 'quickfix' list. Can open it with `:cw` or (:copen). Can open the local one with `:lw` (or :lopen)
* Cycle through the fixes with `:cn` and `:cp`
* In quickfix list, use `<C-w><Enter>` to open in horizontal split
* Search in current directory (shown with `pwd`) for keyword `Main` in all actionscript files: `vimgrep /Main/gj *.as`

## ctags

'Jump to function/class defintion' feature. I kind of stopped using this, but might be useful to have around

* External program that scans through a codebase and generates an index of keywords
* Can navigate around a codebase by quickly jumping to definitions of function and classes
* tags file is generated with ctags - has a few names of metadata, then lists one keyword per line, along with filename and address where that keyword is defined in the source code.
* Keywords are arranged in alphabetical order, so can rapidly locate them with a binary search
* Specification for the tags file is that the address can be an ex command. One option is using absolute line numbers - use the search command instead. As long as degenerate code doesnt' exceed 512 characters, file will remain compatible with Vi
* `p` stands for prototype
* To jump to a keyword definition, use `<C-]>`
* Vim maintains a history of the tags we visited. Use `<C-t>` to jump back in the tag history

## Plugins

Tend to use Pathogen to load these up. To reload a specific plugin in Vim, use something like `:source ~/.vim/bundle/vim-scheme/ftplugin/scheme.vim`

### Surround

[Surround operator for text objects](https://github.com/tpope/vim-surround). Use with [repeat.vim](https://github.com/tpope/vim-repeat)

* `cs'"` - changes surrounding from `'` to `"`
* `cs` can also be used to add a surrounding as well, by taking a 'surrounding target'. The surround targets are: `w` for word, `W` for WORD, `s` for sentence, `p` for paragraph
* `ys[motion][surrounding]` - adds a surrounding to the vim motion
* `yss'` - adds a surrounding to the line, without indenting. (Use this if you don't want indenting, instead of doing linewise visual selection).
* `ySS'` - adds a surrounding to the line, and indents it as well
* `ds'` - deletes the surrounding `'`; don't need anything visually selected
* Select visual selection, then press `S`, and then add your selection. This will add the surrounding, place it on a new line and indent it. Alternatively, use `s` to just add a surrounding to the selection

### Emmet Zencoding

HTML generation snippets

[Cheatsheet](http://docs.emmet.io/cheat-sheet/)

In insert mode, typing in `html:5_` where `_` is the cursor position creates a blank html5 template! Pretty neat.

``` html
div>p.foo*3>a
```

produces:

``` html
<div>
    <p class="foo"><a href=""></a></p>
    <p class="foo"><a href=""></a></p>
    <p class="foo"><a href=""></a></p>
</div>
```

In this example:

* `>` gives a nest,
* `*3` gives a multiplier
* `.foo` after a tag gives a class attribute

One more:

``` html
'div>p#foo$*3>a'
```

produces:

``` html
<div>
    <p id="foo1"><a href=""></a></p>
    <p id="foo2"><a href=""></a></p>
    <p id="foo3"><a href=""></a></p>
</div>
```

* `#foo` after a tag gives an id attribute
* `$` adds an auto-incrementing number after the name

* Use `<C-y> n` to go to next edit point. (i.e. empty tag)
* Use `<C-y> /` to toggle commenting, either in insert or normal mode

#### Expanding Abbreviations

``` html
#header+#content+#footer
```

Produces:

``` html
<div id="header">header</div>
<div id="content">content</div>
<div id="footer"></div>
```

#### Wrap with Abbreviation

* Visually select these lines with (`<S-v>`). Then, press `<C-y>`, `,`
* After this, 'Tag:' should come up at the normal mode prompt. Type in what you want to wrap it with. Use an asterisk for the innermost tag to specify that this tag is to be wrapped for EACH line (rather than the whole block).
* i.e. for the below example, try wrapping with `ul>li*`:

```
test1
test2
test3
```

### Pathogen

[Package manager](https://github.com/tpope/vim-pathogen) for Vim.

* use `:call pathogen#helptags()` to replenish the helptags

### Snipmate

* `${1[:description]}` refers to the variable that can be set
* `$1` refers to it elsewhere.

### Markdown

Readme [here](https://github.com/plasticboy/vim-markdown), although have found that it becomes slow on large markdown files

* `gx` to open link in browser

### NERDTree

[File explorer](https://github.com/scrooloose/nerdtree) alternative to the built-in netrw.

* Open up help with `?`
* Open, close a directory with: `o`
* Recursively open/close directory with `O`
* Close all nodes apart from the on you're currently in: `C`
* Go to parent node: `p`
* Go to root: `P`
* Menu (can add new file, directory,delete): `m`
* Refresh current dir: `R`
* Change the pwd to current dir: `cd`
* Open vsplit: `s`
* Open in new tab: `i`
* Recursively open: `O`
* Use `u` and `U` to go up directories. (`U` keeps current node expanded as you go ascend)
* Close nerdtree pane with `q`
* Expand nerdtree pane with `A`

### Sparkup

Similar to zencoding.

Use doctype to get the declaration up (actually done with Snippets).

``` html
doctype
html>head>title{hey there}+link[href=styles.css]<body>script[src=js/jquery.js]
```

produces:

``` html
<!DOCTYPE HTML>
<html>
    <head>
        <title>hey there</title>
        <link href="styles.css" rel="stylesheet" />
    </head>
    <body>
        <script src="js/jquery.js" type="text/javascript"></script>
    </body>
</html>
```

Nice!

### CtrlP

Constant time buffer switcher. Use [this](https://github.com/ctrlpvim/ctrlp.vim) repository instead, since the original one no longer being maintained.

* When open, use `F5` to refresh the cache (in case you created a new file)
* With CtrlP open, use `<C-v>`, `<C-s>` or `<C-t>` to open file in new vsplit, ssplit or tab respectively

### Fugitive

[Git wrapper](https://github.com/tpope/vim-fugitive). [Partial patches](http://vimcasts.org/episodes/fugitive-vim-working-with-the-git-index/)

* Target branch (e.g. master) is the branch you are currently on. Denoted with `//2`
* Merge branch (e.g. feature) is the branch you want merged into the current branch. Denoted with `//3`
* Use `:diffput` on the target/merge branch to use that branch's change
* Use `:diffget //2` or `:diffget //3` on the middle window to use the specified branch's change
* While in 2-way diff mode:
    * Use `:diffupdate` to update the colours after a `diff(get)|(push)`
    * Use `]c` and `[c` to jump to next and previous 'hunk' (change)
    * Use `dp` (`diffput`) on the working copy to stage a patch
    * Use `do` (`diffobtain`) on the git index to stage a patch deletion
    * Save the git index to stage those changes
    * `:Gwrite` in working copy buffer stages all the changes in that file
    * `:Gread` in working copy discards all working tree changes of that file
    * `:Gwrite` in index file discards all working tree changes of that file
    * `:Gread` in index file stages all the changes in that file

#### GStatus

* Use `<C-n>` and `<C-p>` to move between files
* Use `-` to stage and unstage. **also works in visual mode!**

#### GLog

* `:Glog [number]` loads previous `[number]` revisions into the quickfix list
* `:Gedit` with no arguments brings it back to the working copy

### Syntastic

* Check currently activated checkers with `:SyntasticInfo`
* Currently mapped to `,sc`

#### JSHint

Won't run if you have an incorrectly formatted `package.json`, for some reason.

### UltiSnips

* Make sure Vim has been built with Python support
* Use `<C-j>` to jump to next tabstop, and `<C-k>` to jump to previous

### vim-snippets

Add these to the default snippets files:

#### Javascript
    
``` bash
snippet cll
    console.log('${1:decription}: ', $1);
```

#### Python

``` bash
snippet print
    print '${1: var_name}:', $1
```

#### Markdown

* `[c` is a useful expansion for inserting hyperlinks with the url coming from the system clipboard register

Ultisnips:

``` bash
snippet gl "Glossary entry" b
* **${1:entry}**: ${2:definition}
endsnippet
```

## Misc

* [Search/replace unprintable characters](http://stackoverflow.com/questions/2798398/how-to-search-and-replace-an-unprintable-character/2801132#2801132)
* Replace another character (e.g. `\t`for a newline with `%s/\t/\r/g` ([Source](http://stackoverflow.com/questions/71323/how-to-replace-a-character-for-a-newline-in-vim))
* Unix uses `0xA` (Linefeed) for the newline character
* Windows uses `0xA` and `0xD` (Carriage return). Carriage returns are displayed as `^M` characters in Vim
* Check colorscheme with `echo g:colors_name` ([Source](http://stackoverflow.com/questions/2419624/how-to-tell-which-colorscheme-a-vim-session-currently-uses))
* Use one of the following ex-commands to convert DOS formatted files to Unix:
    * `:wc ++ff=unix`
    * `:set ff=unix`
    * `:%s/\r/\r/g`
* Change file encodings to `utf-8` (in case it's using another encoding like `latin1`) with `:set fileencoding=utf8`
* Spaces to tab with: `:set noet|retab!` (or `:set expandtab`, `:retab`)
* Chords like `<C-S>` and `<C-q>` get stuck in the bash terminal; put `stty -ixon` in `.bashrc`. ([Source](http://superuser.com/questions/588846/cannot-get-vim-to-remap-ctrls-to-w))
* To find the directory this is in, use `:echo $MYVIMRC` (this is an environment variable that vim sets if it finds the vimrc file in your home directory)

### Non-ASCII characters

* A good font to use for these (in Cygwin, at the very least) is DejaVu Sans Mono, font 11
* Useful for taking math notes, the setting `set encoding=utf-8` will allow Unicode to be shown.
* `:digraphs` shows how to enter Unicode characters
* [Useful math reference](http://www.alecjacobson.com/weblog/?p=443)

#### Dipgrahs

In insert mode, use `<C-k>, KEYCODE` for entering an Unicode character. Some commonly used ones:

Maths:

|Symbol|Preview|Keycode|
|:---:|:---:|:---:|
|element of|∈|`(-`|
|not elem of|∋|`-)`|
|for all|∀|`FA`|
|there exists|∃|`TE`|
|subset of|⊆|`(_`|
|equivalance|≡|`3=`|
|left arrow|←|`<-`|
|right arrow|→|`->`|
|infinity|∞|`00`|
|if-then|⇒| `=>`|
|turnstile|├|`vr`|
|gte|≥|`>=`|
|lte|≤|`=<`|
|and operator|∧|`AN`|
|or operator|∨|`OR`|
|approx equal|≈|`?2`|
|multiply|×|`/\`|
|intersection|∩|`(U`|
|union|∪|`)U`|
|perpendicular|⊥|`-T`|

Greek:

|Symbol|Preview|Keycode|
|:---:|:---:|:---:|
|phi (lowercase)|φ|`f*`|
|rho (lowercase)|ρ|`r*`|
|mu|μ|`m*`|
|sigma (lowercase)|σ|`s*`|
|sigma (uppercase)|Σ|`S*`|
|epsilon (lowercase)|ε|`e*`|

Misc:

|Symbol|Preview|Keycode|
|:---:|:---:|:---:|
|up arrow|↑|`-!`|
|down arrow|↓|`-v`|
|subscript 1|₁|`1s`|
|superscript 1|¹|`1S`|
|e acute|é|`e'`|
|a acute|á|`a'`|
|tick|✓|`OK`|
|cross|✗|`XX`|

#### Unicode characters

UTF-8 is a character encoding (Universal Character Set Transformation Format 8-bit) capabale of encoding all the characters in Unicode (computing industry standard for consistent encoding, representation and handling of data).

In insert mode, use `<C-v> <Keycode>` to enter a Unicode character

|Symbol|Preview|Keycode|
|:---:|:---:|:---:|
|subscript|ₙ |2099|
|subscript|ᵢ|1D62|
|subscript|ⱼ|2C7C|
|subscript|ₖ |2096|
|not an element of|∉|2209|
|ordinal indicator|ª|2209|
|r carot|ř|u0159|
|i acute|í|u00ed|
|xor|⊕|u2295|
|not equal|≠|u2260|


### Prose

Vim is good for writing unstructured prose. To set sensible word wrap, use the following:

* `:set wrap`: (this is on by default) - wraps long lines instead of not showing them
* `:set linebreak`: breaks when you come to a character specified by `breakat`

* To perform a word count, use `g <C-g>`
* To perform a spell-check, use `:set spell`
    * `]s` to next mispelled word after cursor
    * `]s` to previous mispelled word before cursor
    * To disable, `:set nospell`
    * To toggle, `:set spell!`
    * Bring up suggestions with `z=`

#### Thesaurus

* Download `files.zip` thesaurus from [Gutenburg](http://www.gutenberg.org/files/3202/)
* Extract `mthesaur.txt` somewhere
* Add to vimrc with something like: `set thesaurus+=/home/jsmith/mthesaur.txt`
* Activate with `<C-x> <C-t>` while in insert mode
