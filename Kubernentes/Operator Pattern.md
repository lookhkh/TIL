# Operator Pattern란?
---
> Operators are software extensions to Kubernetes that make use of custom resources to manage applications and their components
<https://kubernetes.io/docs/concepts/extend-kubernetes/operator/>

쿠버네티스의 익스텐션으로, Custom Resource(이하 CR)을 사용하여 어플리케이션과 컴포넌트들을 관리할 수 있도록 해주는 패턴이다.


## Operator Pattern이 필요한 이유
---
> The operator pattern aims to capture the key aim of a human operator who is managing a service or set of services. Human operators who look after specific applications and services have deep knowledge of how the system ought to behave, how to deploy it,   and how to react if there are problems.
People who run workloads on Kubernetes often like to use automation to take care of repeatable tasks. **The operator pattern captures how you can write code to automate a task beyond what Kubernetes itself provides.**
<https://kubernetes.io/docs/concepts/extend-kubernetes/operator/>


 당장 카프카 클러스터를 쿠버네티스에 올려야 한다고 가정해보자. 이 경우, 단순히 카프카만 노드에 설치하여 실행할 수는 없으며, 당장 버전에 따라서는 주키퍼 클러스터도 생성해주어야 하며, 각 클러스터간의 의존성도 생성해주어야 할 것이다. 또한, 의존성에 맞게 적절하게 순서도 지켜주어야 한다. 

 그러다보니 경우에 따라서는 이러한 작업들이 매우 귀찮고 힘들 수 있는데, 이러한 반복적인 작업들을 자동화하기 위하여 쿠버네티스에서는 **Operator Pattern**을 제공해주고 있다. 이를 활용하면 쿠버네티스의 기능을 온전히 사용하면서도 추가적인 코드의 수정 없이 배포 및 어플리케이션의 관리를 자동화할 수 있다.

 이를 위하여 개발자는 Custom Resource를 생성하고, 이를 관리하는 컨트롤러를 직접 선언하여, POD로 띄어두면, 해당 컨트롤러는 클러스터의 공통 저장소(예를 들어 etcd)를 Control loop 함으로써 변경을 감지 및 처리의 자동화를 가능케 해준다. 즉, Custome Resource의 값이 변경될 경우, Controller는 이를 확인하고 있다가 변경을 감지하면, 감지된 변경에 따른 작업을 자동으로 처리해 주는 것이다.

 또한, 기존에 공개된 Operator가 없거나, 요구사항에 적절하지 않은 경우, 이를 직접 개발할 수 있는 API 혹은 SDK 등을 제공해주기 때문에 필요하다면 직접 개발을 할 수도 있다.

 



