# Stage 1: Build the application
FROM python:3.9-slim as builder

# Set the working directory
WORKDIR /app

# Copy the requirements file
COPY requirements.txt .

# Install dependencies in a virtual environment
RUN python -m venv /opt/venv && \
    /opt/venv/bin/pip install --no-cache-dir -r requirements.txt

# Stage 2: Create the final lightweight image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the virtual environment from the builder stage
COPY --from=builder /opt/venv /opt/venv

# Copy the application code
COPY app.py .

# Set environment variables
ENV FLASK_APP=app.py
ENV FLASK_ENV=production
ENV PATH="/opt/venv/bin:$PATH"

# Expose port 5000
EXPOSE 5000

# Run the application using Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]