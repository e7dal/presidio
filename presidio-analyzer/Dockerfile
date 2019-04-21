ARG REGISTRY=presidio.azurecr.io

FROM ${REGISTRY}/presidio-python-deps

ARG NAME=presidio-analyzer
WORKDIR /usr/bin/${NAME}
ADD ./${NAME} /usr/bin/${NAME}

RUN pipenv run pylint analyzer && \
    pipenv run flake8 analyzer --exclude "*pb2*.py" && \
    pipenv run pytest --log-cli-level=0

#----------------------------

FROM ${REGISTRY}/presidio-python-deps

ARG NAME=presidio-analyzer
ADD ./${NAME}/analyzer /usr/bin/${NAME}/analyzer
WORKDIR /usr/bin/${NAME}/analyzer

CMD python __main__.py serve --env-grpc-port
