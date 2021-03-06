

# Interactive Tutorial - Creating a Cluster (Module 1)

> 使用 Minikube 创建一个集群 https://kubernetes.io/zh/docs/tutorials/kubernetes-basics/cluster-intro/
>> Interactive Tutorial - Creating a Cluster https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-interactive/

## Step 1 Cluster up and running

We already installed minikube for you. Check that it is properly installed, by running the `minikube version` command:
```
$ minikube version
minikube version: v0.28.2
```

OK, we can see that minikube is in place.

Start the cluster, by running the `minikube start` command:
```
$ minikube start
Starting local Kubernetes v1.10.0 cluster...
Starting VM...
Getting VM IP address...
Moving files into cluster...
Setting up certs...
Connecting to cluster...
Setting up kubeconfig...
Starting cluster components...
Kubectl is now configured to use the cluster.
Loading cached images from config file.
```
Great! You now have a running Kubernetes cluster in your online terminal. Minikube started a virtual machine for you, and a Kubernetes cluster is now running in that VM.

## Step 2 Cluster version

To interact with Kubernetes during this bootcamp we’ll use the command line interface, kubectl. We’ll explain kubectl in detail in the next modules, but for now, we’re just going to look at some cluster information. To check if kubectl is installed you can run the `kubectl version` command:
```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"11", GitVersion:"v1.11.0", GitCommit:"91e7b4fd31fcd3d5f436da26c980becec37ceefe", GitTreeState:"clean", BuildDate:"2018-06-27T20:17:28Z", GoVersion:"go1.10.2", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.0", GitCommit:"fc32d2f3698e36b93322a3465f63a14e9f0eaead", GitTreeState:"clean", BuildDate:"2018-04-10T12:46:31Z", GoVersion:"go1.9.4", Compiler:"gc", Platform:"linux/amd64"}
```
OK, kubectl is configured and we can see both the version of the client and as well as the server. The client version is the kubectl version; the server version is the Kubernetes version installed on the master. You can also see details about the build.

## Step 3 Cluster details

