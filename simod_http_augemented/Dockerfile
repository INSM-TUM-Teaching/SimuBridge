# Dockerfile for Simod HTTP wrapper using Simod 5.1.6
# Based on the official nokal/simod:5.1.6 image

FROM nokal/simod:5.1.6

# Prevents Python from writing pyc files and buffering stdout/stderr
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Install dependencies for the HTTP wrapper
COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt

# Create storage directory
RUN mkdir -p /tmp/simod

# Copy the HTTP wrapper
WORKDIR /app
COPY main.py /app/main.py

# Expose port
EXPOSE 80

# Run the HTTP server
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80", "--log-level", "info"]
