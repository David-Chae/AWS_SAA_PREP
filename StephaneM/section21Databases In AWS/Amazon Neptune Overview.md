```md
# Amazon Neptune Overview
# Amazon Neptune 개요
# → AWS의 Neptune 그래프 DB 소개

Now let's talk about Amazon Neptune.  
이제 Amazon Neptune에 대해 이야기해봅시다.  
→ 강의 시작 안내.

## Introduction to Amazon Neptune
## Amazon Neptune 소개
## → Neptune 기본 개념

Amazon Neptune is a fully managed graph database.  
Amazon Neptune은 완전 관리형 그래프 데이터베이스입니다.  
→ 서버 관리 필요 없이 그래프 DB 사용 가능.

An example of a graph dataset is something we all know: a social network.  
그래프 데이터셋의 예로 잘 알려진 것은 소셜 네트워크입니다.  
→ 시험 대비: 그래프 DB = 관계 데이터.

In a social network, people are friends, they like, connect, read, comment, and so on.  
소셜 네트워크에서는 사람들이 친구가 되거나, 좋아요, 연결, 읽기, 댓글 등을 합니다.  
→ 노드와 엣지 개념 이해.

Users have friends; posts have comments; comments have likes from users; users share and like posts.  
사용자는 친구가 있고, 게시물에는 댓글이 있으며, 댓글에는 좋아요가 있고, 사용자는 게시물을 공유하고 좋아요를 누릅니다.  
→ 관계형 데이터보다 더 복잡하게 얽힌 상호작용.

All these interactions are interconnected, creating a graph.  
모든 상호작용이 서로 연결되어 그래프를 형성합니다.  
→ Neptune 활용 이유.

This is why Neptune is a great choice of database when it comes to graph datasets.  
그래서 그래프 데이터셋에는 Neptune이 훌륭한 선택입니다.  
→ 시험 포인트: 그래프 DB = Neptune.

## Features of Amazon Neptune
## Amazon Neptune 특징
## → 주요 기능

Neptune supports replication across three availability zones and up to 15 read replicas.  
Neptune은 세 개의 가용 영역과 최대 15개의 읽기 복제본(replica)을 지원합니다.  
→ 고가용성 및 읽기 성능 향상.

It is used to build and run applications with highly connected datasets, such as social networks.  
Neptune은 소셜 네트워크처럼 연결이 많은 데이터셋을 다루는 애플리케이션 구축에 사용됩니다.  
→ 연결 중심 데이터 처리에 최적화.

Neptune is optimized to run complex and demanding queries on graph datasets.  
Neptune은 그래프 데이터셋에서 복잡하고 무거운 쿼리를 실행하도록 최적화되어 있습니다.  
→ 빠른 그래프 탐색 가능.

You can store up to billions of relationships in the database and query the graph with millisecond latency.  
수십억 개의 관계를 저장하고 밀리초 단위 지연으로 쿼리할 수 있습니다.  
→ 대규모 그래프 처리.

It is highly available with applications across multiple availability zones.  
애플리케이션은 여러 가용 영역에서 고가용성을 제공합니다.  
→ 장애 대비 설계.

Neptune is also great for storing knowledge graphs. For example, the Wikipedia database is a knowledge graph because all Wikipedia articles are interconnected.  
Neptune은 지식 그래프 저장에도 적합합니다. 예를 들어 Wikipedia 데이터베이스는 모든 문서가 연결되어 있으므로 지식 그래프입니다.  
→ 연결형 데이터 모델 활용 예시.

Other use cases include fraud detection, recommendation engines, and social networking.  
그 외 사용 사례로는 사기 탐지, 추천 엔진, 소셜 네트워킹 등이 있습니다.  
→ 시험 출제 가능 포인트.

From an exam perspective, any time you see anything related to graph databases, think of Neptune.  
시험 관점에서 그래프 DB 관련 문제가 나오면 Neptune을 떠올리세요.  
→ 핵심 시험 전략.

## Neptune Streams
## Neptune Streams
## → Neptune 스트림 기능

Amazon Neptune also has a feature called Neptune Streams.  
Amazon Neptune에는 Neptune Streams라는 기능도 있습니다.  
→ 실시간 데이터 변경 추적 기능.

Streams in Amazon Neptune are a real-time ordered sequence of data for every change that happens within your graph data in the Neptune database.  
Neptune Streams는 Neptune DB 내 그래프 데이터의 모든 변경 사항을 실시간으로 순서대로 제공하는 스트림입니다.  
→ 이벤트 기반 실시간 처리.

Whenever an application writes to Amazon Neptune, the changes will be available immediately after writing in Neptune Streams.  
애플리케이션이 Neptune에 쓰기를 수행하면, 변경 사항은 즉시 Neptune Streams에서 확인할 수 있습니다.  
→ 실시간 반영.

The stream contains no duplicates and maintains a strict ordering of changes happening within your Neptune cluster.  
스트림에는 중복이 없으며, Neptune 클러스터 내 변경 사항의 순서를 엄격히 유지합니다.  
→ 순서 보장 및 데이터 무결성.

In a graph, writes are written to your Neptune cluster and also to a Neptune stream.  
그래프에 대한 쓰기 작업은 Neptune 클러스터와 Neptune 스트림 모두에 기록됩니다.  
→ 동시 저장 구조.

This stream data is accessible using an HTTP REST API.  
이 스트림 데이터는 HTTP REST API를 통해 접근할 수 있습니다.  
→ 외부 애플리케이션 연동 가능.

Applications that want to read your Neptune Stream can use this API to get all the changes in real time.  
Neptune Stream을 읽고 싶은 애플리케이션은 이 API를 사용해 실시간으로 모든 변경 사항을 가져올 수 있습니다.  
→ 실시간 알림, 데이터 동기화 활용 가능.

## Use Cases for Neptune Streams
## Neptune Streams 활용 사례
## → 실무 및 시험 활용

Use cases for enabling Neptune Streams include sending notifications whenever changes are made within your graph data.  
Neptune Streams 활성화 사용 사례는 그래프 데이터 변경 시 알림 전송입니다.  
→ 이벤트 알림 시스템 구현.

They also include maintaining your data synchronized into another data store.  
또한 데이터를 다른 데이터 스토어와 동기화하는 것도 포함됩니다.  
→ 데이터 복제 및 동기화.

For example, you may want to replicate the changes happening within your Neptune cluster into Amazon S3, OpenSearch, ElastiCache, or more.  
예를 들어, Neptune 클러스터 내 변경 사항을 S3, OpenSearch, ElastiCache 등으로 복제할 수 있습니다.  
→ 여러 AWS 서비스 연계 활용.

Another use case is replicating data across multiple regions for your Neptune cluster by looking at all the changes in the stream and rewriting those into a target Neptune cluster.  
또 다른 사용 사례는 스트림의 모든 변경 사항을 보고 대상 Neptune 클러스터로 다시 기록하여 여러 리전에 데이터 복제하는 것입니다.  
→ 멀티 리전 복제.

That concludes this lecture. I hope you liked it, and I will see you in the next lecture.  
이로써 강의를 마칩니다. 즐거우셨길 바라며, 다음 강의에서 뵙겠습니다.  
→ 강의 종료 안내.

## Key Takeaways
## 핵심 요약
## → 시험/실무 필수 포인트

Amazon Neptune is a fully managed graph database optimized for highly connected datasets.  
Amazon Neptune은 완전 관리형 그래프 DB로, 연결성이 높은 데이터셋에 최적화되어 있습니다.  
→ 그래프 DB 정의 요약.

It supports replication across three availability zones and up to 15 read replicas for high availability.  
세 개 가용 영역과 최대 15개 읽기 복제본을 지원하여 고가용성을 제공합니다.  
→ 가용성, 확장성 핵심 포인트.

Neptune Streams provide a real-time, ordered sequence of data changes accessible via HTTP REST API.  
Neptune Streams는 실시간, 순서대로 정렬된 데이터 변경 사항을 HTTP REST API를 통해 제공합니다.  
→ 스트림 활용 포인트.

Use cases for Neptune Streams include sending notifications on data changes, synchronizing data to other stores, and replicating data across regions.  
Neptune Streams 활용 사례에는 데이터 변경 알림, 다른 스토어와 데이터 동기화, 리전 간 데이터 복제가 포함됩니다.  
→ 실무 및 시험 활용 예시.
```

🎮 **게임보상: Neptune 그래프 마스터 등극! 🏆**
→ 그래프 DB 문제, 실시간 스트림 문제 모두 자신감 있게 대응 가능.
