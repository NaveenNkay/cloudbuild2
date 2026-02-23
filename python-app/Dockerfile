FROM python:3.11-slim as builder

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# Install dependencies
COPY requirements.txt .

RUN pip install --prefix=/install --no-cache-dir -r requirements.txt

#multi stage build
FROM python:3.11-slim

WORKDIR /app
COPY --from=builder /install /usr/local/
# Copy application code
COPY app.py .

# Create non-root user without home directory and switch to that user
# RUN useradd --create-home --shell /bin/bash appuser
# USER appuser

EXPOSE 8080

CMD ["gunicorn", "--bind", "0.0.0.0:8080", "app:app"]