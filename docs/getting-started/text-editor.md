# Which text editor?

Another source of needless options paralysis, is "Which text editor shall I use for my code?".

There are many available (hundreds, at least), and they cater for all sorts of needs 

## Use VSCode

Microsoft VSCode is a really nice, stable and feature-packed editor which has come from 'nowhere' to being one of the most commonly used text editors,in just a couple of years. It is simple enough to be 'simple' for the people that like simple. But it can be extended using extenstions to have lots of helpful features, which make it more like an 'Integrated Development Environment'. It has lots of extensions which make it easy to handle Git and GitHub repositories, many different coding practices and styles, and even things like Docker containers.

It's free and open source. I strongly recommend it. In the end you may settle on something different, but VSCode will get you through anything in this book.

Download here <https://code.visualstudio.com/download>

### Suggested VSCode plugins

You don't need to install **all** of these at the start, perhaps install the first few and then install the others as and when you start to be using that particular tool or technology.

* Python
* Git 
* Github
* Prettier
* LiveShare
* Docker
* Markdown All In One
* Markdown Preview GitHub Styling
* YAML

You can experiment with many different visual themes for the overall VSCode UI and the syntax highlight colours used. I use Solarized Dark pretty much everywhere I can. Search the Extensions for `theme`.

## Learn `nano` for when there is no GUI

Sometimes you will need to edit a configuration file on a remote server using a text-only login such as [SSH](). You will not be able to use a sophisticated text editor because there is only a text interface. There is almost always a text-based editor available, except in the most minimal of installations. I tend to use the `nano` text editor (even though many people are derisory about it). It works for me. It doesn't really matter, you are not going to be using it for writing acres of code, just small edits to config files.

To edit a file

``` bash
nano <FILENAME>
```

* If the file doesn't exist it will be created

* Navigate up and down using the arrow keys. Normal typing works as you would expect, and you can use ++delete++ to delete, again no surprises here.

* To delete a whole line, you can use ++ctrl+k++, this is a handy trick

* To save, press ++ctrl+o++

* To exit, press ++ctrl+x++

* If you can't make it save, this could be because the file is protected and you need `sudo` permissions. Running `nano` like this will usually fix it.

``` bash
sudo nano <FILENAME>
```

see chapters on server management for more information on Linux and `sudo`

!!! tip "Tip - You don't need to invent anything - transplant ideas from elsewhere... in both directions!"
    Look at how the 'real' industry (ie outside of healthcare) solves generic problems, and bring those solutions into healthcare technology. That's all I'm doing most of the time. Examples are things like open 'RFC' standards and version control, automation, and open source.
    
    However, also note the places where healthcare culture has got it **right**, and the tech industry should be learning from **us**! An example of this is the 'precautionary principle' - _proving_ something is safe before using it widely. This is how we do Evidence Based Medicine, and sadly is not widely practiced in the majority of the tech industry, where 'move fast and break stuff' is a sad adage (attr: Facebook)
