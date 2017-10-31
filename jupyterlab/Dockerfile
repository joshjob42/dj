FROM joshjob42/julia
RUN pip install jupyterlab  && jupyter serverextension enable --py jupyterlab --sys-prefix
RUN julia -e "Pkg.add(\"IJulia\");Pkg.build(\"IJulia\");using IJulia"
ENV CONDA_DIR /opt/conda
ENV JULIA_LOAD_PATH="/root/.julia/v0.6"
RUN     mv $HOME/.local/share/jupyter/kernels/julia* $CONDA_DIR/share/jupyter/kernels/ && \
    chmod -R go+rx $CONDA_DIR/share/jupyter && \
    rm -rf $HOME/.local
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq xorg
COPY ./keyboard /etc/default/keyboard
RUN apt-get install bash-completion
RUN cd /
ADD mykey.key /mykey.key
ADD mycert.pem /mycert.pem
CMD jupyter lab --ip=* --port=8888 --no-browser --allow-root --certfile=/mycert.pem --keyfile=/mykey.key
