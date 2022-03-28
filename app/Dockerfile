FROM python:alpine

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV DJANGO_SUPERUSER_PASSWORD admin



RUN mkdir /app
WORKDIR /app

RUN pip install --upgrade pip
# RUN pip install -r requirements.txt
RUN pip install django==3.2.12 gunicorn

CMD python3 manage.py makemigrations --no-input && \
    python3 manage.py migrate --no-input && \
    python3 manage.py collectstatic --no-input && \
    python3 manage.py createsuperuser --username admin --email ertebateweb@gmail.com --no-input; \
    gunicorn -b 0.0.0.0:8000 config.wsgi

