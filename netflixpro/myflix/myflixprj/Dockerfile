# Use an official Python runtime as a parent image
FROM python:3.11.7-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

RUN sudo apt install python3-pip
# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Use a non-root user for security
RUN adduser --disabled-password --gecos '' myuser
USER myuser

# Define environment variable
ENV DJANGO_SETTINGS_MODULE="netflixpro\myflix\myflixprj\myflixprj.settings"

# Apply migrations and collect static files
RUN python manage.py migrate
RUN python manage.py collectstatic --noinput

# Use Gunicorn as the production server
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "netflixpro\myflix\myflixprj\myflixprj.wsgi:application"]

