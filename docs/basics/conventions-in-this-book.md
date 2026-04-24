# Conventions used in this book

## Commands and code snippets

Commands that you run by typing into the Command Prompt (Windows), Terminal (MacOS/Linux) or Python console are in monospaced 'typerwriter' font like this

`some code`

``` python
>>> print('this is a command')
```

Where you need to insert your own details into a command I've used angle brackets and capitals so it looks like `<THIS_KIND_OF_THING>`:

``` python
my_secret_api_key = "<INSERT_YOUR_API_KEY_HERE>"
```

Full-size code snippets have a small 'copy' icon in the top right, which will copy the command to your clipboard for easy pasting.

### What is $ and # at the start of a line of code?

`$` is the 'standard-user' command prompt character in Unix/Linux. You type commands after the $, and press ++enter++ to make them run.

`#` is the 'super-user' (`su`) command prompt character in Unix/Linux. It's purely to remind you that you are in super-user mode, and you can cause more damage in this mode! You can get into `su` mode by typing `sudo su`, and you will stay in super-user mode until you type `exit`.

My advice is to use standard (`$`) user mode all the time, and enter super-user only to execute specific commands. You can run a command in `su` mode by typing `sudo` and then the command. You will need to enter your admin password.

For more information on super-user, see [Managing Servers]()

-----

## Tips

!!! tip "Marcus's Random Tips"
    Scattered through the book, formatted in these 'tip' boxes, I've included some tips and advice which I've either learned from opther places during my time in tech, or which I've concluded myself. I've tried to make them interesting and actionable. (I'm sure you'll tell me if they aren't)