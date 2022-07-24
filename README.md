# REPLMasteryWorkshop - JuliaCon2022

```julia-repl
julia> using JuliaCon, Distributed

julia> @everywhere Juliacon2022().today()
```

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
🐍XXXXX           XXXX   
      X   XXXX    X  X 
      X   X  X    X  X 
      X   X  XXXXXX  X 
      XXXXX          X 
                     X🍎
""";
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
* `Ctrl+Right`/`Ctrl+Left` will skip over an entire word

```
words = """
Badger Badger Badger Mushroom 
Badger Badger Mushroom Badger
Badger Mushroom Badger Mushroom 
""";
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
parse(<TAB>) # Shows all methods
parse(Int, <TAB>) # Narros to all methods that start with Int!
fi<TAB>
String.<TAB>
lines = readlines("file<TAB>")
parse(Int, <TAB>)
\alpha<TAB>
\:boat:<TAB> |> clipboard
; cd ~/.julia/<TAB>
```
... and you can setup your own latex shortcuts ([Hat tip to Keno 🤠](https://twitter.com/KenoFischer/status/1402828171213479936)!
```
using REPL
REPL.REPLCompletions.latex_symbols["\\pol"] = "`∂⃖" # instead of \partial<tab>\overl<tab>a<tab><tab>`
```

...[and many more](https://github.com/JuliaLang/julia/blob/c5a63d8b6465c97ffef282b81d5a42627fe1468b/stdlib/REPL/src/REPLCompletions.jl).

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
    length(s1) == length(s2) || return -1
    for i in 1:length(s1)
        if s1[i] != s2[i]
            counter = counter + 1
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
    length(s1) == length(s2) || erturn -1     # Ctrl+T, then meta-Up
                    OOPS end              # meta-Left
```
It seems a very dedicated cat 🐈 ran across our keyboard (and maliciously inverted the length check???). The following should be useful for getting rid of may of those mistakes:

* `Ctrl+/.`/`Ctrl+_` to undo our previous actions (Help? Can't get this to work?)
* `Ctrl+K` will `K`ill to the end of the line and place it in the `kill ring`/clip board
* `Ctrl+D` will delete one character and a`D`vance the cursor
* `Ctrl+W` will delete previous text going up to whitespace
* `meta+l` will lowercase a word
* `Ctrl+T` will `T`ranspose the characters about the cursor, use it on the malformed `break`
* `meta+Up` will "float" the entire line up to where it's supposed to go
* `meta-left` to re-indent the last line appropriately

**TODO**: Master the kill rings...

### Custom keybindings

[The manual specifies how to setup your own keybindings](https://docs.julialang.org/en/v1/stdlib/REPL/#Customizing-keybindings).
Here's what a "minimalist" vim profile would look like for me:
```julia
import REPL
import REPL.LineEdit

const mykeys = Dict{Any,Any}(
    # Up
    "^k" => (s,o...)->(LineEdit.edit_move_up(s) || LineEdit.history_prev(s, LineEdit.mode(s).hist)),
    # Down
    "^j" => (s,o...)->(LineEdit.edit_move_down(s) || LineEdit.history_next(s, LineEdit.mode(s).hist))
)

function customize_keys(repl)
    repl.interface = REPL.setup_interface(repl; extra_repl_keymap = mykeys)
end

atreplinit(customize_keys)
```
but you can find oodles more actions in the [LineEdit.jl](Lang/julia/blob/master/stdlib/REPL/src/LineEdit.jl)

However, Julia ships with a much more structured way to include "helpful" information along code, and that can be done by pressing `?` via the help mode.

### REPL Modes 

At time of writing, there are 4 standard Julia REPL modes:
1. Julian mode
2. Help mode, with `?`
3. Pkg mode, with `]`
4. Shell mode, with `;`
#### Help mode

The king of kings. Instead of needing to open a browser window for every

Try the following:
```julia
?parse
```
Your prompt should now look like `?>` and turn yellow.

When you define a function, you can also define a `docstring` by writing a string comment just above it.
That string gets rendered as Markdown within the terminal.

Try this
```julia
" Super helpful string comment"
hamming(s1, s2) = mapreduce(!=, +, s1, s2)
```
or this
```julia
@doc "Also clever insight" hamming
```

But there's many kinds of "markup" that the Julia REPL allows.
Try adding:
- a header
- a note
- a compat warning above Julia 1.6
- julia examples 
- bolded text
- a part that says `# Extended help` and then running `??parse` 👀
- `?DataFrames` - if you don't have a docstring for your main Module, it will just display your repo's `README.md`.

(Hint: Look at `?parse` and try and find all the doc comments with `@edit parse(Int, "123")`)

Interestingly, Julia has a particular flavor of documentation because of multiple dispatch - when new methods are defined for old types, those get also added to the documentation.

Try this
- add another docstring to `parse` in a new module to a local type and see that the docs get updated

You can also use the `apropos("Unicode")` function, or `?>"Unicode"` to get a dump of all function docstrings that contain the string "Unicode".

If you know some regular expressions, you can also ask with those!

Try this:
```julia
?r"arg[0-9]"
```
To find all docstrings that contain `arg` followed by a number.

Try this
```julia
julia> 'c'
```

Julia will kindly show you the Unicode character representation of whatever character you input.

Try it with emojis!

Try this:
```julia
?> ∂
"∂" can be typed by \partial<tab>
```
This is called reverse latex/emoji lookup! If you come across a weird symbol, you can just ask Julia how to type it.

#### Shell mode

This is a "fake" shell mode - ideally best for jumping around directories with `cd ~/.julia` and cleaning up `git` stuff really quick.
Try this:
1. Go into a Package you own
2. type `; vim README.md` or your favorite editor
3. Fix a typo, save and quit
4. Commit the file and push to the repo.

I said "fake" because it's not really a shell - it's an emulated version run by Julia (see [the code here](https://github.com/JuliaLang/julia/blob/master/base/shell.jl). 

Try this 💎:
```julia
shell> echo $(readdir())
```
You can, however, run Julia code "inside" that emulated shell. Neat, huh!

#### Pkg mode

Alright, now for the *real* productivity booster: The Pkg REPL. There's many more configs than what I will talk about, but these will get you 95% of the way there as a confident Julia user.
You can [checkk all the commands in the Pkg.jl manual](https://pkgdocs.julialang.org/v1/repl/)

* `]add X Y Z` will add `X Y Z` packages. 
Try this:
```julia
]add Diff<TAB>
```
It will autocomplete with matching package names in the registry!

Try this when developing a package
```julia
]test X
```
or just `]test`. This will run all the tests under `tests/runtests.jl` and include some really nice output. This is *vital* to knowing that other's people's code works on your computer!

Try this:
```julia
]status
```
You'll get an info dump of all the packages and the version that they are at in the active environment. 

To start an environment, do this:
```julia
]activate --temp
```
(or `]activate --temp` if you want a quick sandbox to debug/setup a MWE!). You will see you prompt change to `MyPkg>` in blue.
This now makes all your installations *only* valid for the current environment! 

Congrats! You have now graduated from the I-don't-have-to-spend-more-time-fighting-pip-for-the-rest-of-my-life academy!

If you want to eagerly download all the dependecies of an environment,
```julia
]instantiate
```
Will pull them in.

```julia
]dev YourPackage
```
Will start a new "development" version of a package that you can locally make changes to in `~/.julia/dev` - so you don't have to mess with your installed packages either!

Small tip - if you've been running Julia for a while (a few versions now), try running 
```julia
]gc
```
To get rid of a bit of cruft you may have accumulated.

  - workflow demos for contributing code fixes
  - Revise.jl
  - REPLMaker.jl
   BuildYourOwnMode demo,
* Cross language comparison of REPL features
(Cultural aside: using `grep`, `bat` and `tree` and `git`:)
* terminals and font support
* startup file options
* prompt changing
* Easter eggs in the chat? 🥚 🎉 👀

* flag configurations (quiet, banner)
##### Tools and packages 
  - `@code_*` 
  - `BenchmarkTools.jl`
  - OhMyREPL.jl, 
  - TheFix.jl
  - Latexify.jl
```julia
using Latexify
arr = ["x/y" 3//7 2+3im; 1 :P_x :(gamma(3))]
latexify(arr)
```
  - PkgTemplates.jl
```julia
t = Template(user = "miguelraz")
t("MySuperPackage")
```
  - Eyeball.jl
```julia
using Eyeball
a = (h=rand(5), e=:(5sin(pi*t)), f=sin, c=33im, set=Set((:a, 9, rand(1:5, 8))), b=(c=1,d=9,e=(i=9,f=0)), x=9 => 99:109, d=Dict(1=>2, 3=>4), ds=Dict(:s=>4,:t=>7), dm=Dict(1=>9, "x"=>8))
eye(a)
```
  - TerminalPager.jl, 
```julia-repl
julia> rand(100, 100) |> pager

julia> pager(rand(100, 100))
```
  - AbstractTrees.jl,
```julia-repl
julia> print_tree(FloatTree(NaN, [FloatTree(Inf, []), FloatTree(-Inf, [])]))
NaN
├─ Inf
└─ -Inf
```
  - Debugger.jl / Cthulhu.jl / SnoopCompile.jl
```julia
using Debugger
@enter parse(Int, 123)
```
  - UnicodePlots.jl
  - ProgressMeters.jl
```julia
using ProgressMeter

@showprogress 1 "Computing..." for i in 1:50
    sleep(0.1)
end
```
  - Term.jl
  - PrettyTables.jl
  - PlutoREPL.jl (???) **project**

### Miscelanea
- `juliaup`: Be comfortable switching between channels!
- TerminalMenus.jl in base
- [Terminal User Interfaces in Julia](https://www.youtube.com/watch?v=-TASx67pphw) by Dheepak Krishnamurthy
- VideosInTerminal.jl + ImagesInTerminal.jl like Jesse Betancourt's 
```julia-repl
julia> using VideoInTerminal

julia> framestack = map(i->rand(Gray{N0f8},60,40), 1:200); # a vector of images of the same type and dims

julia> play(framestack) # play through the framestack

julia> colorcube = rand(Gray{N0f8},60,40,30);

julia> play(colorcube, 2) # play slices along dim 2

julia> play("path/to/video.mp4")
```

And if you wanna try out something kinda funky...
```julia-repl
julia> showcam
```
- [PortAudio.jl](https://github.com/juliaaudio/portaudio.jl) - I mean, we might as well record audio now, right?
```julia-repl
julia> import LibSndFile # must be in Manifest for FileIO.save to work

julia> using PortAudio: PortAudioStream

julia> using SampledSignals: s

julia> using FileIO: save

julia> stream = PortAudioStream(1, 0) # default input (e.g., built-in microphone)

julia> buf = read(stream, 5s)
480000-frame, 2-channel SampleBuf{Float32, 2, SIUnits.SIQuantity{Int64,0,0,-1,0,0,0,0,0,0}}
10.0 s at 48000 s⁻¹
▁▄▂▃▅▃▂▄▃▂▂▁▁▂▂▁▁▄▃▁▁▄▂▁▁▁▄▃▁▁▃▃▁▁▁▁▁▁▁▁▄▄▄▄▄▂▂▂▁▃▃▁▃▄▂▁▁▁▁▃▃▂▁▁▁▁▁▁▃▃▂▂▁▃▃▃▁▁▁▁
▁▄▂▃▅▃▂▄▃▂▂▁▁▂▂▁▁▄▃▁▁▄▂▁▁▁▄▃▁▁▃▃▁▁▁▁▁▁▁▁▄▄▄▄▄▂▂▂▁▃▃▁▃▄▂▁▁▁▁▃▃▂▁▁▁▁▁▁▃▃▂▂▁▃▃▃▁▁▁▁

julia> close(stream)

julia> save(joinpath(homedir(), "Desktop", "myvoice.ogg"), buf)
```
- DoctorDoctrings.jl and hijacking REPL history
- BinaryBuilder.jl
```julia
using BinaryBuilder
BinaryBuilder.run_wizard()
```
- InteractiveErrors.jl
- AbbreviatedStackTraces.jl
- pkg prompt with temp directory - incredibly useful for debugging/setting up MWE
- `] add Foo; undo`!

- Jacob Quinn: ?foo gives you help, but ??foo gives you the stuff under "# Extended help"
https://julialang.slack.com/archives/C6FGJ8REC/p1623860727294500

- `LLVM_JULIA_ARGS=-time-passes ./julia -e 'using Plots; plot(1:10)'`
- https://github.com/JuliaLang/julia/pull/38791

- Change your prompt:
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
* The REPL has Emacs-y bindings by default - Can you try adding Vim keybindings? Normal editing is a more mechanical PR. Composing the vim keys is where it's interesting!
* Can you get regular expressions to dump into the terminal as you can? [Try this for inspiration](https://twitter.com/thingskatedid/status/1316074032379248640).
* [Data structure graphs would also be amazing](https://twitter.com/thingskatedid/status/1386077306381242371) to have at the Julia terminal - anyone wanna give it a shot?

### Issues to pickup:
* `@which parse(Int, "123")` doesn't print with regular highlighting
* Alright, `<TAB>` autocompletes, but why doesn't it show me colors of functions/Structs/Modules/vars/constants in different formats when I do `LinearAlgebra.<TAB>`? Can you do it?
* "terse" `]test` mode flag that doesn't print all the Pkg deps and status?
* switch repl modes via menu https://github.com/JuliaLang/julia/pull/33875
* Why is the shell mode not better documented? Send a PR!

