secrets ra configmap , nodejs app ra mongo db config or connect garna lai ho 

secrets le mongo db ko user name password ra configmap le mongo db ko url hold garxa 

service le web lai external access ko lagi kam garxa 

![alt text](image.png)  = all component communication s

![alt text](image-1.png)    = configmap

cnofig ra secrete ko acutual data , data vanne ma hunxa . 
Secrete ko data ko values base64 ma encoded hunu parxa , HUNXA 


DEPLOYMENT RA SERVICE  dui chuttai yaml file banauda ni hunxa but they belong together ( all deployment need services) so ahutai file ma rakhda ni hunxa 
mathi deployment ani last tira --- paxi service 


***selector***
    1. Purpose : The selector field in a Deployment specifies how to identify the Pods that the Deployment should manage.
    2. Components: It typically contains matchLabels or matchExpressions, which define the criteria to select Pods.
***matchLabels***
    1. Purpose: The matchLabels field is a key-value pair that must match the labels on the Pods for them to be managed by the Deployment.
    2. Simplification: It is a simple and straightforward way to specify criteria. Pods with labels that match these key-value pairs are selected.

***template***
    1. Defines the Pod configuration.
    2. Ensures consistency across all Pods managed by the Deployment.
    3. Part of the Deployment spec. **imp point**
***Deployment***
   1.  Manages the lifecycle of Pods defined by the template.
   2.  Controls the number of replicas.
    3. Handles updates and scaling.
    4. Uses the s to create and update Pods.

***Deployment ko afnai meta data ra spec hunxa same to template , template ko ni meta data hunxa ani sepc pani***
![alt text](image-2.png)

lables = key value pair ma hunxa pod ma compuslory hunxa cinina ko lagi kun k ho vanera 
![alt text](image.png)
![alt text](image-1.png)
label , configm , pod, secre sabai ko rakhna milxa , 
***POD ma label is compulsory but aru lai ni rakhna milxa for better readable***


Replica = mean how many pod you want to create
![alt text](image.png)



Service = externale expose ra pod bich communicate garauney, yo bhitra ko selector le cahi service lai pod sanga connect or communicate garauxa, kun pod sanga communicate garney vnane cahi selector le garxa 
![alt text](image.png)

port in service 
![alt text](image.png)

port vaneko service ko port
targeport vaneko  pod ko port ho , such as mangodb pod ko port
subai same rakhna milxa dubai port ko value 
![alt text](image.png)


Deployment and service component ma configmap ra secrete ko data pathaunu parxa 
![alt text](image-1.png)
- tyo deployment file ma envrionemnt variable banayera rakhnu parxa configmap ra secrete ko data 
![alt text](image.png)

webapp commicating with db
![alt text](image.png)


SERVICE ki internal service hunxa jun pod bicha communicate garxa ki external service hunxa jun externally webapp lai access garna use hunxa 
-now web app externally avaialbel banauna lai web app ko service ma spec ma type NodePort rakera garnu parxa 
-NOdeport vaneko external service type ho
![alt text](image.png)



Run garna lai tala ko her aba
### Repository for the K8s in 1 hour video

#### K8s manifest files 
* mongo-config.yaml
* mongo-secret.yaml
* mongo.yaml
* webapp.yaml

#### K8s commands

##### start Minikube and check status
    minikube start --vm-driver=hyperkit 
    minikube status

##### get minikube node's ip address
    minikube ip

##### get basic info about k8s components
    kubectl get node
    kubectl get pod
    kubectl get svc
    kubectl get all

##### get extended info about components
    kubectl get pod -o wide
    kubectl get node -o wide

##### get detailed info about a specific component
    kubectl describe svc {svc-name}
    kubectl describe pod {pod-name}

##### get application logs
    kubectl logs {pod-name}
    
##### stop your Minikube cluster
    minikube stop

<br />

> :warning: **Known issue - Minikube IP not accessible** 

If you can't access the NodePort service webapp with `MinikubeIP:NodePort`, execute the following command:
    
    minikube service webapp-service

<br />

#### Links
* mongodb image on Docker Hub: https://hub.docker.com/_/mongo
* webapp image on Docker Hub: https://hub.docker.com/repository/docker/nanajanashia/k8s-demo-app
* k8s official documentation: https://kubernetes.io/docs/home/
* webapp code repo: https://gitlab.com/nanuchi/developing-with-docker/-/tree/feature/k8s-in-hour
