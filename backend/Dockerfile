FROM python:3.11-slim

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    git \
    curl \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt gunicorn

COPY . .

ENV PYTHONUNBUFFERED=1
ENV BACKEND_PORT=8010
ENV FLASK_DEBUG=off

EXPOSE 8010

CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:8010", "--workers", "1", "--threads", "2", "--timeout", "1500"]
