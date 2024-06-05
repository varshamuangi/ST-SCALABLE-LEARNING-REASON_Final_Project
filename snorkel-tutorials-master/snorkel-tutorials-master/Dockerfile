FROM python:3.8-slim-buster

RUN apt-get update && apt-get install -y \
    apt-utils \
    build-essential \
    git \
    wget \
    curl \
    unzip

WORKDIR /app

# First, ensure you copy everything you need
COPY . /app

# Declaring the ARGument for the tutorial
ARG TUTORIAL

# Download the Snorkel requirements
RUN wget -O snorkel-requirements.txt \
    https://raw.githubusercontent.com/snorkel-team/snorkel/master/requirements.txt

# Install requirements from Snorkel
RUN pip install -r snorkel-requirements.txt

# Check if the directory contains the requirements files
RUN ls -alh

# Install other requirements if they exist
RUN if [ -f "$TUTORIAL/requirements.txt" ]; then pip install -r $TUTORIAL/requirements.txt; fi
RUN if [ -f "requirements.txt" ]; then pip install -r requirements.txt; fi

# Download the spaCy model
RUN python -m spacy download en_core_web_sm

WORKDIR $TUTORIAL

ENTRYPOINT ["jupyter", "notebook", "--ip=0.0.0.0", "--no-browser", "--allow-root"]
