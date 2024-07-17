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
   export the file as environmental variable<br/>
   export KUBECONFIG=filename.yaml<br/>
   Now connected to the cluster<br/>
   <img src='./im/kimg5.png' height="80%" width="80%" alt="Disk Sanitization Steps">


   <img src='./im/kimg4.png' height="80%" width="80%" alt="Disk Sanitization Steps">

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
  
 <img src='./sp/kimage8.png' height="80%" width="80%" alt="Disk Sanitization Steps">


  
 <img src='./sp/kimage10.png' height="80%" width="80%" alt="Disk Sanitization Steps">

   
    
    
   
     

</p>
