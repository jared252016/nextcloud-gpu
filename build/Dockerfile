FROM nextcloud:31-fpm

WORKDIR /srv

RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y wget python3 python3-pip

WORKDIR /srv

# Install CUDA & ffmpeg

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
RUN dpkg -i cuda-keyring_1.1-1_all.deb
RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install cuda-toolkit-12-4 libcudnn8 ffmpeg

# Link cuda 12 library to 11 library paths

RUN ln -s /usr/local/cuda/lib64/libcudart.so.12 /usr/local/cuda/lib64/libcudart.so.11.0

RUN ln -s /usr/local/cuda/lib64/libcublas.so.12 /usr/local/cuda/lib64/libcublas.so.11

RUN ln -s /usr/local/cuda/lib64/libcublasLt.so.12 /usr/local/cuda/lib64/libcublasLt.so.11

RUN ln -s /usr/local/cuda/lib64/libcufft.so.11 /usr/local/cuda/lib64/libcufft.so.10

RUN ln -s /usr/local/cuda/lib64/libcusparse.so.12 /usr/local/cuda/lib64/libcusparse.so.11

# Add to path and ld_library_path

ENV LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"
RUN echo "export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH" > /etc/environment

ENV PATH="/usr/local/cuda/lib64:/usr/local/cuda/bin:$PATH"
RUN echo "export PATH=/usr/local/cuda/lib64:/usr/local/cuda/bin:$PATH" > /etc/environment

#RUN ln -s /usr/local/cuda/lib64/libcudnn.so.8 /usr/local/cuda/lib64/libcudnn.so.8

# Cleanup apt cache

RUN rm -rf /var/lib/apt/lists/*

# Install tensorflow[and-cuda]

RUN python3 -m pip install tensorflow[and-cuda] --break-system-packages

WORKDIR /srv

# Install git & fail2ban

#RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

#RUN git clone https://github.com/fail2ban/fail2ban.git

#WORKDIR /srv/fail2ban

#RUN python3 setup.py install

#RUN cp files/debian-initd /etc/init.d/fail2ban

#RUN update-rc.d fail2ban defaults

#RUN service fail2ban start


