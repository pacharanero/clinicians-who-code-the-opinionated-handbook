# What Language Should I Learn?

!!! success ""
    **Answer: *Learn Python***

One of the first problems that you hit when learning to code is the question of which language to learn.

I'm going to end that 'options paralysis' for you right now by advising, no - _asking_ - you to learn Python. Why 'asking'? - because I believe that as Clinicians Who Code we have to band together and collectivise around a language that we can all use, and more importantly, we need to build tools that solve problems and then **share** those tools widely and openly in standard ways like using the [PyPi](https://pypi.org/), the Python Package Index.

If that's enough for you, then you can skip right on to learning how to Python!
You will learn other tools later. But start with Python.

But if you need some more in-depth reasoning for why to learn Python, then read on.

## Why it matters to get on and learn Python **now**, and then learn other stuff later

When I started wanting to code, I asked some friends what would be a good language to learn. I got a variety of answers, but it took me some time to make decent conclusions about whether they were the right things to learn. In short, I wasted quite a bit of time learning languages that were either terrible (Java) or the wrong thing (C) for my needs. So you can skip all that and cut to the chase. *Learn Python*.

One person said "Learn Java because it's 'Enterprise-y' and healthcare applications sound like they are Enterprise-y". Another advised me to start with the basics and learn C or C++ so that I could write super-fast programs. I actually bought books on both of these and really didn't hit it off with either. I then tried Python and subsequently Ruby, and I immediately found them more friendly and straightforward. I've also played around with newer, languages like Elixir and Golang, as well as PHP, Javascript, and Rust. But if you want my advice, *Learn Python*.

This is a roundabout way of saying that none of the languages you could choose are 'right' or 'wrong'. Many of the available alternative languages are absolutely **excellent** languages. That's in fact what makes it so hard to decide. And you can easily plough a lot of your time into the learning curves of a variety of different languages, tyrying to decide what is right for you, when you could be making useful things for healthcare if you just *Learn Python*.

I also believe there is a critical mass effect thing here as well. By concentrating the resources of the Clinicians Who Code community around Python, we can make more progress than if we spread ourselves across numerous languages, tools and frameworks.

## Why the choice of language matters less than you think, **once you get going**

If we are designing our clinical digital tools right, then actually we should be building them so that the inputs and outputs are **language agnostic**, in other words, that the language used to process the data doesn't matter to the user. So, since the choice of language isn't all that important, it's even more reason not to faff about deciding, and just get on and *Learn Python*.

!!! example

     If I build a clinical calculator program, I could make it so that the data going in is in a language-agnostic format such as JSON, and the data coming out is also language-agnostic too:

     ``` bash
     # the input data is in JSON in the { } bit
     # we pass it to our program 'creatinine-ckd-epi' using the 'pipe': |

     $ echo "{'sex': 'male', 'serum_creatinine': 50, 'age': 80, 'race': 'non-black'}" | ./creatinine-ckd-epi

     # result - the output data is also in JSON format, in the { } bit
     {'value': 97, 'units': 'ml/min/1.73m2'}
     ```

     This is an over-simplifed example, but it is here just to explain that we can make our programs in such a way that it doesn't matter what language we wrote them in. We can this and other methods like REST APIs to wrap our code so that it can be called from programs written in any language.

## Why choosing a single language across a community *does* matter

If every clinician set off on their own independent learning journey and chose a language almost at random, then sure, we'd have a lot of Clinicians Who Code, but the opportunities for collaboration are greatly reduced. If we choose to stick together then we can all help out on each others' code.

We can also share libraries of code, all in Python, that help each other to do things that are currently rather hard to do. Healthcare tech is a long way behind the rest of the tech world in terms of the reusable, shared libraries of code that make things easier in our 'domain of expertise'. There are huge numbers of good quality libraries available for statistics, cryptography, and so much else, but comparatively little that would help us in medicine.


!!! example "Fictional Libraries..."

     As a quick example, wouldn't it be great if there were already libraries to calculate some of the parameters we use in everyday care? It would! -  unfortunately they *just don't exist yet*. I want to be able to do something like:

     ``` python
     $ python                 # start the python interpreter
     >>> import snomedct      # import some fictional libraries
     >>> import ckdepi

     # calculate an eGFR from Serum Creatinine using a standard algorithm
     >>> egfr = ckdepi.Creatinine(sex: 'male', serum_creatinine: 50, age: 80, race: 'non-black'); print(egfr)
     {'value': 97, 'units': 'ml/min/1.73m2'}

     # work out the CKD stage from the eGFR
     >>> ckd_stage = ckdepi.Staging(creatinine_clearance['value']); print(ckd_stage)
     {'value': 'CKD stage I'}

     # Get the appropriate SNOMED-CT term
     >>> sct = snomedct.search(ckd_stage['value']); print(sct)
     {'sct_id': '431855005', 'text': 'Chronic kidney disease stage 1 (disorder)'}

     # Print a report!
     >>> print(f"Kidney Report: \nStatus: {sct['text']} \nStore as SNOMED-CT: {sct['sct_id']}\neGFR value: {egfr['value']} {egfr['units']}")
     Kidney Report: 
     Status: Chronic kidney disease stage 1 (disorder) 
     Store as SNOMED-CT: 431855005
     eGFR value: 97 ml/min/1.73m2
     ```

If dozens or hundreds of Clinicians Who Code built just **one** library each, that solves a personal programming need, and publish these libraries in open source so we can all review and improve them, we would soon build an *international, community-curated collection of safe, independently-clinically-validated libraries* that would make the above example possible, turning it from a quite hard problem to solve (which it is currently, it's several day's work at least) to something you could happily do in 5 minutes.

That's what I mean by building a **critical mass** behind Python as a clinical programming language.

## You don't need to optimise for scale or processing speed too early

Programmer time is by far the most expensive commodity in the technology world. CPU cycles are cheap. The most common reason for an application idea to fail is not that it was too slow to scale. It's actually that it never got built in the first place. That's where most ideas die. In development.

> Ideas are worthless; execution on ideas is everything.

So, choose a language that lets you build things quickly, right **now**. Efficient syntax, easy to learn, developer friendly, and has rich libraries. A big developer community so you can ask questions on [StackOverflow](https://en.wikipedia.org/wiki/Stack_Overflow) and get sensible answers. A mature language so you know it will be around for a while. Good, enterprise-grade web frameworks. Y'know. Python, basically.

Another reason not to worry preematurely about scale is that the scale of the NHS is *tiny* in comparison to the 'real tech world' of WhatsApp and Facebook. Even if you had every NHS staff member simultaneously logged into your app, this is about 1.5 million people. WhatsApp can get [2 million concurrent connections out of **one server**](https://blog.whatsapp.com/1-million-is-so-2011/?lang=en), but by the time you need to optimise your app for this kind of performance you'll have a large team to help you!

Scaling too early introduces a lot of complexity to your setup and deployment. Build so that future scaling is possible (with cloud deployments this is very easy anyway) but don't build using a fashionable new language for speed and performance if it is going to make initial development much slower.


-----

!!! Fix those little snags
    I remember hearing on a podcast about coding that you should just tweak just one little thing in your programming workflow *every day*.
    
    This could be by simply adding a useful plugin to your editor, a helpful accessory to your desktop, finding a physically better place to work. But each thing you fix makes you more efficient and better focused.
    
    See [Accessories](../intermediate/accessories.md) for some of my tips in this area.