FROM joshjob42/julia-base
COPY sapi-python-client-2.4.2-linux64.tgz /root/sapi-client.tgz
RUN cd /root && tar -xzf sapi-client.tgz && cd sapi-python-client-2.4.2-linux64 && python install.py
RUN apt-get install -y libssl-dev libnss3
RUN echo '#!/bin/bash'>/root/run_julia && echo 'TMP="$(mktemp)" && echo "cd(\"$1\")" > $TMP && julia -L $TMP ${@:2}' >> /root/run_julia && chmod +x /root/run_julia && mv /root/run_julia /opt/julia/usr/bin/run_julia
RUN conda install pip

CMD /bin/bash