Let’s view the cluster details. We’ll do that by running `kubectl cluster-info`:
```
$ kubectl cluster-info
Kubernetes master is running at https://172.17.0.89:8443

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

We have a running master and a dashboard. The Kubernetes dashboard allows you to view your applications in a UI. During this tutorial, we’ll be focusing on the command line for deploying and exploring our application. To view the nodes in the cluster, run the `kubectl get nodes` command:
```
$ kubectl get nodes
NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     <none>    5m        v1.10.0
```
This command shows all nodes that can be used to host our applications. Now we have only one node, and we can see that ~~it’s~~ status is ready (it is ready to accept applications for deployment).


:couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple:


# Interactive Tutorial - Deploying an App (Module 2)

> 使用 kubectl 创建部署 https://kubernetes.io/zh/docs/tutorials/kubernetes-basics/deploy-intro/
>> Interactive Tutorial - Deploying an App https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-interactive/

## Step 1 kubectl basics

Like minikube, kubectl comes installed in the online terminal. Type kubectl in the terminal to see its usage. The common format of a kubectl command is: ***kubectl action resource***. This performs the specified action (like create, describe) on the specified resource (like node, container). You can use `--help` after the command to get additional info about possible parameters (`kubectl get nodes --help`).

Check that kubectl is configured to talk to your cluster, by running the `kubectl version` command:
```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"11", GitVersion:"v1.11.0", GitCommit:"91e7b4fd31fcd3d5f436da26c980becec37ceefe", GitTreeState:"clean", BuildDate:"2018-06-27T20:17:28Z", GoVersion:"go1.10.2", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.0", GitCommit:"fc32d2f3698e36b93322a3465f63a14e9f0eaead", GitTreeState:"clean", BuildDate:"2018-04-10T12:46:31Z", GoVersion:"go1.9.4", Compiler:"gc", Platform:"linux/amd64"}
```
OK, kubectl is installed and you can see both the client and the server versions.

To view the nodes in the cluster, run the `kubectl get nodes` command:
```
$ kubectl get nodes
NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     <none>    1m        v1.10.0
```
Here we see the available nodes (1 in our case). Kubernetes will choose where to deploy our application based on Node available resources.

## Step 2 Deploy our app

Let’s run our first app on Kubernetes with the `kubectl run` command. The `run` command creates a new deployment. We need to provide the deployment name and app image location (include the full repository url for images hosted outside Docker hub). We want to run the app on a specific port so we add the `--port` parameter:
```
$ kubectl run kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1 --port=8080
deployment.apps/kubernetes-bootcamp created
```
Great! You just deployed your first application by creating a deployment. This performed a few things for you:
- searched for a suitable node where an instance of the application could be run (we have only 1 available node)
- scheduled the application to run on that Node
- configured the cluster to reschedule the instance on a new Node when needed

To list your deployments use the `get deployments` command:
```
$ kubectl get deployments
NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   1         1         1            1           28m
```
We see that there is 1 deployment running a single instance of your app. The instance is running inside a Docker container on your node.

## Step 3 View our app

Pods that are running inside Kubernetes are running on a private, isolated network. By default they are visible from other pods and services within the same kubernetes cluster, but not outside that network. When we use `kubectl`, we're interacting through an API endpoint to communicate with our application.

We will cover other options on how to expose your application outside the kubernetes cluster in Module 4.

The `kubectl` command can create a proxy that will forward communications into the cluster-wide, private network. The proxy can be terminated by pressing control-C and won't show any output while its running.

We will open a second terminal window to run the proxy.
```
$ kubectl proxy
Starting to serve on 127.0.0.1:8001
```

We now have a connection between our host (the online terminal) and the Kubernetes cluster. The proxy enables direct access to the API from these terminals.

You can see all those APIs hosted through the proxy endpoint, now available at through http://localhost:8001. For example, we can query the version directly through the API using the `curl` command:
```
$ curl http://localhost:8001/version
{
  "major": "1",
  "minor": "10",
  "gitVersion": "v1.10.0",
  "gitCommit": "fc32d2f3698e36b93322a3465f63a14e9f0eaead",
  "gitTreeState": "clean",
  "buildDate": "2018-04-10T12:46:31Z",
  "goVersion": "go1.9.4",
  "compiler": "gc",
  "platform": "linux/amd64"
}
```

The API server will automatically create an endpoint for each pod, based on the pod name, that is also accessible through the proxy.

First we need to get the Pod name, and we'll store in the environment variable POD_NAME:
```
$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.mtadata.name}}{{"\n"}}{{end}}')
$ echo Name of the Pod: $POD_NAME
Name of the Pod: kubernetes-bootcamp-5c69669756-mwp4m
```

Now we can make an HTTP request to the application running in that pod:
```
$ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-mwp4m | v=1
```
The url is the route to the API of the Pod.

Note: Check the top of the terminal. The proxy was run in a new tab (Terminal 2), and the recent commands were executed the original tab (Terminal 1). The proxy still runs in the second tab, and this allowed our curl command to work using `localhost:8001`.


:couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple:


# Interactive Tutorial - Exploring Your App (Module 3)

> Viewing Pods and Nodes https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-intro/ --> 这个没中文版。。。我要不是记笔记都没发现。。。
>> Interactive Tutorial - Exploring Your App https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-interactive/
>>> 查看 Pods 和节点 https://kubernetes.io/zh/docs/tutorials/kubernetes-basics/explore-intro/ --> 额，后来发现不是没有，是顺序错了。中文版这个部分本来对应的互动教程里的Module 3，但是实际上它的位置都跑到“执行滚动更新”（也就是Module 6）后面了。

## Step 1 Check application configuration

Let’s verify that the application we deployed in the previous scenario is running. We’ll use the `kubectl get` command and look for existing Pods:
```
$ kubectl get pods
NAME                                   READY     STATUS    RESTARTS   AGE
kubernetes-bootcamp-5c69669756-bx2xq   1/1       Running   0          3m
```
If no pods are running, list the Pods again.

Next, to view what containers are inside that Pod and what images are used to build those containers we run the `describe pods` command:
```
$ kubectl describe pods
Name:           kubernetes-bootcamp-5c69669756-bx2xq
Namespace:      default
Node:           minikube/172.17.0.107
Start Time:     Mon, 18 Feb 2019 09:42:47 +0000
Labels:         pod-template-hash=1725225312
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.4
Controlled By:  ReplicaSet/kubernetes-bootcamp-5c69669756
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://1daee61d6ab8aa525173a0b66c6ea179c369fc2172da2939270f49954bd7e71f
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://gcr.io/google-samples/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Mon, 18 Feb 2019 09:42:51 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-v7z9s (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-v7z9s:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-v7z9s
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age              From               Message
  ----     ------                 ----             ----               -------
  Warning  FailedScheduling       6m (x3 over 6m)  default-scheduler  0/1 nodes are available: 1 node(s) were not ready.
  Normal   Scheduled              6m               default-scheduler  Successfully assigned kubernetes-bootcamp-5c69669756-bx2xq to minikube
  Normal   SuccessfulMountVolume  6m               kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-v7z9s"
  Normal   Pulled                 6m               kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created                6m               kubelet, minikube  Created container
  Normal   Started                6m               kubelet, minikube  Started container
```
We see here details about the Pod’s container: IP address, the ports used and a list of events related to the lifecycle of the Pod.

The output of the describe command is extensive and covers some concepts that we didn’t explain yet, but don’t worry, they will become familiar by the end of this bootcamp.

Note: the describe command can be used to get detailed information about most of the kubernetes primitives: node, pods, deployments. The describe output is designed to be human readable, not to be scripted against.

## Step 2 Show the app in the terminal

Recall that Pods are running in an isolated, private network - so we need to proxy access to them so we can debug and interact with them. To do this, we'll use the `kubectl proxy` command to run a proxy in a second terminal window. Click on the command below to automatically open a new terminal and run the `proxy`:
```
$ kubectl proxy
Starting to serve on 127.0.0.1:8001
```

Now again, we'll get the Pod name and query that pod directly through the proxy. To get the Pod name and store it in the POD_NAME environment variable:
```
$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
$ echo Name of the Pod: $POD_NAME
Name of the Pod: kubernetes-bootcamp-5c69669756-bx2xq
```

To see the output of our application, run a `curl` request.
```
$ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-bx2xq | v=1
```
The url is the route to the API of the Pod.

## Step 3 View the container logs

Anything that the application would normally send to `STDOUT` becomes logs for the container within the Pod. We can retrieve these logs using the `kubectl logs` command:
```
$ kubectl logs $POD_NAME
Kubernetes Bootcamp App Started At: 2019-02-18T09:42:51.375Z | Running On:  kubernetes-bootcamp-5c69669756-bx2xq

