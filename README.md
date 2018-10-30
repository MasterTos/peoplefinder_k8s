# Django kubernetes template

## Create and publish Docker containers
### Django app running within uwsgi
Build the container:

````
cd path/to/you/app
docker build -t username/django-app:1 .
````
Push it to a repository:

````
docker login
docker push username/django-app:1
````

## Deploy these containers to the Kubernetes cluster

### Config template file
- Replace all `peoplefinder` to name of your app.
- Edit postgres/volume and postgres/volume_claim.
- Edit configMap and Secrets in django/configmap and postgres/secrets.
- Edit `<Image>:<Tag>` to your app image.
### PostgreSQL
```
cd postgres
kubectl create -f .

kubectl get deployment
kubectl get pods
kubectl get svc
```

### Django app running within uwsgi
```
cd django
kubectl create -f configmap.yaml
kubectl create -f deployment.yaml
kubectl create -f service.yaml

kubectl get deployment
kubectl get pods
kubectl get svc

kubectl create -f job-migration.yaml
```