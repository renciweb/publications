FROM python:3.7

ENV PYTHONUNBUFFERED 1

RUN mkdir /src
COPY . /src
WORKDIR /src

###  Dependencies
RUN pip3 install pipenv
COPY Pipfile Pipfile
COPY Pipfile.lock Pipfile.lock
RUN pipenv install --deploy --system

### Static files server
RUN apt-get update && apt-get install nginx nano tree -y

### Migrate database
RUN python manage.py migrate
### Collect static files for serving to Django
RUN python manage.py collectstatic --noinput
