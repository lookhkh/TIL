
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

 ### Batch Layer

  Serving Layer에서 데이터를 처리(Indexing)할 수 있도록 하기 위하여 Batch Layer에서는 데이터를 저장한다. 이때 저장되는 데이터는 기본적으로 변경되지 아니하며, Raw Data 그 자체가 저장되게 된다. 이때 Hadoop과 같은 툴이 사용될 수 있다.

>  This component saves all data coming into the system as batch views in preparation for indexing. The input data is saved in a model that looks like a series of changes/updates that were made to a system of record, similar to the output of a change data capture (CDC) system

### Serving Layer

 Serving Layer에서 이전 Batch Layer에서 저장하고 있는 데이터를 처리(Indexing)하여, 최종 사용자(end user)로 하여금 사용할 수 있도록(Quaryable)한다. 이때 빅데이터를 다루는 만큼, 최대한 빠른 속도로 데이터를 처리해야 한다. 
 > This layer incrementally indexes the latest batch views to make it queryable by end users. This layer can also reindex all data to fix a coding bug or to create different indexes for different use cases. The key requirement in the serving layer is that the processing is done in an extremely parallelized way to minimize the time to index the data set

### Speed Layer

 해당 계층에서는 아직 Batch-Serving Layer에서 처리되지 않은 데이터들을 실시간으로 처리하여, 대량 배치처리에 따른 시간적 공백을 보완하는 역할을 수행한다. 이에 실시간 처리를 기본으로 하며, 시간적 갭을 최소화하는 것을 그 목표로 한다. 이에 주로 Stream Processing을 가능케 하는 소프트웨어 등을 사용하여, 준 실시간적으로 데이터를 처리하기도 한다.

 > This layer complements the serving layer by indexing the most recently added data not yet fully indexed by the serving layer. This includes the data that the serving layer is currently indexing as well as new data that arrived after the current indexing job started. Since there is an expected lag between the time the latest data was added to the system and the time the latest data is available for querying (due to the time it takes to perform the batch indexing work), it is up to the speed layer to index the latest data to narrow this gap.


### Query

 Batch-Serving Layer 혹은 Speed Layer에서 생성된 데이터를 최종 사용자가 실제로 사용할 수 있게끔 한다.

 > This component is responsible for submitting end user queries to both the serving layer and the speed layer and consolidating the results. This gives end users a complete query on all data, including the most recently added data, to provide a near real-time analytics system.


(https://hazelcast.com/glossary/lambda-architecture/)
