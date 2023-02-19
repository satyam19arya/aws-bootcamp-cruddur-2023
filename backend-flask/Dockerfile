FROM python:3.10-slim-buster

# make a new folder inside container
WORKDIR /backend-flask

# this contains the libraries want to install to runt the app
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

ENV FLASK_ENV=development

EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]