Running On: kubernetes-bootcamp-5c69669756-bx2xq | Total Requests: 1 | App Uptime: 707.204 seconds | Log Time: 2019-02-18T09:54:38.579Z
```
Note: We don’t need to specify the container name, because we only have one container inside the pod.

## Step 4 Executing command on the container

We can execute commands directly on the container once the Pod is up and running. For this, we use the `exec` command and use the name of the Pod as a parameter. Let’s list the environment variables:
```
$ kubectl exec $POD_NAME env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=kubernetes-bootcamp-5c69669756-bx2xq
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
KUBERNETES_SERVICE_HOST=10.96.0.1
NPM_CONFIG_LOGLEVEL=info
NODE_VERSION=6.3.1
HOME=/root
```

Again, worth mentioning that the name of the container itself can be omitted since we only have a single container in the Pod.

Next let’s start a bash session in the Pod’s container:
```
$ kubectl exec -ti $POD_NAME bash
root@kubernetes-bootcamp-5c69669756-bx2xq:/#
```

We have now an open console on the container where we run our NodeJS application. The source code of the app is in the server.js file:
```
root@kubernetes-bootcamp-5c69669756-bx2xq:/# cat server.js
var http = require('http');
var requests=0;
var podname= process.env.HOSTNAME;
var startTime;
var host;
var handleRequest = function(request, response) {
  response.setHeader('Content-Type', 'text/plain');
  response.writeHead(200);
  response.write("Hello Kubernetes bootcamp! | Running on: ");
  response.write(host);
  response.end(" | v=1\n");
  console.log("Running On:" ,host, "| Total Requests:", ++requests,"| App Uptime:", (new Date() - startTime)/1000 , "seconds", "| Log Time:",new Date());
}
var www = http.createServer(handleRequest);
www.listen(8080,function () {
    startTime = new Date();;
    host = process.env.HOSTNAME;
    console.log ("Kubernetes Bootcamp App Started At:",startTime, "| Running On: " ,host, "\n" );
});
```

You can check that the application is up by running a curl command:
```
root@kubernetes-bootcamp-5c69669756-bx2xq:/# curl localhost:8080
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-bx2xq | v=1
```
Note: here we used localhost because we executed the command inside the NodeJS container

To close your container connection type
```
root@kubernetes-bootcamp-5c69669756-bx2xq:/# exit
exit
``` 


:couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple:


# Interactive Tutorial - Exposing Your App (Module 4)

> 使用服务发布您的应用程序 https://kubernetes.io/zh/docs/tutorials/kubernetes-basics/expose-intro/
>> Interactive Tutorial - Exposing Your App https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-interactive/

## Step 1 Create a new service

Let’s verify that our application is running. We’ll use the `kubectl get` command and look for existing Pods:
```
$ kubectl get pods
NAME                                   READY     STATUS    RESTARTS   AGE
kubernetes-bootcamp-5c69669756-88fkn   0/1       Pending   0          3s
```

Next let’s list the current Services from our cluster:
```
$ kubectl get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   1m
```

We have a Service called kubernetes that is created by default when minikube starts the cluster. To create a new service and expose it to external traffic we’ll use the ***expose*** command with NodePort as parameter (minikube does not support the LoadBalancer option yet).
```
$ kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
service/kubernetes-bootcamp exposed
```

Let’s run again the `get services` command:
```
$ kubectl get services
NAME                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes            ClusterIP   10.96.0.1       <none>        443/TCP          3m
kubernetes-bootcamp   NodePort    10.99.111.170   <none>        8080:31149/TCP   30s
```
We have now a running Service called kubernetes-bootcamp. Here we see that the Service received a unique cluster-IP, an internal port and an external-IP (the IP of the Node).

To find out what port was opened externally (by the NodePort option) we’ll run the `describe service` command:
```
$ kubectl describe services/kubernetes-bootcamp
Name:                     kubernetes-bootcamp
Namespace:                default
Labels:                   run=kubernetes-bootcamp
Annotations:              <none>
Selector:                 run=kubernetes-bootcamp
Type:                     NodePort
IP:                       10.99.111.170
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  31149/TCP
Endpoints:                172.18.0.4:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

Create an environment variable called NODE_PORT that has the value of the Node port assigned:
```
$ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
$ echo NODE_PORT=$NODE_PORT
NODE_PORT=31149
```

Now we can test that the app is exposed outside of the cluster using `curl`, the IP of the Node and the externally exposed port:
```
$ curl $(minikube ip):$NODE_PORT
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-88fkn | v=1
```
And we get a response from the server. The Service is exposed.

## Step 2: Using labels

