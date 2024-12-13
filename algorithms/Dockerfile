FROM --platform=linux/amd64 python:3.11-slim AS example-algorithm-amd64

# Ensures that Python output to stdout/stderr is not buffered: prevents missing information when terminating
ENV PYTHONUNBUFFERED=1

RUN groupadd -r user && useradd -m --no-log-init -r -g user user
USER user

WORKDIR /opt/app

COPY --chown=user:user requirements.txt /opt/app/

# You can add any Python dependencies to requirements.txt
RUN python -m pip install \
    --user \
    --no-cache-dir \
    --no-color \
    --requirement /opt/app/requirements.txt

COPY --chown=user:user inference.py /opt/app/

# Just for the workshop; we make every image completely unique. Bad practice.
ARG BUILD_VERSION
RUN echo "Build version: $BUILD_VERSION"

ENTRYPOINT ["python", "inference.py"]
