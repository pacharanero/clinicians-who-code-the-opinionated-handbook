# Q: What Language Should I Learn?

!!! success ""
     **A: PYTHON!**

One of the first problems that you hit when learning to code is the question of which language to learn.

I'm going to end that 'options paralysis' for you right now by advising, no - _asking_ - you to learn Python. Why 'asking'? - because I believe that as Clinicians Who Code we have to band together and collectivise around a language that we can all use, and more importantly, we need to build tools that solve problems and then **share** those tools widely and openly in standard ways like using the [PyPi](https://pypi.org/), the Python Package Index.

If that's enough for you, then you can skip right on to learning how to Python!

But if you need some more in-depth reasoning for why to learn Python, then read on.

## Why it matters to get on and learn Python **now**, and then learn other stuff later

When I started wanting to code, I asked some friends what would be a good language to learn. I got a variety of answers, but it took me some time to make decent conclusions about whether they were the right things to learn.

One person said "Learn Java because it's 'Enterprisey' and healthcare applications sound like they are Enterprisey". Another advised me to start with the basics and learn C or C++ so that I could write super-fast programs

## Reasons Python is a good language to learn first

### Ease of learning and use

- Python is taught in schools across the world, to children from around the age of 8 upwards. It's readable enough to make sense even if you don't actually code yet.

- As an interpreted (not compiled) language, the 'type-it-try-it-fix-it-try-it' cycle is that much shorter.

- It's supported by basically all the major deployment platforms such as Heroku,

### It doesn't require a ton of 'boilerplate' to get started

Some languages need a lot of 'boilerplate' (apparently meaningless extra text) in order to even run a basic program. Java is a good example of this, you need a bunch of really quite weird stuff to be there before you can even print "Hello, world":

``` java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

The equivalent in Python:

``` python
print("Hello, world)
```

### It's the de-facto language of many existing communities

Python is widely used for all the 'standard' and common things that we use code for - scripting, small simple programs, desktop programs with a graphical user interface, and web programming.

In addition, it's been adopted as the primary language of the scientific community, for used ranging from astrophysics to bioinformatics. Python's scientific and statistical libraries are mature and well used, and

### We CWCs need to 'standardise' around one language for maximum progress

Although I am confident that any clincian of any kind, from any background, can learn to code, the fact remains that at present there aren't all that many of us Clinicians Who Code yet. So we need to group together and

### Python has a huge ecosystem of mature, reliable tools

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

### Web Framework

- Django
- Flask