The Deployment created automatically a label for our Pod. With `describe deployment` command you can see the name of the label:
```
$ kubectl describe deployment
Name:                   kubernetes-bootcamp
Namespace:              default
CreationTimestamp:      Mon, 18 Feb 2019 11:03:00 +0000
Labels:                 run=kubernetes-bootcamp
Annotations:            deployment.kubernetes.io/revision=1
Selector:               run=kubernetes-bootcamp
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  run=kubernetes-bootcamp
  Containers:
   kubernetes-bootcamp:
    Image:        gcr.io/google-samples/kubernetes-bootcamp:v1
    Port:         8080/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   kubernetes-bootcamp-5c69669756 (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  7m    deployment-controller  Scaled up replica set kubernetes-bootcamp-5c69669756 to 1
```

Let’s use this label to query our list of Pods. We’ll use the `kubectl get pods` command with -l as a parameter, followed by the label values:
```
$ kubectl get pods -l run=kubernetes-bootcamp
NAME                                   READY     STATUS    RESTARTS   AGE
kubernetes-bootcamp-5c69669756-88fkn   1/1       Running   0          9m
```

You can do the same to list the existing services:
```
$ kubectl get services -l run=kubernetes-bootcamp
NAME                  TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes-bootcamp   NodePort   10.99.111.170   <none>        8080:31149/TCP   7m
```

Get the name of the Pod and store it in the POD_NAME environment variable:
```
$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
$ echo Name of the Pod: $POD_NAME
Name of the Pod: kubernetes-bootcamp-5c69669756-88fkn
```

To apply a new label we use the ***label*** command followed by the object type, object name and the new label:
```
$ kubectl label pod $POD_NAME app=v1
pod/kubernetes-bootcamp-5c69669756-88fkn labeled
```

This will apply a new label to our Pod (we pinned the application version to the Pod), and we can check it with the describe pod command:
```
$ kubectl describe pods $POD_NAME
Name:           kubernetes-bootcamp-5c69669756-88fkn
Namespace:      default
Node:           minikube/172.17.0.162
Start Time:     Mon, 18 Feb 2019 11:03:07 +0000
Labels:         app=v1
                pod-template-hash=1725225312
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.4
Controlled By:  ReplicaSet/kubernetes-bootcamp-5c69669756
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://6c46d3e81fc5ce18248036e41a6b91220bcbea21210eab04f9eab6ac1874b867
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://gcr.io/google-samples/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Mon, 18 Feb 2019 11:03:09 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-ksmcb (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-ksmcb:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-ksmcb
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age                From               Message
  ----     ------                 ----               ----               -------
  Warning  FailedScheduling       12m (x4 over 12m)  default-scheduler  0/1 nodes are available: 1 node(s) were not ready.
  Normal   Scheduled              12m                default-scheduler  Successfullyassigned kubernetes-bootcamp-5c69669756-88fkn to minikube
  Normal   SuccessfulMountVolume  12m                kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-ksmcb"
  Normal   Pulled                 12m                kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created                12m                kubelet, minikube  Created container
  Normal   Started                12m                kubelet, minikube  Started container
```

We see here that the label is attached now to our Pod. And we can query now the list of pods using the new label:
```
$ kubectl get pods -l app=v1
NAME                                   READY     STATUS    RESTARTS   AGE
kubernetes-bootcamp-5c69669756-88fkn   1/1       Running   0          14m
```
And we see the Pod.

## Step 3 Deleting a service

To delete Services you can use the `delete service` command. Labels can be used also here:
```
$ kubectl delete service -l run=kubernetes-bootcamp
service "kubernetes-bootcamp" deleted
```

Confirm that the service is gone:
```
$ kubectl get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   17m
```

This confirms that our Service was removed. To confirm that route is not exposed anymore you can `curl` the previously exposed IP and port:
```
$ curl $(minikube ip):$NODE_PORT
curl: (7) Failed to connect to 172.17.0.162 port 31149: Connection refused
```

This proves that the app is not reachable anymore from outside of the cluster. You can confirm that the app is still running with a curl inside the pod:
```
$ kubectl exec -ti $POD_NAME curl localhost:8080
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-88fkn | v=1
```
We see here that the application is up.


:couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple:


# Interactive Tutorial - Scaling Your App (Module 5)

> 运行应用程序的多个实例 https://kubernetes.io/zh/docs/tutorials/kubernetes-basics/scale-intro/
>> Interactive Tutorial - Scaling Your App https://kubernetes.io/docs/tutorials/kubernetes-basics/scale/scale-interactive/

## Step 1: Scaling a deployment

To list your deployments use the `get deployments` command: 
```
$ kubectl get deployments
NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   1         1         1            1           4m
```

We should have 1 Pod. If not, run the command again. This shows:

- The DESIRED state is showing the configured number of replicas
- The CURRENT state show how many replicas are running now
- The UP-TO-DATE is the number of replicas that were updated to match the desired (configured) state
- The AVAILABLE state shows how many replicas are actually AVAILABLE to the users

Next, let’s scale the Deployment to 4 replicas. We’ll use the `kubectl scale` command, followed by the deployment type, name and desired number of instances:
```
$ kubectl scale deployments/kubernetes-bootcamp --replicas=4
deployment.extensions/kubernetes-bootcamp scaled
```

To list your Deployments once again, use `get deployments`:
```
$ kubectl get deployments
NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   4         4         4            4           7m
```

