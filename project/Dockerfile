FROM python:3.9-slim-buster

# Set the working directory in the container
WORKDIR /app

ARG APP_UID=1000
ARG APP_GID=1000

RUN groupadd --gid "$APP_GID" appuser \
    && useradd --uid "${APP_UID}" --gid "$APP_GID" \
        --create-home --no-log-init appuser

# Copy the requirements file into the container
COPY requirements.txt .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code into the container
COPY --chown=appuser:appuser . .

# Expose the port the application will run on
EXPOSE 5001

# Define environment variable
#ENV FLASK_APP=main.py

# Run the application
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5001", "main:app"]