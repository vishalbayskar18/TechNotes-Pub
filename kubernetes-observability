
# Readiyness Probes

> The pod have the status and some condition

<img width="757" alt="image" src="https://user-images.githubusercontent.com/45871181/235298485-f5c69a7a-af33-44f8-b36c-1c77915daea5.png">


<img width="998" alt="image" src="https://user-images.githubusercontent.com/45871181/235298543-b475c46e-be78-48d2-b083-d7fb9ef32c42.png">

> When pod first created it's in the pending state, at this time schedule tries to schedule the pod, if scheduler not able to schedule the pod on some node, pod remains in the peding state.
> In order to understand why it is in the pending state, run pod describe command and it will tell you why

<img width="989" alt="image" src="https://user-images.githubusercontent.com/45871181/235298598-0300a160-55f7-4666-8253-2c751c65c19a.png">

<img width="1071" alt="image" src="https://user-images.githubusercontent.com/45871181/235298631-53894114-e96d-4608-80dd-bdfdac105398.png">


> Once the pod is scheduled it goes into container creating state, where the images required for the application are pulled and container starts.

<img width="1079" alt="image" src="https://user-images.githubusercontent.com/45871181/235298673-0b0e8086-b1d7-467b-a2de-f146cdfd3579.png">


> Once all the containers in the pod starts it goes into a running state, where it runs continuously untill the program completed successfully or terminated.
> 

> Pod status can be found using `kubectl get pod` command, pod can be any of these 3 states, Pending, ContainerCreating and Running.

<img width="1096" alt="image" src="https://user-images.githubusercontent.com/45871181/235298732-fb2d6c11-9fe9-4d99-93b3-18f604e99803.png">

> Now comes the condition which gives the clear picture.


<img width="804" alt="image" src="https://user-images.githubusercontent.com/45871181/235298832-f3e3d364-d171-4215-b386-c9ce6ee9790e.png">



> When pod scheduled on the node, PodScheduled is set to true.
> When pod initialized it's value set to true.
> When all the container in the pods are ready ContainerReady set to true.
> And finally pod itself is considered to be ready.


> Conditions can be checked with pod describe command, there is section called Conditions.

<img width="1024" alt="image" src="https://user-images.githubusercontent.com/45871181/235298863-100d2070-0258-4265-8502-fb529e9cee5f.png">

> In get pod command also we see the ready column, it means application running inside the pod is ready and can take the request.

<img width="865" alt="image" src="https://user-images.githubusercontent.com/45871181/235298907-c5b070a1-e8b7-4b0a-ad4a-dda1f93b4ddb.png">

> There may be different application running on the pod e.g. a script, a DB, an web service, and each may take different time e.g. script can be ready in millisecond where web service may take few seconds.

> If you run jenkins server it takes 10-15 seconds and it's web site again take few more seconds to be ready to take the new request.

<img width="825" alt="image" src="https://user-images.githubusercontent.com/45871181/235299325-127a093b-2356-4468-ba5e-fbc7ab3fe920.png">

> And If you see the status of the pod, it will show ready which is not actually true.


> Why it is an issue because service relay on the ready condition of the pod to forward the request, and by default when containers are running inside pod, k8 makes the pods condition to ready.

<img width="411" alt="image" src="https://user-images.githubusercontent.com/45871181/235299412-5c0fa811-13ce-4a83-a930-eabd80b93ab1.png">

> And if application inside pods take longer time to be ready, service will be unware and will send the request to pod, which will fail.
> We need to tie the ready condition to the application actually condition, and as developer of application we know better when the application can take the request.
> 

**There are different ways you can define the readyness checks**

> In case of a web application, it could be when web api server is ready to take the request, for this we can have http test to see the api response. 

<img width="623" alt="image" src="https://user-images.githubusercontent.com/45871181/235299655-108d11e7-f510-47f2-9e63-e22f95b3adb2.png">

<img width="989" alt="image" src="https://user-images.githubusercontent.com/45871181/235299707-bc907e2b-6eca-4251-8ed4-f9af3eaf06f0.png">

> For DB you can check if particular tcp port is listening, or you can exeucte any custom command that will run succesfully if the application is running.

**How to configure the test**

> In the pod definition file add a new field called readinessProbe, 
> And use the httpGet, specifiy the url and port 

<img width="1047" alt="image" src="https://user-images.githubusercontent.com/45871181/235299790-fa909777-d5fd-4ad0-be02-85c410d48ed4.png">

> Now kubernetes does not immediately set the ready condition on the container to true instead it performs a test if the API response is posivite or not, untill then service does not forward the request to pod as it sees pod is not ready.


<img width="1053" alt="image" src="https://user-images.githubusercontent.com/45871181/235299879-c7c232e6-4605-4170-87f0-eac21b04e83b.png">

> Different types of readiness probe can be set, for http use httpget, for tcp, use tcpSocket and command use exec and provide command and option in array.


<img width="1045" alt="image" src="https://user-images.githubusercontent.com/45871181/235299958-452945ba-f36f-4d92-99fb-e74d3145d936.png">

> In case your application takes more time to warm up, you can add additional delay, using initialDelaySeconds and specify how offen it should be checked/probed by default in 3 times it does not gets ready, the probe will be stopped, if you want more attempt you can mentioned using failureThreadshold.

> Now let's see how it can make issue in case of multiple replica of pod.

<img width="741" alt="image" src="https://user-images.githubusercontent.com/45871181/235300068-6b7ab033-a3ff-412f-bce4-57885d97a292.png">

<img width="701" alt="image" src="https://user-images.githubusercontent.com/45871181/235300025-0f9b5881-8001-4737-a098-23578a263f20.png">

> Suppose you have 2 pods running and taking the request and in case you add one more and in case you don't have the readiness, your new pod will be considered to ready and service will start sending the request to new pod and it will fail. 

