---
title: "Pre-exercise: Using docker"
teaching: Self-guided
exercises: ??? min
questions:
- "How do I use docker to effectively interface with the CMS open data?"
objectives:
- "Download (fetch) the correct docker image (IS THIS THE RIGHT NOMENCLATURE?)"
- "Fire up docker in the most useful way"
- "Use docker in a persistent way"
- "Copy data out of the docker environment"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"

---

## Overview

This exercise will walk you through setting up and familiarizing yourself with Docker, so that
you can effectively use it to interface with the CMS open data. It is *not* meant to completely 
cover containers and everything you can do with Docker, but reach out to the organizers
if we are missing something. 


## Install Docker

There are many resources on the web to help you install Docker. You can start
with [the official Docker site](https://docs.docker.com/get-docker/) or whatever you find
that works for you. 


## Using the proper image for CMS software

The first time you go to run Docker, the following command will fetch the docker image and 
put you into a ```bash``` shell in which you have access to a complete CMS software release that
is appropriate for interfacing with the 2011 and 2012 7 and 8 TeV datasets. It may take some time to 
download the full image.

This command and some extra guidance can also be found on the 
[Open Data Portal introduction to Docker](http://opendata.cern.ch/docs/cms-guide-docker), however
the following command differs in that *it allows for X11 forwarding*. That means that if you 
run a program from within Docker that pops up any windows or graphics, like ROOT, they will show up. 

~~~
docker run -it --net=host --env="DISPLAY" --volume="$HOME/.Xauthority:/root/.Xauthority:rw" cmsopendata/cmssw_5_3_32 /bin/bash
~~~
{: .language-bash}

When you're done, you can just type ```exit``` to leave the Docker environment. 

## Using Docker repeatedly

The next time you want to run Docker, it will not need to download any significant data 
so it should open in seconds. You could choose to run the same command as before and while that would
work and quickly put you into a Docker environment, 
there are some issues with this. Most significantly, any files that you make or any code that you write in that
environment will not be there! Instead of the above command, we want to run Docker in a *persistent* way so that
we keep going into the same working area with all our files and code saved each time. 

To do this, we will need to ```start``` and then ```attach``` to the exact same Docker instance as before. 
First of all, we want to see what other Docker processes we have running. To do this, run the following
command
~~~
docker ps -a
~~~
{: .language-bash}

You'll see a list of docker processes that may look something like the following (the exact output
        will vary from user to user).

~~~
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS                      PORTS               NAMES
4f323c317b90        hello-world                "/hello"                 3 minutes ago       Exited (0) 3 minutes ago                        modest_jang
7719a7d74190        cmsopendata/cmssw_5_3_32   "/opt/cms/entrypoint…"   9 minutes ago       Exited (0) 2 minutes ago                        happy_greider
8939ade0bfac        cmsopendata/cmssw_5_3_32   "/opt/cms/entrypoint…"   16 hours ago        Exited (128) 16 hours ago                       hungry_bhaskara
e914cef3c45a        cmsopendata/cmssw_5_3_32   "/opt/cms/entrypoint…"   6 days ago          Exited (1) 9 minutes ago                        beautiful_tereshkova
b3a888c059f7        cmsopendata/cmssw_5_3_32   "/opt/cms/entrypoint…"   13 days ago         Exited (0) 13 days ago                          affectionate_ardinghelli
~~~
{: .language-bash}

You'll want to attach using the ```CONTAINER ID```. In the above example, I know that I've been using the most 
recent container instance for cmsopendata, ```7719a7d74190```. So to reattach, I do

~~~
docker start 7719a7d74190
docker attach 7719a7d74190
~~~
{: .language-bash}

Voila! You should be back in the same container. 


> ## Test X11 forwarding
>
> Go into the Docker environment and open ROOT, simply by typing ```root``` on the command line. 
> Do you see the ROOT splash screen pop up? 
> If not, check that you followed all the instructions
> above correctly or contact the facilitators. 
>
> To exit the ROOT interpreter type ```.q```.
{: .challenge}

> ## Test persistence
>
> Go into the Docker environment and create a test file with your favoite editor.
> (Matt Bellis: mine is vi!) Just add some random text to the file. 
>
> After you've done this, exit out of the container and try to attach to the same
> instance. If you did it correctly, you should be able to list the contents
> of the directory with ```ls -l``` and see your file from before!
> If not, check that you followed all the instructions
> above correctly or contact the facilitators. 
{: .challenge}

## Checkout a git repository and run a small analysis snippet

TO DO!

> ## Further reading
>
> * text
> * text
> * text
>
{: .checklist}

{% include links.md %}

