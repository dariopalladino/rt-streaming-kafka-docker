FROM python:3.8-slim

LABEL maintainer="Dario Palladino <dario.palladino@gmail.com>"

# App setup
COPY . /app
WORKDIR /app
RUN pip install --upgrade pip
RUN pip install kafka-python

EXPOSE 5555

CMD ["python", "udp_to_kafka.py"]