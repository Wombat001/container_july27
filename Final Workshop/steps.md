# Steps to complete the final workshop
## Contents
- [Setup](##-Setup)
- [Namespace](##-Namespace)
- [Secret](##-Secret-Creation-/Generation)
- [DB_Cluster](##-DB-Cluster)
- [ConfigMap](##-ConfigMap)
- [Deployment](##-Deployment)
- [Service](##-Service)
- [Port_Forwarding](##-Port-Forwarding)
- [Ingress](##-Ingress)
- [Final_Confirmation](##-Final-confirmation)

## Setup
- Make sure the MSP - Digital Ocean (DO) is setup properly
- Ensure the Docker Hub account is setup and you have logged in. 
- Create and deploy a K8s cluster on DO
- Download config file 
- export KUBECONFIG="/Users/taychoonwei/Documents/Final Workshop/mydokubecluster-kubeconfig.yaml" {set the config file in the system environment}
- echo $KUBECONFIG {check the config file and location}
- kubectl cluster-info {ensure the cluster (kubernetes Master) is up and running}
    - kubectl cluster-info dump {for very **detailed** information of the cluster and components}
- touch . fwkapp.yaml {create the yaml file for service / deployment specification}
- touch . fwkcluster.yaml {create the yaml file for cluster}
- touch . fwkdb.yaml {create the yaml file for db}
- touch . fwk-secret.yaml {create yaml file for secret}

## Namespace 
- kubectl create ns fwk {create a new namespace}
- kubectl get po -n kube-system {for pod listing}
- kubectl get svc -n kube-system {for svc discovery}
- kubectl get ns {for namespace}

## Secret Creation /Generation
- echo -n secret | base64 {generate the secret on base64}
- Open fwk-secret.yaml with the favorite editor
- Input the script to configure the secret and save 
- kubectl apply -f fwk-secret.yaml -n fwk {apply fwk-secret.yaml in the fwk namespace}
- kubectl get secret/fwk-secret -n fwk >> results.txt {get the fwk-secret yaml file to ensure it's gotten applied successfully, recording the information in results.txt}
- 

## DB Cluster
- Open fwkdb.yaml with the favorite editor
- Input the script to set up and deploy the db while including the secret to access the db
- kubectl apply -f fwkdb.yaml -n fwk {apply the fwkdb.yaml configuration file}
- kubectl get mysql -n fwk {inspect and confirm that the db has been setup and deployed properly}

## ConfigMap
- Open fwkapp.yaml with the favorite editor
- Input script to set up for the configmap
- kubectl apply -f fwkapp.yaml -n fwk {apply the CM component in the fwk namespace}
- kubectl get cm -n fwk >> results.txt {inspect and confirm that CM is up and running, recording the information in results.txt}

## Deployment 
- Open fwkapp.yaml with the favorite editor
- Input script to configure the deployment conditions & strategy while including the PVC 
- kubectl apply -f fwkapp.yaml -n fwk {apply the deployment and storage configuration in the fwk namespace}
- kubectl get pv, pvc -n fwk >> results.txt {inspect and confirm the deployment is up and running, recording the information in results.txt}
 

## Service
- Open the fwkapp.yaml with the favorite editor 
- Input the service settings information and save
- kubectl apply -f fwkapp.yaml -n fwk {apply fwkapp.yaml in the fwk }
- kubectl get svc/fwkapp-svc -n fwk >> results.txt {inspect and confirm the service component, recording the information in results.txt}

## Port-forwarding
- kubectl port-forward svc/fwksvc 8080:80 -n fwk {do a portforward to test the availability of the workpress service}
- Input the localhost url into the browser to determine that the wordpress page is up and available

## Ingress 
- Open the fwkapp.yaml with the favorite editor 
- Input the ingress settings information and save
- kubectl apply -f fwkapp.yaml -n fwk {apply fwkapp.yaml in the fwk }
- kubectl get svc -n nginx-ingress -o wide >> results.txt {inspect the service created for the ingress and record the findings in results.txt as a log}
- kubectl get all,ing,mysql,pv,pvc -n fwk >> results.txt {Do a final inspection of the myriad services deployed so far and record the results in results.txt }

## Final confirmation
- Input into the browser the DNS IP for the wordpress deployment
- Visually inspect and confirm the wordpress application is deployed successfully   

 