# REPLMasteryWorkshop - JuliaCon2022

This workshop will be a jam-packed, hands-on tour of the Julia REPL so that beginners and experts alike can learn a few tips and tricks.
Every Julia user spends a significant amount of coding time interacting with the REPL.
My claim for this workshop is that all Julia users can save themselves more than 3
hours of productive coding time over their careers should they attend this workshop, so why not invest in yourself now?

### Plan for the material that will be covered:

1. Download Julia from [julialang.org](julialiang.org).
2. Click/open the executable to pull up the `JuliaREPL`
3. If you need colors (like I do), type this in:
```julia-repl
julia> using Pkg;

julia> using Pkg.add("OhMyREPL")

julia> using OhMyREPL
```

You should be good to go! 

A less hands-on (but valuable reference) for the information inside this tutorial is in the [Julia REPL manual](https://docs.julialang.org/en/v1/stdlib/REPL/). "Tightening" the feedback loops to find help in 
- the manual
- inside the Julia REPL itself
- with others
- and online
will likely be worthy investment to those that seek to master the Arts of Julia. Don't underestimate mechanical fluency!

Happy hacking!

## Navigation 
----
We're going to start with the *very* basics. It's a good idea to think of this as musical piano scales - we're going for examples to trigger your muscle memory.
### Basic flow in the `Julia mode`
```julia-repl
julia> x = 3+3
6
```
Notable points: You can `copy/paste` input from anywhere into a Julia REPL. Try it now, to make sure you don't need to erase the `julia>`.

Now, type in
```julia-repl
julia> ans
```
And notice the `ans` evaluates to the previously evaluated value. This is extremely useful, and can save your bacon when not re-running expensive calculations.

This is ~about as much mileage as you can extract from many other REPL in many other languages - but we should be *greedy*, because this is Julia, and we expect the best in interactive and performant computing.

We will now squeeze the most out of our `Julia mode` of this REPL. Type the following into the REPL:
```julia
for i in 1:3
    parse(OOPS, "123")
end
```

### Basic Commands

The manual invites you to try the following:
* `Ctrl+D`, to quit (also written as `^D`
* `Ctrl+C` will interrupt/cancel ongoing actions
* `Ctrl+L` will clear your entire screen (I spam this so much - I love it.)
* `Alt+Enter` will let you type in a newline without evaluating the REPL result.
Try the following:
    * Type the `UP` Arrow to get to the definition of `x`. Then press `Enter`.
    This scrolls through your REPL history.
    * Get back to a previous definition in your REPL, press `Enter`, and then `Down`.
    You should notice that you can "get back" to where you started evaluating.
    This is **very** useful for when you have selected the "good REPL history" and you can begin a presentation there.
* Moving around
Moving around with arrow keys is fine, but there's so much more power to learning to move around without resorting to the keys. Try moving around only through the `X`s in the following string:
```julia
# Try and make it to the apple!
snek = """
🐍XXXXX             XX   
    XXX   XXXX    X  X 
      X   X  X    X  X 
      X   X  XXXXXX  X 
      XXXXX          X 
                     X🍎
"""
```

Remember:
* Up: `Ctrl+P` (Memorization tip: `P` is for `Previous`)
* Down: `Ctrl+N` (`Next`)
* Left: `Ctrl+B` (`Back`)
* Right: `Ctrl+F` (`Forward`)

Now try:
```julia
function<CTRL+P>
```
That means that you should type in `Ctrl` and `P` at the same time, just after you have typed in `function`, no spaces.
You should have scrolled "back in time" through your REPL history and hit the first matching previous time you typed in `function`. (The same works with `UP` arrow, btw.)

This trick let's you veeeeery quickly find stuff in your looooong REPL history if you kinda sorta remember what something was called. 

If you liked this trick, please spam your favorite emoji in the Youtube/Twitch/Discord chat and `@miguelraz` on twitter with the `#JuliaCon2022` hashtag.

We're gonna build the hype :D.

---

Back to movement exercises.

Try moving through the four courners of snake box but now with the more powerful
* `meta+F` (word Forward)
* `meta+B` (word Backward)
* `Ctrl+A`/`Home` (At Home, beginning of line)
* `Ctrl+E`/`End` (go to End of line)

Once you've tried a few iterations of the snake and gone back and forth a bit, please ask a question.



### Variables
No, you can't delete your variables in Julia (it makes the compiler and Jeff Bezanson sad).
But you can see what has been defined!
Try
```julia
varinfo()
```

This should show you the variables that are defined and how much they "weigh" in memory.

- `ans` is bound to whatever you evaluated last
- `Base` is where all the batteries-included functionality is prepared
- `Core` is the place where Julia starts itself up from - we don't need to worry about it.

Try defining some new variables and seeing how much they weigh in memory.
which of these is lightest?
```julia
a = 1:1e6
b = collect(1:1e6)
```

### Shortcuts and keyboard combinations
We've already seen a few `Ctrl`s here and there, but there's a few more where you might not have expected them. Again, [please do read the manual and try them out](https://docs.julialang.org/en/v1/stdlib/REPL/#Key-bindings) (even if they are classic Emacs key chords, I know.)
* `meta+<`/`meta+>` change to your first/last entry in this REPL session
* `meta+Backspace` delete the previous word, like the following `Mushrooms`

```
words = """
Badger Badger Badger Mushroom 
Badger Badger Mushroom Badger
Badger Mushroom Badger Mushroom 
"""
```

or the spurious `TODO` here:
```julia
function hello(x)
    println(TODO"Yes hello $x)
end
```

You can also use 
* `meta+d` to delete the forwar`d` word

And also use 
* `Ctrl+W`/`^W` to delete `W`hitespace in the following functions
```julia
3 + "banananananannananananananananananananannanana" 3
OOPS_GARBLED_INPUT simple(x) = x^2
```

(BTW, have you tried using `Ctrl+Right`/`Ctrl+Left` when going through an expression? It's not a bad backup...)

Try this now:
```
julia> @edit @less
```
You should get a gnarly stack trace.

Now type in `2+Ctrl+Q` (beware of some of your shortcuts exiting your terminal window.)

Your normal IDE/Editor of choice should have shown you where the funciton that is defined. If this didn't work, make sure to set 
```julia
ENV["JULIA_EDITOR"] = "/usr/bin/vim"
Env # Hmmmm... I wonder if there's an easier way to explore all this input...
```
or whatever floats your ⛵. This configuration should persist between Julia sessions. (Choosing a lightweight IDE that doesn't spin up a Julia LSP session upon every invocation is good for ninja editing files and staying nimble).

Flow tip:
```
Get an error -> Jump into the stacktrace of your package -> exit your editor -> re-run your code
```

We'll talk a bit more about Julia configuration in a bit, stay tuned! We're almost done with the  gnitty exercises.

**Pro tip**: Whenver you see pretty formatted outfit like the stack traces, you *should* be able to jump to it with `Ctrl+Q` as well.
Try this:
```julia
methods(parse)
```
And jump to one of them.

#### Cultural aside - <TAB> Galore!

When starting with Julia, it can feel very *big*.

What the heck is parsing? Bootstrapping? A compiler? That funky dragon in the LLVM logo that haunts my dreams?

You're about to learn a *very* powerful tip: Just about everything you can touch in the Julia REPL expands/auto-completes when you use the amazing `<TAB>`. Try it!
```julia
using Lin<TAB> 
par<TAB>
fi<TAB>
String.<TAB>
lines = readlines("file<TAB>")
```

This little nugget of wisdom, judiciously used will let you quickly get a grasp of what's available in a library that you just imported - functions, fields, types, etc. For example, use it to find all macros defined in `Base`:
```julia
@<TAB>
```

#### Editing

Let's power up our search by using fuzzy-finding in reverse mode with:
* `Ctrl-R`/`Ctrl-F` (Reverse/Forward)

Cool, huh?

Now let's keep going.

Run this line:
```julia
# Horrible, horrible Julia 🤮
function hamming(s1, s2)
    counter = 0
    length(s1) == length(s2) || break
    for i in 1:length(s1)
        if s1[i] != s2[i]
            counter = counter = 1
        end
    end
    return counter
end
```

1. Place your cursor `🔲` at the beginning of the `for` loop.
2. Now press `Ctrl-Space` - to mark a spot
3. Move your cursor to the `return counter` line and press `Ctrl-X` (E`X`change)

A couple of times to jump back and forth from where you where.
This is useful once your functions start getting longer and longer.

Next drill: **Deleting**

Run this line:
```julia
# Horrible, horrible Julia 🤮
! function hamming(s1, OOPS s2)
    counter = 0 OOOOOOOOOOOOOPS           # Ctrl+K
    for i in ! 1:length(s1)               # Ctrl+D
        if s1[i] OOPS != s2[i]            # Ctrl+W
            OOPS counter = counter = 1    # Ctrl+W
            OOPS OOPS OOPS OOPS           # Ctrl+K
        end
    OOPS end
    return COUNTER                        # meta+l
    length(s1) == length(s2) || breka     # Ctrl+T, then meta-Up
OOPS end
```
It seems a very dedicated cat 🐈 ran across our keyboard (and maliciously inverted the length check???). The following should be useful for getting rid of may of those mistakes:

* `Ctrl-/.`/`Ctrl-_` to undo our previous actions (Help? Can't get this to work?)
* `Ctrl-K` will `K`ill to the end of the line and place it in the `kill ring`/clip board
* 

However, Julia ships with a much more structured way to include "helpful" information along code, and that can be done by pressing `?` via the help mode.

### REPL Modes 
  - Help mode,
  - Shell mode,
  - Pkg mode,
  - workflow demos for contributing code fixes,
  - REPLMaker.jl BuildYourOwnMode demo,
* Cross language comparison of REPL features
* Internals and configuration 
(Cultural aside: using `grep`, `bat` and `tree` and `git`:)
  - Basic APIs,
  - display control codes,
  - terminals and font support,
  - startup file options, prompt changing

  - flag configurations (quiet, banner)
##### Tools and packages 
  - OhMyREPL.jl, 
  - PkgTemplates.jl, 
  - Eyeball.jl, 
  - TerminalPager.jl, 
  - AbstractTrees.jl,
  - Debugger.jl,
  - UnicodePlots.jl,
  - ProgressMeters.jl,
  - PlutoREPL.jl (???) **project**
  - Term.jl

### Miscelanea
- TerminalMenus.jl in base
- VideosInTerminal.jl + ImagesInTerminal.jl like Jesse Betancourt's 
- DoctorDoctrings.jl and hijacking REPL history
- InteractiveErrors.jl
- AbbreviatedStackTraces.jl
- pkg prompt with temp directory
- TerminalPager.jl for DataFrames.jl stuff

- `] add Foo; undo`!
- Latex shortcuts via [Keno](https://twitter.com/KenoFischer/status/1402828171213479936)

- Jacob Quinn: ?foo gives you help, but ??foo gives you the stuff under "# Extended help"
https://julialang.slack.com/archives/C6FGJ8REC/p1623860727294500

- `LLVM_JULIA_ARGS=-time-passes ./julia -e 'using Plots; plot(1:10)'`
- switch repl modes via menu https://github.com/JuliaLang/julia/pull/33875
- fzf reverse search
- https://github.com/JuliaLang/julia/pull/38791

- Reverse latex/emoji lookup with `?\partial`

- Stack traces with `CTRL+Q`, but also `methods(foo) + 1 + CTRL+Q`.

- Change your prompt:
```julia-repl
julia> Base.active_repl.interface.modes[1].prompt = "julia 😷>"
```

- `] activate @juliaimages`


### Ascii goodness:
```
         ▄              ▄    
        ▌▒█           ▄▀▒▌   
        ▌▒▒█        ▄▀▒▒▒▐   
       ▐▄█▒▒▀▀▀▀▄▄▄▀▒▒▒▒▒▐   
     ▄▄▀▒▒▒▒▒▒▒▒▒▒▒█▒▒▄█▒▐   
   ▄▀▒▒▒░░░▒▒▒░░░▒▒▒▀██▀▒▌   
  ▐▒▒▒▄▄▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▀▄▒▌  
  ▌░░▌█▀▒▒▒▒▒▄▀█▄▒▒▒▒▒▒▒█▒▐  
 ▐░░░▒▒▒▒▒▒▒▒▌██▀▒▒░░░▒▒▒▀▄▌ 
 ▌░▒▒▒▒▒▒▒▒▒▒▒▒▒▒░░░░░░▒▒▒▒▌ 
▌▒▒▒▄██▄▒▒▒▒▒▒▒▒░░░░░░░░▒▒▒▐ 
▐▒▒▐▄█▄█▌▒▒▒▒▒▒▒▒▒▒░▒░▒░▒▒▒▒▌
▐▒▒▐▀▐▀▒▒▒▒▒▒▒▒▒▒▒▒▒░▒░▒░▒▒▐ 
 ▌▒▒▀▄▄▄▄▄▄▒▒▒▒▒▒▒▒░▒░▒░▒▒▒▌ 
 ▐▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒░▒░▒▒▄▒▒▐  
  ▀▄▒▒▒▒▒▒▒▒▒▒▒▒▒░▒░▒▄▒▒▒▒▌  
    ▀▄▒▒▒▒▒▒▒▒▒▒▄▄▄▀▒▒▒▒▄▀   
      ▀▄▄▄▄▄▄▀▀▀▒▒▒▒▒▄▄▀     
         ▀▀▀▀▀▀▀▀▀▀▀▀        
```

### Projects
* The REPL has Emacs-y bindings by default - Can you try adding Vim keybindings?

### Issues to pickup:
* `@which parse(Int, "123")` doesn't print with regular highlighting
* 
* Alright, `<TAB>` autocompletes, but why doesn't it show me colors of functions/Structs/Modules/vars/constants in different formats? Can you do it?

