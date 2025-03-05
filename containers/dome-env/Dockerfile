FROM nvidia/cuda:11.1.1-cudnn8-devel-ubuntu20.04
#FROM nvidia/cuda:12.2.0-devel-ubuntu22.04

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8


RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        git \
        wget \
        cmake \
        ninja-build \
        build-essential \
		checkinstall \
		software-properties-common \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 

	
RUN add-apt-repository ppa:deadsnakes/ppa

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
		python3-distutils \
        python3-dev \
        python3-pip \
        python3-venv \
		python-is-python3 \
		libstdc++6 \
		gcc-multilib\
		libc6 \
		 && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* 
	

RUN python3 -m pip install --upgrade pip \
    && python3 -m venv /opt/python3/venv/base
	


COPY requirements.txt /opt/python3/venv/base/


#RUN /opt/python3/venv/base/bin/python3 -m pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
RUN /opt/python3/venv/base/bin/python3 -m pip install --no-cache-dir -r /opt/python3/venv/base/requirements.txt


COPY DOME-master .




COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Set entrypoint to bash
ENTRYPOINT ["/entrypoint.sh"]