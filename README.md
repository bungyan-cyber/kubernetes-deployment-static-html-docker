static-html-docker-server-kubernetes-deployment<a name="TOP"></a>
===================

- - - - 
# Heading 1 #

    Steps for Deploying a Static HTML Site with Docker   

* docker build -t index-app:v1 .

* docker run -d -p 80:80 index-app:v1

* docker ps

* docker container 

* docker image list

Steps for push to dockerhub repository

* docker tag index-app:v1 bungyan07/index-app:v1

* docker login 

* docker push bungyan07/index-app:v1

## Heading 2 ##

Service Deployment Into Kubernetes
Kubernetes service yaml = default

apiVersion: apps/v1
kind: Deployment
metadata:
  name: index-app-deployment
  labels:
    app: index-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: index-app
  template:
    metadata:
      labels:
        app: index-app
    spec:
      containers:
      - name: index-app
        image: bungyan07/index-app:v1
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 500m
            memory: 200Mi
          requests:
            cpu: 200m
            memory: 100Mi
---
apiVersion: v1
kind: Service
metadata:
  name: index-app-service
  labels:
  app: index-app
spec:
  selector:
    matchLabels:
    app: index-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer


### Heading 3 ###

    Markup :  ### Heading 3 ###

#### Heading 4 ####

    Markup :  #### Heading 4 ####


Common text

    Markup :  Common text

_Emphasized text_

    Markup :  _Emphasized text_ or *Emphasized text*

~~Strikethrough text~~

    Markup :  ~~Strikethrough text~~

__Strong text__

    Markup :  __Strong text__ or **Strong text**

___Strong emphasized text___

    Markup :  ___Strong emphasized text___ or ***Strong emphasized text***

[Named Link](http://www.google.fr/ "Named link title") and http://www.google.fr/ or <http://example.com/>

    Markup :  [Named Link](http://www.google.fr/ "Named link title") and http://www.google.fr/ or <http://example.com/>

