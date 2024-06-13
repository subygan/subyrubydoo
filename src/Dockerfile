FROM python:3.8-alpine

# install pipenv, gcc, devel

# Download the static build of Litestream directly into the path & make it executable.
# This is done in the builder and copied as the chmod doubles the size.
ADD https://github.com/benbjohnson/litestream/releases/download/v0.3.8/litestream-v0.3.8-linux-amd64-static.tar.gz /tmp/litestream.tar.gz
RUN tar -C /usr/local/bin -xzf /tmp/litestream.tar.gz
RUN ls -la /usr/local/bin


RUN apk add --no-cache --virtual .build-deps \
    gcc \
    musl-dev\
    python3-dev \
    && pip install pipenv


WORKDIR /code/

ADD Pipfile* /code/
RUN pipenv sync
ADD . /code/
# Copy Litestream configuration file & startup script.
COPY etc/litestream.yml /etc/litestream.yml
COPY scripts/run.sh scripts/run.sh
RUN ls -la /code/scripts
RUN pwd
CMD [ "sh","scripts/run.sh" ]
#CMD ["pipenv", "run", "python", "handler.py"]
