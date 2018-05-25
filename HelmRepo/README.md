## Adding content to your own helm repo

Helm repo is basically http site with index.yaml file. Here is link to a blog post describing the idea.

https://medium.com/ibm-cloud/ibm-cloud-private-deployment-made-easy-with-helm-charts-1e72ddb3e88c

In this case I will use this githup repo as my helm repo. To do this I need to

1. Copy the helm chart .tgz files to this directory
2. Generate index.yaml file using helm repo index command

``` 
helm repo index . --url https://raw.githubusercontent.com/KKaski/DemoScripts/master/HelmRepo/
``` 

You need to force git to add the .tgz files to the repo since default .gitignore file ignores these files

```
git add -f node-red-0.1.1.tgz 
```

After this you need to push your modifications to the github.

``` 
git commit -m 'done'
git push
``` 

Add helm repository to the IBM Cloud Private. Select Manage / Helm Repositories and add the root directory to the dialog. In my case:

``` 
https://raw.githubusercontent.com/KKaski/DemoScripts/master/HelmRepo
``` 
Sync your Helm Repos by pressing Sync Repositories

## Adding locally developed apps

Docker deamon will fail to login on ICP private registry with self signed certificates. To overcome this problem add you ICP as insecure registry and restart your docker deamon.

``` 
sudo vi /etc/docker/daemon.json
``` 
Add the content like this (with you icp hostname)
``` 
{
    "insecure-registries" : [ "mycluster.icp:8500" ]
}
``` 
Initialize your private registry
```
bx pr registry-init -u admin -p admin --server mycluster.icp:8500
```
