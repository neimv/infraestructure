FROM jupyter/all-spark-notebook

COPY --chown=${NB_UID}:${NB_GID} requirements.txt /tmp/

RUN pip install --requirement /tmp/requirements.txt --no-cache-dir -q && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

