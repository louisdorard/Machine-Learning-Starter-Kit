FROM jupyter/base-notebook
# see https://github.com/jupyter/docker-stacks/blob/master/base-notebook/Dockerfile

USER root

RUN REPO=http://cdn-fastly.deb.debian.org \
 && echo "deb $REPO/debian jessie main" > /etc/apt/sources.list \
 && echo "deb $REPO/debian-security jessie/updates main" >> /etc/apt/sources.list \
 && apt-get update && apt-get -yq dist-upgrade \
 && apt-get install -yq \
    gcc \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN pip install bash_kernel
RUN python -m bash_kernel.install

USER $NB_USER

ADD oml.yml /home/$NB_USER/
RUN conda env create --name oml --file /home/$NB_USER/oml.yml
RUN python -m ipykernel install --user --name oml --display-name "Python (oml)"
