# Learning Python

There are a plethora of ways to learn Python, both online and offline. Here are a few that I would recommend, but what's available is changing all the time - let me know if you hit problems with something I'm recommending here, or if you know of better resources.

!!! note "Improve this book!"
    If you have found an error, or have something to contribute that would improve the book, you can [email me](mailto:marcusbaw@gmail.com),  create a [GitHub Issue](https://github.com/pacharanero/clinicians-who-code-the-opinionated-handbook/issues), or even submit a [Pull Request](../intermediate/git.md)

1. ## [CodeCademy](https://www.codecademy.com/learn/learn-python)

    This is where I learned Python originally, and still a great course. You learn step-by-step and everything is in a browser so you don't need to be able to install things on the local machine to be able to learn. This is great when you're in clinical work but have a short break and want to do some learning.
    <https://www.codecademy.com/learn/learn-python>

    The Python 2 course is free, and really there is very little difference between Python 2 and 3 at this level, so I'd say you're fine learning Python 2 here.

1. ## [learnpython.org](https://www.learnpython.org/)

    Another great, web based site which steps you through the main things you need to learn to be able to code in Python.
<https://www.learnpython.org/>

1. ## [Python Koans](https://github.com/gregmalcolm/python_koans)

    This project was ported over from Ruby (another language which is quite similar to Python) - and originally I did these Koans in Ruby. I'm not sure if I actually completed them all, though. The nice thing about them is that they run in your terminal, offline, so if you don't have an internet connection you can still do them. I remember doing these on the train to London from Yorkshire, when connections where patchy.
    <https://github.com/gregmalcolm/python_koans>

## My Python tips

### Using `pyenv` for 'virtualenvs' and Python version management

Once you are writing Python programs on your local machine regularly, and especially if you are working with other people's code or on shared projects, you'll inevitably hit a situation where you need to have multiple different versions of a Python package installed on your computer, or different versions of Python itself.

### Use `pyenv`

Although Python has a number of tools available to help manage this problem, I found `pyenv` to be the easiest to use. It allows you to manage Python versions **and** your collections of libraries on a 'per-project' basis very easily.

!!! tip
    At first I remember thinking it was a lot of extra hassle to bother with `pyenv`, especially when you are just starting, but it really does pay dividends later when you find it's really easy to have numerous different python versions and library collections on your machine. You can also solve this problem with Docker containers, but that is a lot more to learn at this stage and I'd recommend to leave those till later.

You can find out how to install and use `pyenv` here: <https://github.com/pyenv/pyenv#readme>
(it's a GitHub README.md, which is often used for this kind of technical documentation).

There's also a quite helpful 'Intro to pyenv' tutorial I found here <https://realpython.com/intro-to-pyenv/>

#### My `pyenv` Tips

use `pyenv local <VIRTUALENV_NAME>` to create a `.python-version` file in the root of projects. That way, when you navigate to the project root, `pyenv` will automatically select your

## I want MOAR Python learning!

FreeCodeCamp's Learn Scientific Computing with Python track is a big course, but wow there's a lot in there. If you do that course you know more Python than I do, for sure.
<https://www.freecodecamp.org/learn/scientific-computing-with-python/>

--8<-- "../basics/glossary.md"
