FROM ubuntu:16.04

RUN apt-get update -y -m && \
    # adds add-apt-repository command
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y software-properties-common && \
    # ruby ppa
    add-apt-repository -y ppa:brightbox/ruby-ng && \

    apt-get update -y -m && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
                                               wget \
                                               hmmer=3.1b2-2 \
                                               ruby2.6 \
                                               parallel=20161222-1~ubuntu0.16.04.1 && \
    # remove add-apt-repository
    DEBIAN_FRONTEND=noninteractive apt-get remove -y software-properties-common && \
    # clean
    apt-get clean && \
    rm -rf /var/lib/apt/lists/

# install kofamscan
RUN wget https://github.com/takaram/kofam_scan/archive/refs/tags/v1.3.0.tar.gz && \
    tar -xzf v1.3.0.tar.gz && \
    rm v1.3.0.tar.gz && \
    mv kofam_scan-1.3.0 /usr/lib/ && \
    cd /usr/bin && \
    ln -s /usr/lib/kofam_scan-1.3.0/exec_annotation .

# create config file
COPY ./config.yml /usr/lib/kofam_scan-1.3.0/config.yml

# create mounted directories
RUN mkdir /refdata && mkdir /data

ENTRYPOINT ["exec_annotation"]
CMD ["-h"]
