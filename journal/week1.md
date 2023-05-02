# Week 1 — App Containerization

✅ Installed Docker extension for vs code
    https://code.visualstudio.com/docs/containers/overview
    
✅ Created a Dockerfile for backend-flask
   ```
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
  ```
   Run the following commands:
   ```
   cd backend-flask/
   pip install -r requirements.txt
   export FRONTEND_URL="*"
   export BACKEND_URL="*"
   python3 -m flask run --host=0.0.0.0 --port=4567
   ```
   
  - make sure to unlock the port on the port tab
  - open the link for 4567 in your browser
  - append to the url to /api/activities/home
  - you should get the json data
  - to make JSON easy to read install JSON Formatter chrome extension
  
  ```
  unset FRONTEND
  unset BACKEND
  ```
  To build image
  ```
  cd ..
  docker build -t  backend-flask ./backend-flask
  ```
  
  To check
  ```
  docker images
  ```
  To run container
  ```
  FRONTEND_URL="*" BACKEND_URL="*" docker run --rm -p 4567:4567 -it backend-flask
  docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
  ```
  To run in background
  ```
  docker container run --rm -p 4567:4567 -d backend-flask
  ```
  To get Container Images or check running Container Ids
  ```
  docker ps
  docker images
  ```
  To check Container Logs
  ```
  docker logs CONTAINER_ID -f
  docker logs backend-flask -f
  ```
  
  ✅ Created a Dockerfile for frontend
  ```
  cd frontend-react-js
  npm i
  ```
  Create Docker File
  ```
  FROM node:16.18

  ENV PORT=3000

  COPY . /frontend-react-js
  WORKDIR /frontend-react-js
  RUN npm install
  EXPOSE ${PORT}
  CMD ["npm", "start"]
  ```
  To build Container
  ```
  docker build -t frontend-react-js ./frontend-react-js
  ```
  To run container
  ```
  docker run -p 3000:3000 -d frontend-react-js
  ```
  
  ✅ Docker compose
  ```
  Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then,     with a single command, you create and start all the services from your configuration.
  ```
  Create docker-compose.yml at the root of your project.
  ```
    version: "3.8"
    services:
      backend-flask:
        environment:
          FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
          BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
        build: ./backend-flask
        ports:
          - "4567:4567"
        volumes:
          - ./backend-flask:/backend-flask
      frontend-react-js:
        environment:
          REACT_APP_BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
        build: ./frontend-react-js
        ports:
          - "3000:3000"
        volumes:
          - ./frontend-react-js:/frontend-react-js

    # the name flag is a hack to change the default prepend folder
    # name when outputting the image names
    networks: 
      internal-network:
        driver: bridge
        name: cruddur
  ```
  Run docker compose up and the Docker compose command starts and runs your entire app
  <img width="936" alt="image" src="https://user-images.githubusercontent.com/77580311/220022365-4bb172c2-c822-4080-a536-e9cefd97fdab.png">
  
  # Adding DynamoDB Local and Postgres
  Add following into our existing docker compose file:
  ```
      db:
        image: postgres:13-alpine
        restart: always
        environment:
          - POSTGRES_USER=postgres
          - POSTGRES_PASSWORD=password
        ports:
          - '5432:5432'
        volumes: 
          - db:/var/lib/postgresql/data
    volumes:
      db:
        driver: local
  ```
  ```
  dynamodb-local:
    user: root
    command: "-jar DynamoDBLocal.jar -sharedDb -dbPath ./data"
    image: "amazon/dynamodb-local:latest"
    container_name: dynamodb-local
    ports:
      - "8000:8000"
    volumes:
      - "./docker/dynamodb:/home/dynamodblocal/data"
    working_dir: /home/dynamodblocal
 ```
  
