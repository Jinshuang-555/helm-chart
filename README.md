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

helm install app1 appchart

helm list -a
kubectl get all

8. upgrade application helm chart

change version 0.1.0 -> 0.1.1 // chart.yaml
change the replica 1 -> 2 // values.yaml

helm upgrade app1 appchart

helm list -a
kubectl get all 

9. roll back helm release:

helm rollback release versionNo.

helm rollback app1 1

helm list -a
kubectl get all 

10. delete helm release

helm delete app1.0 (release name)





