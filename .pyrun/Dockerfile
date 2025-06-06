# Python 3.6
#FROM python:3.6-slim-buster

# Python 3.7
#FROM python:3.7-slim-buster

# Python 3.8
FROM public.ecr.aws/docker/library/python:3.8-slim-buster

# Python 3.9
#FROM python:3.9-slim-buster

# Python 3.10
#FROM python:3.10-slim-buster

RUN apt-get update \
    # Install aws-lambda-cpp build dependencies
    && apt-get install -y \
      g++ \
      make \
      cmake \
      unzip \
      git \
    # cleanup package lists, they are not used anymore in this image
    && rm -rf /var/lib/apt/lists/* \
    && apt-cache search linux-headers-generic

ARG FUNCTION_DIR="/function"

# Copy function code
RUN mkdir -p ${FUNCTION_DIR}

ARG LITHOPS

# Update pip
RUN pip install --upgrade --ignore-installed pip wheel six setuptools \
    && pip install --upgrade --no-cache-dir --ignore-installed \
        pandas \
        pyarrow \
        scipy \
        pyImagingMSpec \
        cpyImagingMSpec \
        pyMSpec \
        cpyMSpec==0.3.5 \
        pyimzML \
        requests \
        msgpack \
        msgpack-numpy \
        pypng \
        awslambdaric \
        boto3 \
        redis \
        httplib2 \
        requests \
        numpy \
        pika \
        kafka-python \
        cloudpickle \
        ps-mem \
        tblib \
        matplotlib \
        ipykernel \
        ipywidgets \
        tenacity \
        "$LITHOPS" \
        gql[aiohttp]

ENV PYTHONUNBUFFERED TRUE

# Set working directory to function root directory
WORKDIR ${FUNCTION_DIR}

