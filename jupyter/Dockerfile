# Start from Jupyterlab scipy. 
# View here:
# https://github.com/jupyter/docker-stacks/blob/master/scipy-notebook/Dockerfile

ARG BASE_CONTAINER=jupyter/minimal-notebook
FROM $BASE_CONTAINER

USER root

RUN apt-get update && apt-get install -yq --no-install-recommends \
    vim libpq-dev openssh-client

USER $NB_UID

RUN mkdir /home/$NB_USER/venv && \
    fix-permissions /home/$NB_USER
WORKDIR /home/$NB_USER/venv

# Create the venvs first
ARG ENV_NAME=data
RUN python -m venv $ENV_NAME && \
    . $ENV_NAME/bin/activate && \
    pip install --upgrade pip wheel && \
    pip install ipykernel && \
    python -m ipykernel install --user --name=$ENV_NAME && \
    deactivate
ARG ENV_NAME=invest
RUN python -m venv $ENV_NAME && \
    . $ENV_NAME/bin/activate && \
    pip install --upgrade pip wheel && \
    pip install ipykernel && \
    python -m ipykernel install --user --name=$ENV_NAME && \
    deactivate

# Install the venv packages
COPY requirements requirements
ARG ENV_NAME=data
RUN . $ENV_NAME/bin/activate && \
    pip install -r requirements/$ENV_NAME.txt --no-cache-dir && \
    deactivate
ARG ENV_NAME=invest
RUN . $ENV_NAME/bin/activate && \
    pip install -r requirements/$ENV_NAME.txt --no-cache-dir && \
    deactivate

# Restore standard environment
USER $NB_UID
WORKDIR $HOME
