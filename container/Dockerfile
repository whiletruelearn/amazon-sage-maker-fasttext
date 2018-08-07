
FROM python:2.7.14-stretch

RUN apt-get -y update && apt-get install -y --no-install-recommends \
         wget \
         nginx \
         ca-certificates \
         software-properties-common \
    && rm -rf /var/lib/apt/lists/* \
    && python -v



RUN pip install --upgrade pip \
    && pip install cython==0.25.2 awscli numpy==1.11.2 cysignals nltk \
    && pip install spacy==1.8.2 scipy scikit-learn pandas flask gevent gunicorn   \
    && python -c 'import nltk; nltk.download("stopwords")' \
    && python -c 'import nltk; nltk.download("snowball_data")' \
    && python -c 'import nltk; nltk.download("punkt")' \
    && python -c 'import nltk; nltk.download("wordnet")' \
    && python -m spacy download en


RUN pip install pybind11>=2.2 \
    && git clone https://github.com/facebookresearch/fastText.git \
    && cd fastText && \
    pip install .


ENV PYTHONUNBUFFERED=TRUE
ENV PYTHONDONTWRITEBYTECODE=TRUE
ENV PATH="/opt/program:${PATH}"

# Set up the program in the image
COPY fasttext /opt/program
WORKDIR /opt/program

