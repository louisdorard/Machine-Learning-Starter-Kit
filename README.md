# Machine Learning Starter Kit

The Machine Learning Starter Kit contains resources for developers and managers to gain practical ML knowledge and to learn how to apply it to their own projects.

There is also an accompanying email course with additional, exclusive and free content to help you get started progressively with ML — [sign up](http://louisdorard.com/machine-learning-starter-kit#form) if you haven’t done so already!

![](https://static1.squarespace.com/static/5206b718e4b0bdc26006bae2/t/5862badcf5e23110755c7c1e/1482865374964/starter-kit.png) 


## Contents of the Kit

* `Bootstrapping Machine Learning 1.0.5 sample.pdf` (Introduction to Machine Learning taken from my [book](http://louisdorard.com/machine-learning-book))
* `When Machine Learning fails.pdf`
* `How to improve your business by predicting churn.pdf` (Practical & code-free tutorial)
* `Machine Learning with BigML API - Interactive Code Tutorial.ipynb` (Jupyter notebook in Python on the basics of BigML — see set up instructions below or use the version hosted on Wakari)
* `Machine Learning with BigML API - Interactive Code Tutorial.html` (Link to the notebook above hosted on Wakari)
* `AmazonML-Python.ipynb`
* `Machine Learning Canvas v0.4.pdf` (blank template to formalize your own ML use case)
* `From Data to AI with the ML Canvas.pdf`: a preliminary guide to using the Canvas


## Datasets

Below is a list of real-world datasets that you can use to experiment with ML. I’m not including the actual datasets in this kit in order to make it smaller in size. You can download the datasets you’re interested in via http (links provided) or you can point to them from BigML or Amazon ML using the S3 paths given between brackets.

* [Real-estate properties in Las Vegas](https://papiseval.s3.amazonaws.com/realtor-las-vegas.csv) (`s3://papiseval/realtor-las-vegas.csv`)
* [Priority Inbox](https://papiseval.s3.amazonaws.com/emails.csv) (`s3://papiseval/emails.csv`)
* [Orange Churn](https://bml-data.s3.amazonaws.com/churn-orange.tsv.zip) (`s3://bml-data/churn-orange.tsv.zip`)


## Running the notebooks

Notebooks are very popular in the Data Science and Machine Learning communities as they provide great ways to learn and experiment. They are interactive web pages that include blocks of code that you can run and edit. For this to work, they need to be served by a notebook server called Jupyter. You can either use your own installation of Jupyter or you can use a 3rd party service such as Wakari (see `Machine Learning with BigML API - Interactive Code Tutorial.html`).

The easiest way to install Python and Jupyter on your own machine is with [Anaconda](https://www.continuum.io/downloads) (I recommend to use Python 2.7). Once you’ve installed Anaconda, you’ll need to install the BigML API wrappers, which you can do from the Anaconda prompt via:

```
 pip install bigml
```

Then, launch the Jupyter server from Anaconda Navigator or from the command line (e.g. `jupyter-notebook` on Mac). This should open a new window in your web browser, with a page served by Jupyter that lists the contents of the folder from which the server was launched. Make sure that the notebooks are within that folder or a sub-folder so you can navigate to them.

The first thing to do upon loading a notebook will be to fill in your API credentials.


## Creating accounts on cloud ML platforms

* Create an account on [BigML](http://www.bigml.com). Usage of the service is free in “dev” mode.
* Create an Amazon Web Services account in order to use [Amazon ML](https://aws.amazon.com/machine-learning/) (AML). Unfortunately there is no free trial, so if you want to use AML you will need to give your credit card details. That being said, usage is very cheap for basic experiments (see pricing: $0.42 per hour plus a few cents for predictions). If you want to use AML, you will need to go through identity verification and to make sure you can list “entities” on the AML dashboard.

I recommend you to write down your access credentials somewhere safe (I use [LastPass](http://lastpass.com)).


### Other services

There are many other services you could be using and which could be better fits for your own needs. I recommend you to have a look at the PAPIs conferences ([past events](http://www.papis.io/past-events) and [videos](http://youtube.com/channel/UCHMa1aYqXIQPnQD34W-ejQg/)) to learn more.


## Continue your journey in Machine Learning

Part of this Kit is based on my book, [Bootstrapping Machine Learning](http://louisdorard.com/machine-learning-book), where you’ll find more details and resources to go further.

Chris Bourguignat (Data Science Lead at global insurance company Axa) said about the book:

> [“I really wish it existed when I first learned machine learning”](https://twitter.com/chris_bour/status/577196664219426816)

Don’t wait up and [get your copy now](http://louisdorard.com/machine-learning-book)!


## Copyright

[Louis Dorard](http://louisdorard.com) © 2017 — All Rights Reserved

Follow me on Twitter [@louisdorard](https://twitter.com/louisdorard) | Contact me [here](http://louisdorard.com/contact)