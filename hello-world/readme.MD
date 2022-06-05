Sample application using helm.
steps:
1.  helm add stable repo
`helm repo add stable https://charts.helm.sh/stable`
2. Create a heml hello worl applciation
`helm create hello-world`
3. Create a namespace
`kubectl create namespace dev`
4. deploy the application
`helm install -f hello-world/values.yaml -n dev hello-world ./hello-world`
5.  export the pod name
`export POD_NAME=$(kubectl get pods --namespace dev -l "app.kubernetes.io/name=hello-world,app.kubernetes.io/instance=hello-world" -o jsonpath="{.items[0].metadata.name}")`
6. export container port
`export CONTAINER_PORT=$(kubectl get pod --namespace dev $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")`
7. forward the port
`kubectl --namespace dev port-forward $POD_NAME 8080:$CONTAINER_PORT`
8. To find out which cluster Tiller would install to
`kubectl config current-context`
9. 