The change was applied, and we have 4 instances of the application available. Next, let’s check if the number of Pods changed:
```
$ kubectl get pods -o wide
NAME                                   READY     STATUS    RESTARTS   AGE       IP        NODE
kubernetes-bootcamp-5c69669756-9jzgb   1/1       Running   0          8m        172.18.0.4   minikube
kubernetes-bootcamp-5c69669756-9k7fm   1/1       Running   0          2m        172.18.0.6   minikube
kubernetes-bootcamp-5c69669756-vm4xk   1/1       Running   0          2m        172.18.0.7   minikube
kubernetes-bootcamp-5c69669756-zckl4   1/1       Running   0          2m        172.18.0.5   minikube
```

There are 4 Pods now, with different IP addresses. The change was registered in the Deployment events log. To check that, use the describe command:
```
$ kubectl describe deployments/kubernetes-bootcamp
Name:                   kubernetes-bootcamp
Namespace:              default
CreationTimestamp:      Tue, 19 Feb 2019 10:45:46 +0000
Labels:                 run=kubernetes-bootcamp
Annotations:            deployment.kubernetes.io/revision=1
Selector:               run=kubernetes-bootcamp
Replicas:               4 desired | 4 updated | 4 total | 4 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  run=kubernetes-bootcamp
  Containers:
   kubernetes-bootcamp:
    Image:        gcr.io/google-samples/kubernetes-bootcamp:v1
    Port:         8080/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Progressing    True    NewReplicaSetAvailable
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   kubernetes-bootcamp-5c69669756 (4/4 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  10m   deployment-controller  Scaled up replica set kubernetes-bootcamp-5c69669756 to 1
  Normal  ScalingReplicaSet  4m    deployment-controller  Scaled up replica set kubernetes-bootcamp-5c69669756 to 4
```
You can also view in the output of this command that there are 4 replicas now.

## Step 2: Load Balancing

Let’s check that the Service is load-balancing the traffic. To find out the exposed IP and Port we can use the describe service as we learned in the previously Module:
```
$ kubectl describe services/kubernetes-bootcamp
Name:                     kubernetes-bootcamp
Namespace:                default
Labels:                   run=kubernetes-bootcamp
Annotations:              <none>
Selector:                 run=kubernetes-bootcamp
Type:                     NodePort
IP:                       10.109.160.47
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  32623/TCP
Endpoints:                172.18.0.4:8080,172.18.0.5:8080,172.18.0.6:8080 + 1 more...
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

Create an environment variable called NODE_PORT that has a value as the Node port:
```
$ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
$ echo NODE_PORT=$NODE_PORT
NODE_PORT=32623
```

Next, we’ll do a `curl` to the exposed IP and port. Execute the command multiple times:
```
$ curl $(minikube ip):$NODE_PORT
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-5c69669756-zckl4 | v=1
```
We hit a different Pod with every request. This demonstrates that the load-balancing is working.

## Step 3: Scale Down

To scale down the Service to 2 replicas, run again the `scale` command:
```
$ kubectl scale deployments/kubernetes-bootcamp --replicas=2
deployment.extensions/kubernetes-bootcamp scaled
```

List the Deployments to check if the change was applied with the `get deployments` command:
```
$ kubectl get deployments
NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   2         2         2            2           15m
```

The number of replicas decreased to 2. List the number of Pods, with `get pods`:
```
$ kubectl get pods -o wide
NAME                                   READY     STATUS    RESTARTS   AGE       IP        NODE
kubernetes-bootcamp-5c69669756-9jzgb   1/1       Running   0          16m       172.18.0.4   minikube
kubernetes-bootcamp-5c69669756-zckl4   1/1       Running   0          10m       172.18.0.5   minikube
```
This confirms that 2 Pods were terminated.


:couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple::couple:


# Interactive Tutorial - Updating Your App (Module 6)

> 执行滚动更新 https://kubernetes.io/zh/docs/tutorials/kubernetes-basics/update-intro/
>> Interactive Tutorial - Updating Your App https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-interactive/

## Step 1: Update the version of the app

To list your deployments use the `get deployments` command:
```
$ kubectl get deployments
NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   4         4         4            4           1m
```

To list the running Pods use the `get pods` command:
```
$ kubectl get pods
NAME                                   READY     STATUS    RESTARTS   AGE
kubernetes-bootcamp-5c69669756-bf5jx   1/1       Running   0          1m
kubernetes-bootcamp-5c69669756-lgqw2   1/1       Running   0          1m
kubernetes-bootcamp-5c69669756-n9k2g   1/1       Running   0          1m
kubernetes-bootcamp-5c69669756-psgxf   1/1       Running   0          1m
```

To view the current image version of the app, run a `describe` command against the Pods (look at the Image field):
```
$ kubectl describe pods
Name:           kubernetes-bootcamp-5c69669756-bf5jx
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:11:11 +0000
Labels:         pod-template-hash=1725225312
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.4
Controlled By:  ReplicaSet/kubernetes-bootcamp-5c69669756
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://36d77baddc817473e2895dcc47945a4c689415340a16d62543ffc518ceee1264
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://gcr.io/google-samples/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:11:14 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age              From               Message
  ----     ------                 ----             ----               -------
  Warning  FailedScheduling       1m (x5 over 2m)  default-scheduler  0/1 nodes are available: 1 node(s) were not ready.
  Normal   Scheduled              1m               default-scheduler  Successfully assigned kubernetes-bootcamp-5c69669756-bf5jx to minikube
  Normal   SuccessfulMountVolume  1m               kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal   Pulled                 1m               kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created                1m               kubelet, minikube  Created container
  Normal   Started                1m               kubelet, minikube  Started container


