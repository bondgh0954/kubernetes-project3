<h1>Kubernetes Demo Project3</h1>
<h2>Technologies used</h2>

- <b>K8s</b> 
- <b>Helm</b>
- <b>MongoDB</b>
- <b>MongoExpress</b>
- <b>Linode LKE</b>
- <b>Linux</b>


<h2>Detailed Description of Project </h2>
1. Create a managed K8s cluster with Linode Kubernetes Engine<br/>
2. Deploy replicated MongoDB service in LKE cluster using a Helm chart<br/>
3. Configure data persistence for MongoDB with Linode's cloud storage<br/>
4. Deploy UI client Mongo Express for MongoDB<br/>
5. Deploy and configure nginx ingress to access the UI application from browser<br/>

   <p align="">
   <h2>step1</h2>
   Create K8s cluster on Linode Kubernetes Engine(LKE)<br/>
   Download the 'kubeconfig file' after creating the cluster<br/>
   change permissions of the file so that only the user can have read access to the file<br/>
   chmod 400 filename<br/>
   <img src='./im/kimg.png' height="80%" width="80%" alt="Disk Sanitization Steps">
   export the file as environmental variable<br/>
   export KUBECONFIG=filename.yaml<br/>
   Now connected to the cluster<br/>
   <img src='./im/kimg.png' height="80%" width="80%" alt="Disk Sanitization Steps">

  <h2>step2</h2>
  Deploy MongoDB statefulSet in the cluster using bundles of config files (Helm Chart)<br/>
  Install Helm in order to search for helm chart<br/>
  check official document for installation guide<br/>
  
 <img src='./sp/kimage7.png' height="80%" width="80%" alt="Disk Sanitization Steps">

  Add the repository that contains the MongoDB chart<br/>
  helm repo add bitnami https://charts.bitnami.com/bitnami<br/>
  helm search repo bitnami (shows all charts the repository contains)<br/>
  helm search repo bitnami/mongodb<br/>
  <img src='./sp/kimage6.png' height="80%" width="80%" alt="Disk Sanitization Steps">

  The helm charts has default values that need to be overridden:<br/>
  eg. set architecture to replicaSet<br/>
      set auth.rootPassword <br/>
      override volume to use eg. linode volume<br/>
 Create a file that will contain key value pair that need to be overridden<br/>
 filename: 'helm-mongodb.yaml'<br/>
 Issue a command that will install that chart with the values created<br/>
 helm install[ourname] --values[values filename] [chart name]<br/>
 helm install mongodb --values helm-mongodb.yaml bitnami/mongodb<br/>

 Mongodb chart installed and deployed with the values in the cluster<br/>
 <img src='./sp/kimage8.png' height="80%" width="80%" alt="Disk Sanitization Steps">

 mongodb pods running in the cluster<br/>
 <img src='./sp/kimage8.png' height="80%" width="80%" alt="Disk Sanitization Steps">
 

<h2>step3</h2>
Deploy mongo express which is the UI for mongodb<br/>
create a mongo express deployment and mongo-express service using a configuration file 
eg. file ('mongo-exp.yaml')
set the environmental values for mongo-express
reference the value of the rootpassword from the secret that is created with the mongodb helm chart

  
 <img src='./sp/kimage8.png' height="80%" width="80%" alt="Disk Sanitization Steps">

 <h2>step4</h2>
 Since mongo-express service is an internal service we need to open it to external so that it can be accessed in the browser
 this is done using "ingress"
 1. deploy ingress controller
 2. configure ingress rule

 Use helm chart to deploy ingress controller
 add the repository of the helm chart
 eg. helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
 install the helm chart after adding the repo
 eg. helm install nginx-ingress ingress-nginx/ingress-nginx --set controller-publicService.enable=true
 to make sure we automatically allocate a public IP address for ingress address to use with nginx we pass in the following command during installation of the chart
 (--set controller-publicService.enabled=true)
 A NodeBalancer will be dynamically created in linode as the ingress controller is deployed
 The NodeBalancer becomes the entry point to the cluster


  
 <img src='./sp/kimage10.png' height="80%" width="80%" alt="Disk Sanitization Steps">

 <h2>step5</h2>
Configure Ingress Rule
Create ingress rule for mongo-express
with configuration file eg. "helm-ingress.yaml"

   
    
    
   
     

</p>
