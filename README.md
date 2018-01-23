# DemoScripts

#CFtoKubernetes
Purpose of this demo script is to show how to do put existing CF app to run in the Kubernetes cluster at IBM Cloud

##Foundation
1. Create example node.js app cft0kubex
2. Enable CI for the app 
3. git clone (url)
4. Modify the public/index.html, git commit -m, git push Validate that the delivery pipeline works

##Kubernetes enablement
1. bx dev enable
2. Look for the content that was generated
3. Run locally
4. bx dev build
5. bx dev run

##Modify deliverypipeline
1. Add new build stage to build docker container
    - Check the region
    - Check the name space (bx cr namespace-list)
2. Add new Deploy stage to deploy to kubernetes kluster
    - Create API key
    - Define region
    - Define clustername
3. git add .
4. git commint -m kuebe
5. git push
6. Follow the delivery pipelines so that the run

##Check the resuts form command line
1. bx cs clusters
2. bx cs cluster-config mydemocluster2
3. set env variables
4. export KUBECONFIG=/Users/kimmok/.bluemix/plugins/container-service/clusters/mydemocluster2/kube-config-hou02-mydemocluster2.yml
5. kubectl get deployments
6. kubectl get pods
7. kubectl get svc
8. kubectl describe pod xxx

##Do the same thing with Helm
1. Before doing this you might need to delete the existing deployment and service
3. Check the images in the image repository bx cr images
4. go to the ./char/cftokube3 directory
5. edit values.yaml and correct the namespace and tag information to relate your image
6. hel install ./chart/cftokube3