Name:           kubernetes-bootcamp-5c69669756-lgqw2
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:11:11 +0000
Labels:         pod-template-hash=1725225312
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.5
Controlled By:  ReplicaSet/kubernetes-bootcamp-5c69669756
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://339626a9270a595206cd1bca86ce9a3043578254a428a222f687ce8b6f671a63
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://gcr.io/google-samples/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:11:13 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age              From               Message
  ----     ------                 ----             ----               -------
  Warning  FailedScheduling       1m (x5 over 2m)  default-scheduler  0/1 nodes are available: 1 node(s) were not ready.
  Normal   Scheduled              1m               default-scheduler  Successfully assigned kubernetes-bootcamp-5c69669756-lgqw2 to minikube
  Normal   SuccessfulMountVolume  1m               kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal   Pulled                 1m               kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created                1m               kubelet, minikube  Created container
  Normal   Started                1m               kubelet, minikube  Started container


Name:           kubernetes-bootcamp-5c69669756-n9k2g
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:11:11 +0000
Labels:         pod-template-hash=1725225312
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.7
Controlled By:  ReplicaSet/kubernetes-bootcamp-5c69669756
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://81ef67f111f99662e20c8caf3b266b25c0453ba44b0ba577c11ea60181ef2d48
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://gcr.io/google-samples/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:11:14 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age              From               Message
  ----     ------                 ----             ----               -------
  Warning  FailedScheduling       1m (x5 over 2m)  default-scheduler  0/1 nodes are available: 1 node(s) were not ready.
  Normal   Scheduled              1m               default-scheduler  Successfully assigned kubernetes-bootcamp-5c69669756-n9k2g to minikube
  Normal   SuccessfulMountVolume  1m               kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal   Pulled                 1m               kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created                1m               kubelet, minikube  Created container
  Normal   Started                1m               kubelet, minikube  Started container


Name:           kubernetes-bootcamp-5c69669756-psgxf
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:11:11 +0000
Labels:         pod-template-hash=1725225312
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.6
Controlled By:  ReplicaSet/kubernetes-bootcamp-5c69669756
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://aae5e1c2ee67f73a83d2993f7f4df3256c8babb7f8a4073d6bd287b765d3676f
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://gcr.io/google-samples/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:11:14 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age              From               Message
  ----     ------                 ----             ----               -------
  Warning  FailedScheduling       1m (x5 over 2m)  default-scheduler  0/1 nodes are available: 1 node(s) were not ready.
  Normal   Scheduled              1m               default-scheduler  Successfully assigned kubernetes-bootcamp-5c69669756-psgxf to minikube
  Normal   SuccessfulMountVolume  1m               kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal   Pulled                 1m               kubelet, minikube  Container image "gcr.io/google-samples/kubernetes-bootcamp:v1" already present on machine
  Normal   Created                1m               kubelet, minikube  Created container
  Normal   Started                1m               kubelet, minikube  Started container
```

To update the image of the application to version 2, use the `set image` command, followed by the deployment name and the new image version:
```
$ kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
deployment.extensions/kubernetes-bootcamp image updated
```

The command notified the Deployment to use a different image for your app and initiated a rolling update. Check the status of the new Pods, and view the old one terminating with the `get pods` command:
```
$ kubectl get pods
NAME                                   READY     STATUS    RESTARTS   AGE
kubernetes-bootcamp-7799cbcb86-4r2sv   1/1       Running   0          50s
kubernetes-bootcamp-7799cbcb86-n45v5   1/1       Running   0          49s
kubernetes-bootcamp-7799cbcb86-rr424   1/1       Running   0          48s
kubernetes-bootcamp-7799cbcb86-z5h29   1/1       Running   0          51s
```

## Step 2: Verify an update

First, let’s check that the App is running. To find out the exposed IP and Port we can use `describe service`:
```
$ kubectl describe services/kubernetes-bootcamp
Name:                     kubernetes-bootcamp
Namespace:                default
Labels:                   run=kubernetes-bootcamp
Annotations:              <none>
Selector:                 run=kubernetes-bootcamp
Type:                     NodePort
IP:                       10.100.142.117
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  32543/TCP
Endpoints:                172.18.0.10:8080,172.18.0.11:8080,172.18.0.8:8080 + 1 more...
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

Create an environment variable called NODE_PORT that has the value of the Node port assigned:
```
$ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')
$ echo NODE_PORT=$NODE_PORT
NODE_PORT=32543
```

Next, we’ll do a `curl` to the the exposed IP and port:
```
$ curl $(minikube ip):$NODE_PORT
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7799cbcb86-n45v5 | v=2
```

We hit a different Pod with every request and we see that all Pods are running the latest version (v2).

The update can be confirmed also by running a rollout status command:
```
$ kubectl rollout status deployments/kubernetes-bootcamp
deployment "kubernetes-bootcamp" successfully rolled out
```

