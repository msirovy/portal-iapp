Example kubernetes static application
=====================================

Example application with my bussines static html page. 


Deployment
----------
  - create git repository including application and Dockerfile
  - create dockerhub autobuild image service with this git code
  - create dedicated namespace for application on kubernetes cluster
    ```
    kubectl create -f iapp-ns.yaml
    ```
  - create replication controler on kubernetes cluster
    ```
    kubectl create -f iapp-rc.yaml
    ```
  - create service on Kubernetes cluster
    ```
    kubectl create -f iapp-svc.yaml
    ```


Rolling update
--------------
This method simplify HA deployment of new versions to production environment. It's simply start new application next to current working application, and than set service to send requests to new instance of application. It's bring lot off issue in case the new version do any db migrations or something simmilar, but if everything is possible. In this simple case deployment is simply this one command

    ```
    kubectl rolling-update www-iapp-${CUR_NAME} www-iapp-${NEW_NAME} --image=msirovy/portal-iapp --namespace iapp
    ```


