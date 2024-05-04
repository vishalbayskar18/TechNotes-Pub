# Node Affinity

> The purponse of node affinity is to ensure that particular pod is scheduled on particular node.
> E.g. in this case we want Large pod (e.g. image processing application) get scheduled on Large node.


<img width="343" alt="image" src="https://user-images.githubusercontent.com/45871181/235296428-417eea06-dd48-4d56-8c92-49ad1352126e.png">

> This is how it changes from NodeSelector to NodeAffinity, with high power comes high responsiblity.


<img width="910" alt="image" src="https://user-images.githubusercontent.com/45871181/235296463-1c7284fe-c38d-4dce-8628-4419649ce8b4.png">

> If you want Large or Medium you can add one more value.

<img width="631" alt="image" src="https://user-images.githubusercontent.com/45871181/235296519-167b08e9-cb43-4f36-8d59-351884121431.png">

> Or if you don't want POD to go to small Node, can be done like below.

<img width="584" alt="image" src="https://user-images.githubusercontent.com/45871181/235296537-5dcbbc28-f723-4fb5-9474-48a92fd05c40.png">

> Or if you want to schedule on which label exist 

<img width="601" alt="image" src="https://user-images.githubusercontent.com/45871181/235296576-04f6d48c-21df-4374-a5d7-be793a749882.png">

**What if there are no nodes available with affinity mentioned in the pod**

> E.g. in case somebody change the label on the node, will the pod continues to run on the node?
> It will be decided based on the property mentioned.

> There are following types of node affinity available and 1 is planned.
> 
<img width="720" alt="image" src="https://user-images.githubusercontent.com/45871181/235297123-a954567f-f762-424d-9849-99327a93d3c3.png">

**Type of Affinity**

<img width="760" alt="image" src="https://user-images.githubusercontent.com/45871181/235297249-76010b08-176c-4fcf-8ab5-9b5270739d34.png">

> When pod is getting created and needs to be scheduled and in case there is no node available with the Label then based on the type it will be schedule to some other Node or it will not be scheduled.
> If it's required then it will not be scheduled if it's preffered then it will be scheduled.
> During Execution - in case pod is running on some node and node label is changed, at present as per the affinity of DuringExecution is Ingore so it will continue to run.

<img width="777" alt="image" src="https://user-images.githubusercontent.com/45871181/235297409-7944d4bf-f9b0-4d58-aeb7-ec3b0fcfd1fb.png">

> The new one which is planned having change only during the exeuction, in that case it will be evicted/terminated.

<img width="858" alt="image" src="https://user-images.githubusercontent.com/45871181/235297445-7647f4ec-fda9-44e1-a1d5-da0f0ee6c8e1.png">


