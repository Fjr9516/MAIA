ARG BASE_IMAGE
FROM $BASE_IMAGE


USER root
# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apt-get install -y default-libmysqlclient-dev build-essential pkg-config
RUN mkdir /etc/MAIA-Dashboard
WORKDIR /etc/MAIA-Dashboard
COPY requirements.txt /etc/MAIA-Dashboard
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

COPY manage.py /etc/MAIA-Dashboard
COPY apps /etc/MAIA-Dashboard/apps
COPY core /etc/MAIA-Dashboard/core

COPY start.sh /etc/MAIA-Dashboard


#COPY MAIA /etc/MAIA-Dashboard/MAIA
#COPY MAIA_scripts /etc/MAIA-Dashboard/MAIA_scripts

#COPY db.sqlite3 /etc/MAIA-Dashboard
#COPY env env

ENTRYPOINT ["bash", "start.sh"]
# gunicorn
CMD [ "python", "manage.py", "runserver", "0.0.0.0:8000","--insecure"]
#CMD ["gunicorn", "--config", "gunicorn-cfg.py", "core.wsgi"]

