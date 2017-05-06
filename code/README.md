This directory contains Jupyter notebooks (the .ipynb files), which themselves contain Python code. The best way to use these notebooks (and the Python libraries/packages they depend on) is to get a "conda" environment set up.

**Contents:**

* [I. Introduction to notebooks](#intro-notebooks)
* [II. Setting up the conda environment](#setup-conda-environment)
* [III. Accessing notebooks from Jupyter](#access-notebooks-jupyter)
* [Appendix A: How the conda environment and docker image were created](#how)
* [Appendix B: Further reading](#further-reading)
* [Appendix C: Work In Progress](#wip)


<a name="intro-notebooks"></a>
## I. Introduction to notebooks

Notebooks are very popular in the Data Science and Machine Learning communities as they provide great ways to learn and experiment. They are interactive web pages that include blocks of code that you can run and edit. For this to work, they need to be served by a notebook server called Jupyter. For a quick introduction to Jupyter notebooks, check out this video: [https://youtu.be/pwr-pR0tu5Y](https://youtu.be/pwr-pR0tu5Y)

The easiest way to install Python and Jupyter is via [conda](http://conda.io) (I recommend to use Python 2.7 to maximize compatibility with various packages). You can choose from 3 options:

1. Using a docker image that already contains Miniconda
2. Installing Miniconda (command line)
3. Installing Anaconda (graphical interface)

### Remarks

* Options 1 and 2 require some basic command line knowledge (you can learn more about the command line in this free course: [Codeacademy — Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line)).
* If you're not familiar with docker and you're leaning towards option 2 or 3, but aren't sure which one to choose, check out this discussion on [Miniconda vs Anaconda](https://conda.io/docs/download.html#should-i-download-anaconda-or-miniconda).
* Consult the system requirements for your preferred option and make sure you meet them.
* The Python code in the notebooks included here is pretty simple, but if you want to learn Python from scratch or to improve your Python skills, check out the free resources below:
   * [Codeacademy — Learn Python](https://www.codecademy.com/learn/python)
   * [Robert Johansson — Scientific Python Lectures](https://github.com/jrjohansson/scientific-python-lectures) (and in particular "Introduction to Python programming")

<a name="setup-conda-environment"></a>
## II. Setting up the conda environment

Conda environments allow us to make sure we are all working with the same version of Python and Python packages. Follow the indications below to create an environment that will allow you to use my code.

### Option 1: docker

Docker containers act as lightweight virtual machines. Similarly to VMs, they are built from images. The docker image we’ll use is referenced by "louisdorard/oml" (check out the Dockerfile of this repository for more information on how it was built).

Docker is pretty easy to use, but if you're completely new to it, this may not be the best choice for you — unless you run into issues with options 2 & 3.

For a quick introduction to Docker, check out this video: [https://youtu.be/9hzFzcIX10g](https://youtu.be/9hzFzcIX10g)

#### Install docker

Learn more about docker and how to install it on your OS at [https://www.docker.com/](https://www.docker.com/)

#### Run docker container

Launch the following command from the current directory:

```bash
docker run -d -p 8888:8888 -v $PWD:/home/jovyan/work --name oml louisdorard/oml start-notebook.sh --NotebookApp.token=''
```

That's it! Everything's already set up in the docker container. You can jump straight to the section of this document on "Accessing notebooks from Jupyter".

If you're curious, here's some more information on the command line above:

* it creates a docker container called 'oml' -- which you can think of as a lightweight virtual machine -- from an image found on docker hub and referenced by 'louisdorard/oml'
* it maps the current directory in your OS to /home/jovyan/work in the container
* it maps the 8888 port so that when accessing it in your OS, everything gets redirected to the container on the same port
* when the container is created the command `start-notebook.sh --NotebookApp.token=''` is executed inside of it, which starts the Jupyter notebook (the "token" option is to make it easier to connect to that notebook and is not recommended in production settings).

### Option 2: local install via Miniconda and the command line

2.1 On Linux:

```bash
wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh -O /tmp/miniconda.sh
/bin/bash /tmp/miniconda.sh -b -p ~/anaconda/
export PATH="~/anaconda/bin:$PATH"
echo "export PATH=\"\$PATH:~/anaconda/bin\"" >> ~/.bashrc
```

On macOS and Windows, follow these [instructions](https://conda.io/docs/install/quick.html). Choose Python 2.7, and the 64-bit installer if in doubt.

Make sure that `conda` is installed:

```bash
conda --version
```

2.2 Install Jupyter:

```bash
conda install jupyter
```

2.2 Create an environment which contains all the libraries used in the notebooks. The environment configuration file is `oml.yml`. Execute this command from the directory where this file is (i.e. the same where this README file is):

```bash
conda env create --name oml --file oml.yml
```

(Side note: this environment also contains libraries that I use in my _Operational Machine Learning_ workshop, in particular...

- scikit-learn, the most popular open source machine learning library
- skll, a library to compare predictive models easily
- bigmler, a command-line tool for BigML
- xgboost, an efficient multi-threaded implementation of a very powerful predictive modeling technique
- hyperopt, a library to optimize (hyper)parameters used to train predictive models.)

2.2 Make this environment available to Jupyter:

```bash
source activate oml
python -m ipykernel install --user --name oml --display-name "Python (oml)"
```

Launching Jupyter is as simple as:

```bash
jupyter notebook
```

Note: it's best to run this command from the directory where your .ipynb notebook files are.

### Option 3: local install via Anaconda and the GUI

Follow the [instructions](https://conda.io/docs/install/full.html). If asked for a version of Python, choose 2.7.

Once this is done, launch Anaconda Navigator:

* Go to the 'Environments' tab and choose 'Import'; enter 'oml' as the name of the environment and point to `oml.yml`
* Go back to the 'Home' tab and click on the Jupyter icon

<a name="access-notebooks-jupyter"></a>
## III. Accessing notebooks from Jupyter

Launching Jupyter should open a new window in your web browser ([http://localhost:8888](http://localhost:8888))

The home page served by Jupyter lists the contents of the folder from which the server was launched. Make sure that the notebooks you want to open are within that folder (or a sub-folder) so you can navigate to them.

If you're new to Jupyter notebooks, start with opening `Simple intro to Jupyter.ipynb`. You can then try `Machine Learning with BigML API - Interactive Code Tutorial.ipynb` and move on to `AmazonML-Python.ipynb` to see how Amazon ML compares to BigML.

When opening a notebook, make sure that the kernel displayed on the right hand side of the page is "Python (oml)". If Jupyter notifies you that the kernel was not found, choose "Python [conda env:oml]".

<a name="how"></a>
## Appendix A: How the conda environment and docker image were created

### Conda environment

From a [jupyter/base-notebook](https://github.com/jupyter/docker-stacks/blob/master/base-notebook/) docker container, as root:

```bash
apt-get update
apt-get install -yq gcc # required for bigmler later on
```

As user "jovyan":

```bash
conda update conda --yes
conda create --name oml python=2.7 scikit-learn=0.17.1 pandas nltk boto ipykernel matplotlib --yes
source activate oml
conda install --yes -c aterrel xgboost=0.4.0.c4fa2f
pip install bigmler==3.8.7 skll==1.2.1 bash_kernel pymongo indicoio
pip install -i https://pypi.anaconda.org/pypi/simple hyperopt==0.0.2
conda install --yes 'tensorflow=1.0*'
conda install --yes -c conda-forge keras=2.0.2
conda env export -n oml
```

### Docker image

From this directory:

```bash
docker build -t="louisdorard/oml" .
```

Automated builds were also set up on [docker hub](hub.docker.com/r/louisdorard/oml/).

<a name="further-reading"></a>
## Appendix B: Further reading

- [What is the difference between pip and conda?](http://stackoverflow.com/questions/20994716/what-is-the-difference-between-pip-and-conda)
- [Conda: Myths and Misconceptions](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/)
- TODO: docker quickstart

<a name="wip"></a>
## Appendix C: Work In Progress

If you notice anything that needs fixing, please [open an issue](https://github.com/louisdorard/Machine-Learning-Starter-Kit/issues).

TODO test Amazon ML notebook

TODO test Option 2 on Windows
