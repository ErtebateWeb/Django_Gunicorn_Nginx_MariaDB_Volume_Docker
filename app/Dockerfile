FROM python:alpine

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV DJANGO_SUPERUSER_PASSWORD admin



RUN mkdir /app
ADD ./requirements.txt /app/

WORKDIR /app

RUN apk update
RUN apk add --no-cache gcc python3-dev musl-dev mariadb-dev

RUN pip install --upgrade pip
RUN pip install -r requirements.txt
# RUN pip install django==3.2.12 gunicorn mysqlclient

RUN apk del gcc python3-dev musl-dev

CMD while ! python3 manage.py sqlflush > /dev/null 2>&1 ; do sleep 1 ; done && \
    python3 manage.py makemigrations --no-input && \
    python3 manage.py migrate --no-input && \
    python3 manage.py collectstatic --no-input && \
    python3 manage.py createsuperuser --username admin --email ertebateweb@gmail.com --no-input; \
    gunicorn -b 0.0.0.0:8000 config.wsgi

