# helm-chart
This is the repo for application helm chart which can help deploy applications to kubernetes cluster

1. create the helm chart for new application:

helm create appchart 

2. modify the values.yaml file :

change the application image and port to the corresponding docker hub repo and tag

3. check the actual values for the real helm chart:

helm template appchart 

4. check the error for helm chart 

helm lint appchart

5. helm --debug --dry-run

// first appchart is a release name

helm install appchart --debug --dry-run appchart

6. helm intsall releasename chartname

// ---- pass value file into helm install -------

hell install -f myvals.yaml ./mychart

// ----- individual paramenters passed with ---------

hell install --set elasticsearchHosts=http://localhost:9200"

helm install app1 appchart

helm install appstest

helm list -a
kubectl get all

export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=appchart,app.kubernetes.io/instance=app1" -o jsonpath="{.items[0].metadata.name}")

POD_NAME=app1-appchart-5c65bdfd45-ktc7l 

kubectl describe pod $POD_NAME 
kubectl logs $POD_NAME -c init-container 
kubectl logs $POD_NAME -c appchart 
kubectl logs $POD_NAME -c appchart-search 

kubectl get svc release-name-appchart

export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
echo "Visit http://127.0.0.1:8080 to use your application"
kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT

8. upgrade application helm chart

change version 0.1.0 -> 0.1.1 // chart.yaml
change the replica 1 -> 2 // values.yaml

helm upgrade app1 appchart --set image1.tag=app-1682711158

helm list -a
kubectl get all 

9. roll back helm release:

helm rollback release versionNo.

helm rollback app1 1

helm list -a
kubectl get all 

kubectl get services

10. delete helm release

helm delete app1 (release name)

kubectl port-forward service/app1-appchart 8081:8081
kubectl port-forward app1-appchart-5b545d889b-7j9ch 8082:8082


kubectl logs $POD_NAME -c istio-proxy


  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=searchchart,app.kubernetes.io/instance=search1" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")

  kubectl exec -it $POD_NAME -- /bin/sh