# Creating Manifest template using Kubectl 

There is a quick and less minial way of creating manifest template using kubectl commands along with it's flags this flag is called `--dry-run `. But there is limitation to this method, we cannot create all kind of manifests like statefulset and presistent volume. 

## Here are some of the examples

-Create a pod YAML
You can use your image here i am using `nginx:latest` 

`kubectl run mypod --image=nginx:latest --labels type=web --dry-run=client -o yaml > mypod.yaml`

-Create a pod servie YAML 
Your pod should be in running state inorder to integrate the service.

`kubectl expose pod mypod --port=80 --name mypod-service --type=NodePort --dry-run=client -o yaml > mypod-service.yaml`

-Create a Nodeport service YAML
Here you can select any nodeport from the range *30000-32767* and you can map it to the port your pod is exposed in my case it is 80.

`kubectl create service nodeport mypod --tcp=80:80 --node-port=30001 --dry-run=client -o yaml > mypod-service.yaml`

-Create a Deployment YAML
You can use your image over here

`kubectl create deployment mydeployment --image=nginx:latest --dry-run=client -o yaml > mydeployment.yaml`

-Create service YAML for you deployment
`kubectl expose deployment mydeployment --type=NodePort --port=8080 --name=mydeployment-service --dry-run=client -o yaml > mydeployment-service.yaml`

-Create job YAML
`kubectl create job myjob --image=nginx:latest --dry-run=client -o yaml`

-Create cronjob YAML
`kubectl create cj mycronjob --image=nginx:latest --schedule="* * * * *" --dry-run=client -o yaml`