# Use the official Python image.
# https://hub.docker.com/_/python
FROM python:3.7-slim

# Copy local code to the container image.
ENV APP_HOME /app
WORKDIR $APP_HOME
COPY . ./

ARG PROJECT_ID
ENV PROJECT_ID ${PROJECT_ID}
ENV PROMETHEUS_MULTIPROC_DIR /tmp/prometheus-multiproc

RUN mkdir -p $PROMETHEUS_MULTIPROC_DIR && chown -R nobody:nogroup $PROMETHEUS_MULTIPROC_DIR && chmod -R 777 $PROMETHEUS_MULTIPROC_DIR



# Install production dependencies.
RUN apt-get update && \
    pip install --upgrade pip && \
    pip install -r requirements.txt

CMD ["gunicorn", "--access-logfile", "-", "--error-logfile", "-", "-w", "4", "-b", "0.0.0.0:8080", "app:app"]
