---
title: "Pre-exercise: Using docker"
teaching: 0
exercises: 0
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
FIXME
## Section 

Here is the link to [trigger tutorial on Github](https://github.com/cms-legacydata-analyses/TriggerInfoTool)

References to callout sections [here](https://carpentries.github.io/lesson-example/04-formatting/index.html).

Built on [Open Data Portal introduction to docker](http://opendata.cern.ch/docs/cms-guide-docker).


~~~
for thing in collection:
    do_something
~~~
{: .language-python}

The first time you run, you want to fetch the docker image.
~~~
docker run --name opendata -it cmsopendata/cmssw_5_3_32 /bin/bash
~~~
{: .language-bash}

After that you can run it this way to open it. 
~~~
docker run -it --net=host --env="DISPLAY" --volume="$HOME/.Xauthority:/root/.Xauthority:rw" cmsopendata/cmssw_5_3_32 /bin/bash
~~~
{: .language-bash}

More stuff
~~~
docker ps -a
docker start 8d1c5b30745c
docker attach 8d1c5b30745c
~~~
{: .language-bash}


> ## Challenge Title
>
> text
> text
> text
>
{: .challenge}

## Section next

Here is some more text.

> ## Further reading
>
> * text
> * text
> * text
>
{: .checklist}

{% include links.md %}

