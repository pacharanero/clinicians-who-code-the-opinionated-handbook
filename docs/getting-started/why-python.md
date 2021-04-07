## Why Python?

Why is Python a good language to learn first?

### Ease of learning and use

Python is taught in schools across the world, to children from around the age of 8 upwards. It's readable enough to make sense even if you don't actually code yet.

As an *interpreted* (as opposed to *compiled*) language, the 'type-it-*try-it*-fix-it-*try-it*' cycle is that much shorter.

It's supported in 'serverless' deployment features by basically all the major platforms such as Heroku, Microsoft Azure, Amazon Web Services, so it's quite easy to deploy experiments and demos.

You can use it in Jupyter Notebook form


### Python's the de-facto science language

Python is widely used for all the 'standard' and common things that we use code for - scripting, small simple programs, desktop programs with a graphical user interface, and web programming.

In addition, it's been adopted as the primary language of the scientific community, for used ranging from astrophysics to bioinformatics. Python's scientific and statistical libraries are mature and well supported.

Python is also used in a lot of 'cutting edge' things such as machine learning, natural language processing, computer vision and image recognition.

Data science also uses a lot of Python although that community is also strongly invested in the R language, which is specifically aimed at statistical analysis and data visualisation. 

### Critical mass
So, to make progress faster, we need to group together and 'centralise' our efforts around a single language, or at most a small cluster of languages and frameworks, building and sharing tools that make us all more efficient and productive.

Although I am confident that any clinician of any kind, from any background, can learn to code, the fact remains that at present there aren't *all* that many of us Clinicians Who Code yet.

We need to collectivise our efforts behind a single language so that we focus on developing the ecosystem of tools and libraries of code that we need. If we're spread across many languages then we simply won't hit a 'critical mass', or at least it could take longer.


### Python's ecosystem

Python has a huge ecosystem of mature, reliable tools in its libraries. Libraries are called different things in different languages, but they all do the same essential function - they are reusable units of code that you can use in your programs to make it easier to make progress faster.

Python has a great Web Framework called Django, which is used at full production scale for a number of major websites including [Instagram](https://stackshare.io/instagram/instagram), [Pinterest](https://stackshare.io/pinterest/pinterest) and [Udemy](https://stackshare.io/udemy/udemy). The traffic going through these sites is probably a million times the entire NHS data throughput. Django will cope fine

### Python has an established worldwide community

### Miscellaneous other reasons...

- Want to use a C program in Python? - no problem, it has several easy ways to wrap a C library in a Python wrapper.

- Want to use Python for Internet Of Things development? -

## Things I don't love so much about Python

(But still learn Python)

### It can seem irritatingly pedantic

Python likes things to be done the right way, and the design of the language is intended to give you 'one good way' of doing things (just like the ATLS course!). Occasionally this can make it seem like Python is being annoyingly pedantic, as in this example:

``` python hl_lines="6"
╰─$ python
Python 3.8.0 (default, Aug 23 2020, 17:45:09)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit
Use exit() or Ctrl-D (i.e. EOF) to exit
>>>
```

I typed `exit` - Python clearly understood what I intended to do, because it gave me advice on **how** to successfully exit. But it wants me to do it the right way, so it's going to deliberately **not** exit and wait patiently for me to do it _properly_.

### Python syntax isn't as beautiful as my dear Ruby

This is a minor complaint, since Ruby is fairly close in style to Python. But in Python, things like method chaining look ugly:

``` python
len("My_Text".upper().split('_')[1].encode())
```

Notice all the empty parentheses `()`? And the fact that sometimes you use dot notation to chain the operations, and other times you enclose the expression with a function call `len()`

Same thing in Ruby:

``` ruby
"My_Text".upcase.split('_')[1].encode.length
```

Just cleaner and neater.

But despite this, I've had to get over myself, suck it up, and stick to Python for any projects that other people might need to get involved in. So should you.