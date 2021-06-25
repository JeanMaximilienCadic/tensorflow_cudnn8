```dockerfile
FROM nvidia/cuda:11.0.3-cudnn8-runtime-ubuntu18.04
ENV DEBIAN_FRONTEND=noninteractive

# Install python
RUN apt update -y
RUN apt install wget -y
RUN apt install python3.8 python3.8-distutils -y

#Create links
RUN ln -s /usr/bin/python3.8 /usr/bin/python

# Install pip3
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN rm get-pip.py
RUN ln -s /usr/bin/pip3 /usr/bin/pip

#Install deps
RUN apt install libgl1-mesa-dev \
                libglib2.0-0 \
                libsm6 \
                libxrender1 \
                libxext6 -y

#Install requirements
RUN pip install tensorflow-gpu=2.4

#Check the gpu
CMD ["python", "-c", "import tensorflow as tf;print(tf.config.list_physical_devices())"]
```

