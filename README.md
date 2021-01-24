# Instruction for creating a vue application with a CI/CD pipeline, hosted on GCP

## What you'll need installed

- Docker
- node/npm
- gcloud cli
- kubectl cli

## Creating the Vue application

```shell
npm install -g @vue/cli
vue create app_name
cd app_name
npm run build
```

### Create a Docker Image That bundles the Vue App with nginx

```shell
# Dockerfile
FROM nginx:1.17
COPY ./nginx.conf /etc/nginx/nginx.conf
WORKDIR /app
COPY ./dist .
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
```

### Build a docker image

```shell
docker build -t cicd .
```

### Start the container

```shell
docker run -d --rm --name app_name -p 3000:8080 cicd
```

Test that your application is working by navigation to localhost:8080

You should see a basic vue application.
Changes made to the src _should_ be mirrored in the docker container.

### Stop the container

```shell
docker stop app_name
```
