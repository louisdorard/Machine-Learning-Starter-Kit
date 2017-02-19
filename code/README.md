This directory contains Jupyter notebooks (the .ipynb files), which themselves contain Python code. The best way to use these notebooks (and the Python libraries/packages they depend on) is to get a "conda" environment set up.

## Introduction to notebooks

Notebooks are very popular in the Data Science and Machine Learning communities as they provide great ways to learn and experiment. They are interactive web pages that include blocks of code that you can run and edit. For this to work, they need to be served by a notebook server called Jupyter.

You can either use your own installation of Jupyter or you can use a 3rd party service such as Wakari (see `Machine Learning with BigML API - Interactive Code Tutorial.html`) or Microsoft Azure Notebooks.

The easiest way to install Python and Jupyter is via [conda](http://conda.io) (I recommend to use Python 2.7 to maximize compatibility with various packages). You can choose from 3 options:

1. Using a docker image that already contains Miniconda
2. Installing Miniconda (command line)
3. Installing Anaconda (graphical interface)

Check out this discussion on [Miniconda vs Anaconda](https://conda.io/docs/download.html#should-i-download-anaconda-or-miniconda).

## Setting up the conda environment

Conda environments allow us to make sure we are all working with the same version of Python and Python packages. Follow the indications below to create an environment that will allow you to use my code.

### Option 1: docker

Docker is pretty easy to use, but if you're completely new to it, this may not be the best choice for you — unless you run into issues with options 2 & 3.

#### Install docker

Learn more about docker and how to install it on your OS at [https://www.docker.com/](https://www.docker.com/)

#### Run docker container

From the current directory:

> docker run -d -p 8888:8888 -v $PWD:/home/jovyan/work --name oml louisdorard/oml

That's it! Everything's already set up in the docker container. You can jump straight to the section of this document on "Accessing notebooks from Jupyter".

For more info on the docker image we're using (louisdorard/oml), check out the Dockerfile in this repo.

### Option 2: local install via Miniconda and the command line

2.1 Follow these [instructions](https://conda.io/docs/install/quick.html). If asked for a version of Python, choose 2.7.

2.2 Install Jupyter:

> conda install jupyter

2.2 Create an environment which contains all the libraries used in the notebooks. The environment configuration file is `oml.yml`. Execute this command from the directory where this file is (i.e. the same where this README file is):

> conda env create --name oml --file oml.yml

(Side note: this environment also contains libraries that I use in my _Operational Machine Learning_ workshop, in particular...

- scikit-learn, the most popular open source machine learning library
- skll, a library to compare predictive models easily
- bigmler, a command-line tool for BigML
- xgboost, an efficient multi-threaded implementation of a very powerful predictive modeling technique
- hyperopt, a library to optimize (hyper)parameters used to train predictive models.)

2.2 Make this environment available to Jupyter:

> python -m ipykernel install --user --name oml --display-name "Python (oml)"

Launching Jupyter is as simple as:

> jupyter notebook

Note: it's best to run this command from the directory where your .ipynb notebook files are.

### Option 3: local install via Anaconda and the GUI

Follow the [instructions](https://conda.io/docs/install/full.html). If asked for a version of Python, choose 2.7.

Once this is done, launch Anaconda Navigator:

* Go to the 'Environments' tab and choose 'Import'; enter 'oml' as the name of the environment and point to `oml.yml`
* Go back to the 'Home' tab and click on the Jupyter icon


## Accessing notebooks from Jupyter

Launching Jupyter should open a new window in your web browser ([http://localhost:8888](http://localhost:8888))

The home page served by Jupyter lists the contents of the folder from which the server was launched. Make sure that the notebooks are within that folder or a sub-folder so you can navigate to them.

You may need to enter a "token" in order to access this home page. The token will be given to you when launching the server from the command line, or if you're using docker, you can get it with the following command:

> docker exec --user jovyan oml jupyter notebook list

## Work In Progress

TODO test Option 3

TODO test Option 2 on Windows

TODO test Amazon ML notebook

If you notice anything that needs fixing, please open an issue on this Github repo.