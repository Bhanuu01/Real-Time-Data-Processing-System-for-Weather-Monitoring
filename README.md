# ClimaCast Weather Monitoring System

This repository contains a Django-based weather monitoring application with scheduled data collection, daily summaries, and alerting.

The project was built around a simple but useful systems question: how do you keep a small application updating external data reliably, summarize it on a schedule, and surface alerts when thresholds are crossed?

## What this repo includes

- a Django web application
- Celery workers for scheduled background jobs
- Redis as the task broker
- PostgreSQL-backed application data
- dashboard views for recent weather information and summaries
- temperature-threshold alerts

## Main workflow

- fetch weather data for configured cities on a schedule
- store the incoming values
- generate daily summaries
- check for alert conditions such as high temperature
- render the results in the dashboard

## Stack

- Django
- Celery
- Redis
- PostgreSQL
- Python

## Running locally

Install dependencies:

```bash
pip install -r requirements.txt
```

Apply migrations:

```bash
python manage.py makemigrations
python manage.py migrate
```

Start the Django server:

```bash
python manage.py runserver
```

Start Redis, then run Celery in separate terminals:

```bash
celery -A weather_monitoring worker --loglevel=info
celery -A weather_monitoring beat --loglevel=info
```

Populate default cities if needed:

```bash
python manage.py populate_cities
```

## Dashboard

Once the app is running, open:

- `http://127.0.0.1:8000/dashboard/`

The dashboard includes temperature views and supports switching between Celsius and Fahrenheit.

## Why this repo matters

This is a smaller project, but it shows the kind of backend habits I cared about early on: scheduled jobs, background processing, stateful application data, and alert-driven behavior instead of a static page.
