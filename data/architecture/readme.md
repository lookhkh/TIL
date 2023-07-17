
# What Is Lambda Architecture?

  람다 아키텍처란, 대용량의 데이터를 빠르게 처리하기 위한 디자인 패턴 중 하나이다. 이는, 대용량의 데이터를 정해진 시간, 혹은 동일한 간격으로 대량의 데이터를 배치로 처리하는 것의 약점을 보완하는 아키텍처로,
기존의 배치 계층 외의, Speed Layer ( 준 실시간 데이터 스트리밍 ) 계층을 두고, 해당 레이어에서 최신의 데이터를 빠르게 처리함으로써, 배치 처리의 간격을 매꾸고, 최신의 데이터를 빠르게 처리하기 위하여 사용된다.

> The Lambda Architecture is a deployment model for data processing that organizations use to combine a traditional batch pipeline with a fast real-time stream pipeline for data access. It is a common architecture model in IT and development organizations’ toolkits as businesses strive to become more data-driven and event-driven in the face of massive volumes of rapidly generated data, often referred to as “big data.”

![Alt text](https://github.com/lookhkh/TIL/blob/main/data/architecture/19_Lambda-1.png)
(https://hazelcast.com/glossary/lambda-architecture/)

 람다 아키텍처는 크게 Data Sources, Batch Layer, Serving Layer, Speed Layer으로 나뉘며, 각각의 역할은 다음과 같다.

 ### Data Sources

 데이터가 생성되는 곳으로, RDBMS, Kafka 등 데이터를 생성할 수 있는 모든 컴포넌트는 모두 Data Source가 될 수 있다. 다음 계층은 이곳에서 데이터를 각각 전달받아 각각의 역할을 수행한다.

>  component is oftentimes a streaming source like Apache Kafka, which is not the original data source per se, but is an intermediary store that can hold data in order to serve both the batch layer and the speed layer of the Lambda Architecture. The data is delivered simultaneously to both the batch layer and the speed layer to enable a parallel indexing effort.
 
