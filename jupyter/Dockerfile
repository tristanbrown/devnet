# Start from Jupyterlab scipy. 
# View here:
# https://github.com/jupyter/docker-stacks/blob/master/scipy-notebook/Dockerfile

ARG BASE_CONTAINER=jupyter/scipy-notebook
FROM $BASE_CONTAINER

# USER root
USER $NB_UID

# Prepare the global environment
RUN pip install --upgrade pip wheel && \
    pip install ipykernel && \
    mkdir /home/$NB_USER/venv && \
    fix-permissions /home/$NB_USER
WORKDIR /home/$NB_USER/venv

# Create the venvs
COPY requirements requirements
ARG ENV_NAME=data
RUN python -m venv $ENV_NAME && \
    . $ENV_NAME/bin/activate && \
    python -m ipykernel install --name=$ENV_NAME && \
    pip install -r requirements/$ENV_NAME.txt && \
    deactivate
ARG ENV_NAME=invest
RUN python -m venv $ENV_NAME && \
    . $ENV_NAME/bin/activate && \
    python -m ipykernel install --name=$ENV_NAME && \
    pip install -r requirements/$ENV_NAME.txt && \
    deactivate

# Restore standard environment
USER $NB_UID
WORKDIR $HOME