To view the current image version of the app, run a describe command against the Pods:
```
$ kubectl describe pods
Name:           kubernetes-bootcamp-7799cbcb86-4r2sv
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:45 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.9
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://1f92a6c8805285652737946f689d4b7b1339eae0129a760fc91c6e42b8b45f0f
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:46 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              4m    default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-4r2sv to minikube
  Normal  SuccessfulMountVolume  4m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 4m    kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                4m    kubelet, minikube  Created container
  Normal  Started                4m    kubelet, minikube  Started container


Name:           kubernetes-bootcamp-7799cbcb86-n45v5
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:46 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.10
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://00794a87b7f33b1aa37d51526c20ea596bf1f8e2091b8d116ee3120373194e3e
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:47 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              4m    default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-n45v5 to minikube
  Normal  SuccessfulMountVolume  4m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 4m    kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                4m    kubelet, minikube  Created container
  Normal  Started                4m    kubelet, minikube  Started container


Name:           kubernetes-bootcamp-7799cbcb86-rr424
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:47 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.11
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://ce8b147733f9127cee6456643c9de664d29eb3a4e3b56b18d59261a1ba0c8667
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:48 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              4m    default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-rr424 to minikube
  Normal  SuccessfulMountVolume  4m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 4m    kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                4m    kubelet, minikube  Created container
  Normal  Started                4m    kubelet, minikube  Started container


Name:           kubernetes-bootcamp-7799cbcb86-z5h29
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:45 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.8
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://47c0633a189ad12a2f39b912ae8fad68de3819aa032bda6b156533e0c6c5b05c
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:46 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              4m    default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-z5h29 to minikube
  Normal  SuccessfulMountVolume  4m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 4m    kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                4m    kubelet, minikube  Created container
  Normal  Started                4m    kubelet, minikube  Started container
```
We run now version 2 of the app (look at the Image field)

## Step 3: Rollback an update

Let’s perform another update, and deploy image tagged as `v10`:
```
$ kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=gcr.io/google-samples/kubernetes-bootcamp:v10
deployment.extensions/kubernetes-bootcamp image updated
```

Use `get deployments` to see the status of the deployment:
```
$ kubectl get deployments
NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   4         5         2            3           10m
```

And something is wrong… We do not have the desired number of Pods available. List the Pods again:
```
$ kubectl get pods
NAME                                   READY     STATUS             RESTARTS   AGE
kubernetes-bootcamp-5f76cd7b94-qsp6x   0/1       ImagePullBackOff   0          1m
kubernetes-bootcamp-5f76cd7b94-xch4w   0/1       ImagePullBackOff   0          1m
kubernetes-bootcamp-7799cbcb86-4r2sv   1/1       Running            0          7m
kubernetes-bootcamp-7799cbcb86-n45v5   1/1       Running            0          7m
kubernetes-bootcamp-7799cbcb86-z5h29   1/1       Running            0          7m
```

A `describe` command on the Pods should give more insights:
```
$ kubectl describe pods
Name:           kubernetes-bootcamp-5f76cd7b94-qsp6x
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:20:37 +0000
Labels:         pod-template-hash=1932783650
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Pending
IP:             172.18.0.4
Controlled By:  ReplicaSet/kubernetes-bootcamp-5f76cd7b94
Containers:
  kubernetes-bootcamp:
    Container ID:
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v10
    Image ID:
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          False
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age               From               Message
  ----     ------                 ----              ----               -------
  Normal   Scheduled              2m                default-scheduler  Successfully assigned kubernetes-bootcamp-5f76cd7b94-qsp6x to minikube
  Normal   SuccessfulMountVolume  2m                kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal   Pulling                1m (x4 over 2m)   kubelet, minikube  pulling image"gcr.io/google-samples/kubernetes-bootcamp:v10"
  Warning  Failed                 1m (x4 over 2m)   kubelet, minikube  Failed to pull image "gcr.io/google-samples/kubernetes-bootcamp:v10": rpc error: code = Unknown desc = unauthorized: authentication required
  Warning  Failed                 1m (x4 over 2m)   kubelet, minikube  Error: ErrImagePull
  Normal   BackOff                47s (x6 over 2m)  kubelet, minikube  Back-off pulling image "gcr.io/google-samples/kubernetes-bootcamp:v10"
  Warning  Failed                 47s (x6 over 2m)  kubelet, minikube  Error: ImagePullBackOff


Name:           kubernetes-bootcamp-5f76cd7b94-xch4w
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:20:37 +0000
Labels:         pod-template-hash=1932783650
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Pending
IP:             172.18.0.5
Controlled By:  ReplicaSet/kubernetes-bootcamp-5f76cd7b94
Containers:
  kubernetes-bootcamp:
    Container ID:
    Image:          gcr.io/google-samples/kubernetes-bootcamp:v10
    Image ID:
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          False
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age               From               Message
  ----     ------                 ----              ----               -------
  Normal   Scheduled              2m                default-scheduler  Successfully assigned kubernetes-bootcamp-5f76cd7b94-xch4w to minikube
  Normal   SuccessfulMountVolume  2m                kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal   Pulling                1m (x4 over 2m)   kubelet, minikube  pulling image"gcr.io/google-samples/kubernetes-bootcamp:v10"
  Warning  Failed                 1m (x4 over 2m)   kubelet, minikube  Failed to pull image "gcr.io/google-samples/kubernetes-bootcamp:v10": rpc error: code = Unknown desc = unauthorized: authentication required
  Warning  Failed                 1m (x4 over 2m)   kubelet, minikube  Error: ErrImagePull
  Normal   BackOff                40s (x6 over 2m)  kubelet, minikube  Back-off pulling image "gcr.io/google-samples/kubernetes-bootcamp:v10"
  Warning  Failed                 40s (x6 over 2m)  kubelet, minikube  Error: ImagePullBackOff


Name:           kubernetes-bootcamp-7799cbcb86-4r2sv
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:45 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.9
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://1f92a6c8805285652737946f689d4b7b1339eae0129a760fc91c6e42b8b45f0f
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:46 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              8m    default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-4r2sv to minikube
  Normal  SuccessfulMountVolume  8m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 8m    kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                8m    kubelet, minikube  Created container
  Normal  Started                8m    kubelet, minikube  Started container


Name:           kubernetes-bootcamp-7799cbcb86-n45v5
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:46 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.10
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://00794a87b7f33b1aa37d51526c20ea596bf1f8e2091b8d116ee3120373194e3e
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:47 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              8m    default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-n45v5 to minikube
  Normal  SuccessfulMountVolume  8m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 8m    kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                8m    kubelet, minikube  Created container
  Normal  Started                8m    kubelet, minikube  Started container


Name:           kubernetes-bootcamp-7799cbcb86-z5h29
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:45 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.8
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://47c0633a189ad12a2f39b912ae8fad68de3819aa032bda6b156533e0c6c5b05c
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:46 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              8m    default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-z5h29 to minikube
  Normal  SuccessfulMountVolume  8m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 8m    kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                8m    kubelet, minikube  Created container
  Normal  Started                8m    kubelet, minikube  Started container
```

