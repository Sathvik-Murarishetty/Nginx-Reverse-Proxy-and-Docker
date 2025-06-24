FROM python:3.13-slim-buster AS builder

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends build-essential && rm -rf /var/lib/apt/lists/*
RUN pip install --no-cache-dir --upgrade pip && pip install --no-cache-dir uv

COPY uv.lock .
COPY pyproject.toml .

RUN uv pip install --no-cache-dir -f uv.lock
RUN uv pip install --no-cache-dir gunicorn

COPY app.py .

FROM python:3.13-slim-buster

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.13/site-packages /usr/local/lib/python3.13/site-packages
COPY --from=builder /app/app.py /app/app.py

EXPOSE 8002

CMD ["gunicorn", "--bind", "0.0.0.0:8002", "app:app"]