## Why Python?

Why is Python a good language to learn first?

### Ease of learning and use

Python is taught in schools across the world, to children from around the age of 8 upwards. It's readable enough to make sense even if you don't actually code yet.

As an *interpreted* (as opposed to *compiled*) language, the 'type-it-*try-it*-fix-it-*try-it*' cycle is that much shorter.

It's supported in 'serverless' deployment features by basically all the major platforms such as Heroku, Microsoft Azure, Amazon Web Services, so it's quite easy to deploy experiments and demos.

You can use it in Jupyter Notebook form


### Python's the de-facto science language

Python is widely used for all the 'standard' and common things that we use code for - scripting, small simple programs, desktop programs with a graphical user interface, and web programming.

In addition, it's been adopted as the primary language of the scientific community, for uses ranging from astrophysics to bioinformatics. Python's scientific and statistical libraries are mature and well supported.

Python is also used in a lot of 'cutting edge' things such as machine learning, natural language processing, computer vision and image recognition.

Data science also uses a lot of Python although that community is also strongly invested in the R language, which is specifically aimed at statistical analysis and data visualisation.

Medicine is (primarily) a scientific discipline. Yeah, it's an art too, but for the computing side of things, science is the way to go. Let's give scientific tools to the humans who practice the art of medicine. I love the phrase *'Machine Assisted Human'*. It's something I came up with when trying to describe what we were doing with the UI of a new GP system. We're not trying to *replace* the human, we're trying to give the human practitioner 'super-powers'. That's the future of medicine.

### One language, Critical mass

So, to make progress faster, we need to group together and 'centralise' our efforts around a single language, or at most a small cluster of languages and frameworks, building and sharing tools that make us all more efficient and productive.

Although I am confident that any clinician of any kind, from any background, can learn to code, the fact remains that at present there aren't *all* that many of us Clinicians Who Code yet. One day, all clinicians will be able to code. It probably isn't that far away - 10-20 years? So let's start building now the tools that those clinicians will need.

We need to collectivise our efforts behind a single language so that we focus on developing the ecosystem of tools and libraries of code that are needed. If we're spread across many languages then we simply won't hit a 'critical mass', or at least it could take longer to hit it.

### Python's ecosystem

Python has a huge ecosystem of mature, reliable tools in its libraries. Libraries are called different things in different languages, but they all do the same essential function - they are reusable units of code that you can use in your programs to make it easier to make progress faster.

Python has a great Web Framework (a library which makes it easier to build web applications) called Django, which is used at full production scale for a number of major websites including [Instagram](https://stackshare.io/instagram/instagram), [Pinterest](https://stackshare.io/pinterest/pinterest) and [Udemy](https://stackshare.io/udemy/udemy). The daily traffic going through these sites is probably a million times the entire NHS data throughput. Django will cope fine. If you get to the point where parts of your application need to be replatformed to a faster-performing language because of the sheer volume of traffic, then you have a [Champagne Problem](https://www.urbandictionary.com/define.php?term=champagne%20problem). Until then, you'll be fine with these tools. See [Solving Imaginary Scaling Issues At Scale](https://dev.to/ben/solving-imaginary-scaling-issues-at-scale)

### Community

A word you will read a fair bit in this book is 'Community'. You are part of building a community of Clinicians Who Code, but also, we're part of a larger community - of all coders, and also - a community of all clinicians. We're a very special part of the Venn diagram.

I've built up several communities within health tech - the main ones being discourse.digitalhealth.net and openhealthhub.org, and there are a few others. Community is hugely important. It gives the members a place to talk, to learn, understand, discuss, and disagree. We can use a community to explore the [Zone Of Uncomfortable Debate](https://www.digitalhealth.net/2017/05/joes-view-leadership-cultural-revolution-health-informatics/).

Communities make us more productive, simply because we can learn from each other. It's a right that you have, in any good community, to ask for help, and you should get it. Similarly, as you start to accrue knowledge in the community, it's a responsibility of yours now to share your knowledge with the other members. 

### Miscellaneous other reasons...

- Want to use a C program in Python? - no problem, it has several easy ways to wrap a C library in a Python wrapper.

- Want to use Python for Internet Of Things development? - you can use Python for that: https://micropython.org/



## Things I don't love so much about Python

(But still learn Python please...)

### Pedantry and pedanticism

Python likes things to be done the right way, and the design of the language is intended to give you 'one good way' of doing things (just like the ATLS course). Occasionally this can make it seem like Python is being annoyingly pedantic, as seen in this commonly encountered example:

``` python hl_lines="6"
╰─$ python
Python 3.8.0 (default, Aug 23 2020, 17:45:09)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit
Use exit() or Ctrl-D (i.e. EOF) to exit
>>>
```

I typed `exit` - Python clearly understood what I intended to do, because it gave me advice on **how** to successfully exit. But it wants me to do it the right way, so it's going to deliberately **not** exit and wait superciliously for me to do it _properly_. 

### It's no Ruby

This is a minor complaint, since Ruby is fairly close in style to Python. But in Python, things like method chaining look ugly:

``` python
len("My_Text".upper().split('_')[1].encode())
```

Notice all the empty parentheses `()`? And the fact that sometimes you use dot notation to chain the operations, and other times you enclose the expression with a function call `len()`. There's probably some logic in there somewhere, but certainly no elegance.

Same thing in Ruby:

``` ruby
"My_Text".upcase.split('_')[1].encode.length
```

Just cleaner and neater. Elegant and well thought through.

But despite this, I've had to get over myself, suck it up, and stick to Python for any projects that other people might need to get involved in. So should you.