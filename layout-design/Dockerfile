# Specify the base Docker image
FROM redhat/ubi9

ARG PYTHON_VER="3.14.0"

# Install required packages & update certificates
RUN dnf update -y && \
    dnf -y install git wget nano openssl-devel bzip2-devel libffi-devel zlib-devel ca-certificates postgresql-devel automake cmake make gcc sqlite-devel python3-devel && \
    dnf clean all

# Download and install the latest Python
RUN wget -Lk "https://www.python.org/ftp/python/$PYTHON_VER/Python-$PYTHON_VER.tgz" -O /tmp/python.tgz
RUN tar -xzvf /tmp/python.tgz
WORKDIR /Python-$PYTHON_VER
RUN sh -c "./configure" && make -j $(nproc) && make install

# Copy the sample plugin to temporary location in the container
COPY ./layout-design/sample-design-engine-plugin/plugins/sample_design_engine/ /opt/sample_design_engine/
# Copy the sample plugin configuration file
COPY ./layout-design/config/config_sample_design_engine.yaml /opt/sample_design_engine/config_sample_design_engine.yaml

# Set the working directory
WORKDIR /layout-design

# Build and install the layout-design package
ARG CACHE_BUST=1
COPY layout-design/layout-design /layout-design/layout-design
RUN echo "Cache busting: $CACHE_BUST" && pip3.14 install /layout-design/layout-design
RUN mkdir -p /var/log/cdim

# Expose the required port
EXPOSE 8000

# set the command to copy the sample plugin to the plugins directory and start the server
CMD ["sh","-c","cp -r /opt/sample_design_engine/ /usr/local/lib/python3.14/site-packages/plugins/ && exec layoutdesign-server"]
