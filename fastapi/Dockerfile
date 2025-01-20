# Stage 1: Builder
FROM python:3.13 AS builder

WORKDIR /code

# Install dependencies
COPY ./requirements.txt /code/requirements.txt
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

# Stage 2: Runtime
FROM python:3.13-slim AS runtime

WORKDIR /code

# Copy only necessary files from the builder stage
COPY --from=builder /usr/local/lib/python3.13/site-packages /usr/local/lib/python3.13/site-packages
COPY --from=builder /usr/local/bin /usr/local/bin

# Copy the application code
COPY ./ /code/

CMD ["fastapi", "run", "--host", "0.0.0.0", "--port", "80"]