There is no image called `v10` in the repository. Let’s roll back to our previously working version. We’ll use the `rollout` undo command:
```
$ kubectl rollout undo deployments/kubernetes-bootcamp
deployment.extensions/kubernetes-bootcamp
```

The `rollout` command reverted the deployment to the previous known state (v2 of the image). Updates are versioned and you can revert to any previously know state of a Deployment. List again the Pods:
```
$ kubectl get pods
NAME                                   READY     STATUS    RESTARTS   AGE
kubernetes-bootcamp-7799cbcb86-4r2sv   1/1       Running   0          11m
kubernetes-bootcamp-7799cbcb86-n45v5   1/1       Running   0          11m
kubernetes-bootcamp-7799cbcb86-pw7fw   1/1       Running   0          49s
kubernetes-bootcamp-7799cbcb86-z5h29   1/1       Running   0          11m
```

Four Pods are running. Check again the image deployed on the them:
```
$ kubectl describe pods
Name:           kubernetes-bootcamp-7799cbcb86-4r2sv
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:45 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.9
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://1f92a6c8805285652737946f689d4b7b1339eae0129a760fc91c6e42b8b45f0f
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:46 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              11m   default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-4r2sv to minikube
  Normal  SuccessfulMountVolume  11m   kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 11m   kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                11m   kubelet, minikube  Created container
  Normal  Started                11m   kubelet, minikube  Started container


Name:           kubernetes-bootcamp-7799cbcb86-n45v5
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:46 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.10
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://00794a87b7f33b1aa37d51526c20ea596bf1f8e2091b8d116ee3120373194e3e
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:47 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              11m   default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-n45v5 to minikube
  Normal  SuccessfulMountVolume  11m   kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 11m   kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                11m   kubelet, minikube  Created container
  Normal  Started                11m   kubelet, minikube  Started container


Name:           kubernetes-bootcamp-7799cbcb86-pw7fw
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:25:03 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.6
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://c8318d41bd2c52237d43cb471bc9ba4eca8009cd5f51216fbeb3bc2f32506931
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:25:03 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              1m    default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-pw7fw to minikube
  Normal  SuccessfulMountVolume  1m    kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 1m    kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                1m    kubelet, minikube  Created container
  Normal  Started                1m    kubelet, minikube  Started container


Name:           kubernetes-bootcamp-7799cbcb86-z5h29
Namespace:      default
Node:           minikube/172.17.0.27
Start Time:     Tue, 19 Feb 2019 11:14:45 +0000
Labels:         pod-template-hash=3355767642
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             172.18.0.8
Controlled By:  ReplicaSet/kubernetes-bootcamp-7799cbcb86
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://47c0633a189ad12a2f39b912ae8fad68de3819aa032bda6b156533e0c6c5b05c
    Image:          jocatalin/kubernetes-bootcamp:v2
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 19 Feb 2019 11:14:46 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hxjgm (ro)
Conditions:
  Type           Status
  Initialized    True
  Ready          True
  PodScheduled   True
Volumes:
  default-token-hxjgm:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hxjgm
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason                 Age   From               Message
  ----    ------                 ----  ----               -------
  Normal  Scheduled              11m   default-scheduler  Successfully assigned kubernetes-bootcamp-7799cbcb86-z5h29 to minikube
  Normal  SuccessfulMountVolume  11m   kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-hxjgm"
  Normal  Pulled                 11m   kubelet, minikube  Container image "jocatalin/kubernetes-bootcamp:v2" already present on machine
  Normal  Created                11m   kubelet, minikube  Created container
  Normal  Started                11m   kubelet, minikube  Started container
```
We see that the deployment is using a stable version of the app (v2). The Rollback was successful.

