# simple-web

Running simple-web application on azure kubernetes cluster
By using virtual machine in azure platform, to connect to AKS cluster, deploy simple-web application.
This machine also host jenkins application with job deploy-desdtroy-simple-web, with 2 option to deploy or destroy the app.  


prerequisites cli tools and Env use:
  * azure cli
  * kubectl
  * helm cli
  * virtual machine in azure that has permision to connect to resources using managed identity

installation:
  * jenkins on the virtual machine
  * Ingress controller on the kubernetes cluster

jenkins job deploy-desdtroy-simple-web:
  * connect to azure using managed identity
  * connect to aks cluster 
  * check if the app is already running
  * if the selection was to deploy, and the app is not running or in terminating phase, running command helm install.
  * if the selection was to destroy, and the app is not running or not in terminating phase, running command helm uninstall 
  
http://20.101.63.153:8080/job/deploy-desdtroy-simple-web/ 


simple-web auto-scaler
  * using KEDA, defined 3 triggers for auto scale:
    - between 8:00am to 12:00am
    - cpu 150
    - memory 150
