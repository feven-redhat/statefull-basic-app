Repo for a todo app statefull application with Quarkus and Postgresql

#Quickstart

```shell
git clone https://github.com/feven-redhat/statefull-basic-app.git
cd statefull-basic-app
```

```shell
oc create secret generic postgres-credentials     --from-literal=POSTGRES_USER=task-user     --from-literal=POSTGRES_PASSWORD=mysecretpassword     --from-literal=POSTGRES_DB=task     --from-literal=POSTGRES_PORT=5432
```

```shell
oc apply -f  postgres.yaml
oc apply -f quarkus-app-config.yaml
oc apply -f todo-app.yaml
```


# DYI Package the app

cd todo-demo

./mvnw package

podman build -f src/main/docker/Dockerfile.jvm -t quay.io/feven/todoapp:latest .
podman tag quay.io/feven/todoapp:latest quay.io/feven/todoapp:$APP_VERSION
podman push quay.io/feven/todoapp:$APP_VERSION
podman push quay.io/feven/todoapp:latest   

# Clean

oc delete ns demo-app

 
