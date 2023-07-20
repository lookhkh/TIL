# StateFullSet이란?

WorkLoad API Object의 일종으로서, Deployment와 비슷하게 이미지의 스펙을 정의하고, 
scale의 개수를 미리 정하며, 해당 개수를 유지, 관리하는 것은 동일하지만, 여기에 더하여 추가로
각 파드의 순서와 유일성을 보장한다.


> Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec.
> Unlike a Deployment, a StatefulSet maintains a sticky identity for each of its Pods.
> These pods are created from the same spec, but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling.
> (https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

예를 들어, Storage Volumes을 사용하여 파드의 생명주기와 관계없이 데이터의 영속성을 제공하고자 할 경우, 
StateFullSet을 사용할 수 있다. 파드의 경우 사라질 수 있지만, StateFullSet으로 배포된 파드의 경우,
 유니크한 식별자를 가지고 있기 때문에, 파드가 죽더라도 기존에 존재하는 식별자를 바탕으로 volumes과 매칭이 가능하다.

>   If you want to use storage volumes to provide persistence for your workload,
>  you can use a StatefulSet as part of the solution.
> Although individual Pods in a StatefulSet are susceptible to failure,
>  the persistent Pod identifiers make it easier to match existing volumes to the new Pods that replace any that have failed.

이때 아래와 같은 경우, StateFullSet을 사용을 고려해볼 수 있다.

* Stable, unique network identifiers.
* Stable, persistent storage.
* Ordered, graceful deployment and scaling.

 이때, 배포하고자 하는 어플리케이션이 일정한 식별자, 배포 순서, 삭제 순서, 확장 순서 등이 
 상관이 없는 경우(StateLess)에는 Deployment를 사용하는 것이 좋다.
* Ordered, automated rolling updates.


