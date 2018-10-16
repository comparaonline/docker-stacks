FROM jupyter/scipy-notebook

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends ssh-client && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Switch back to jovyan to avoid accidental container runs as root
USER $NB_UID

RUN conda install --quiet --yes \
    -c conda-forge ipywidgets jupyter_contrib_nbextensions

