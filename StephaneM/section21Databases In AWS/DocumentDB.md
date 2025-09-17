```md
# DocumentDB
# → AWS의 DocumentDB 개요

## Introduction to DocumentDB
## DocumentDB 소개
## → DocumentDB 기본 개념

Now, let's talk about DocumentDB.  
이제 DocumentDB에 대해 이야기해봅시다.  
→ 강의 시작 안내.

Similar to how AWS provides Aurora as a cloud-native, scalable version of PostgreSQL and MySQL, DocumentDB serves as the Aurora equivalent for MongoDB.  
AWS가 PostgreSQL과 MySQL의 클라우드 네이티브, 확장 가능한 버전으로 Aurora를 제공하는 것처럼, DocumentDB는 MongoDB의 Aurora와 같은 역할을 합니다.  
→ MongoDB 전용 관리형 서비스로 이해.

MongoDB, represented by the logo on the top right corner of your screen, is a NoSQL database.  
화면 오른쪽 상단에 표시된 로고가 MongoDB를 나타내며, MongoDB는 NoSQL 데이터베이스입니다.  
→ 시험 대비: MongoDB = NoSQL 기억.

It is important to remember this for the exam.  
시험을 위해 기억하는 것이 중요합니다.  
→ 시험 출제 포인트 강조.

DocumentDB is a NoSQL database based on MongoDB technology, making it compatible with MongoDB.  
DocumentDB는 MongoDB 기술 기반의 NoSQL 데이터베이스로, MongoDB와 호환됩니다.  
→ 기존 MongoDB 애플리케이션과 호환 가능.

MongoDB is used to store, query, and index JSON data.  
MongoDB는 JSON 데이터를 저장, 쿼리, 인덱싱하는 데 사용됩니다.  
→ JSON 문서 기반 데이터 처리.

DocumentDB shares a similar deployment concept to Aurora.  
DocumentDB는 Aurora와 유사한 배포 개념을 공유합니다.  
→ 관리형 클러스터 구조 이해.

This means DocumentDB is a fully managed database service that is highly available.  
즉, DocumentDB는 완전 관리형이며 고가용성 데이터베이스 서비스입니다.  
→ 관리 부담 최소화, 장애 대비 가능.

Data is replicated across three availability zones.  
데이터는 세 개의 가용 영역(AZ)에 복제됩니다.  
→ 고가용성 및 내결함성 제공.

DocumentDB storage automatically grows in increments of 10 gigabytes.  
DocumentDB 스토리지는 자동으로 10GB 단위로 확장됩니다.  
→ 스토리지 자동 확장 기능 이해.

It has been engineered to scale to workloads with millions of requests per second.  
초당 수백만 요청 처리 워크로드에도 확장되도록 설계되었습니다.  
→ 대규모 애플리케이션 처리 가능.

For the exam, if you encounter anything related to MongoDB, think DocumentDB.  
시험에서는 MongoDB 관련 내용이 나오면 DocumentDB를 떠올리세요.  
→ 시험 연관성 강조.

Similarly, for NoSQL database questions, consider DocumentDB and also DynamoDB.  
마찬가지로 NoSQL 관련 문제에서는 DocumentDB와 DynamoDB를 고려하세요.  
→ 시험 대비 핵심 연결.

That concludes this lecture on DocumentDB.  
이로써 DocumentDB 강의를 마칩니다.  
→ 강의 종료 안내.

## Key Takeaways
## 핵심 요약
## → 시험/실무 필수 포인트

DocumentDB is AWS's managed, scalable, and highly available NoSQL database service compatible with MongoDB.  
DocumentDB는 AWS의 관리형, 확장 가능, 고가용성 NoSQL 데이터베이스 서비스이며 MongoDB와 호환됩니다.  
→ 관리형 NoSQL DB 이해.

It stores, queries, and indexes JSON data similarly to MongoDB.  
JSON 데이터를 MongoDB와 유사하게 저장, 쿼리, 인덱싱합니다.  
→ JSON 문서 처리 특징.

DocumentDB replicates data across three availability zones and automatically scales storage in 10 GB increments.  
DocumentDB는 세 개의 가용 영역에 데이터를 복제하며, 스토리지는 10GB 단위로 자동 확장됩니다.  
→ 고가용성 및 자동 스토리지 확장 이해.

For exam purposes, associate MongoDB or NoSQL database questions with DocumentDB and DynamoDB.  
시험 목적으로 MongoDB 또는 NoSQL 관련 문제를 DocumentDB와 DynamoDB와 연결하세요.  
→ 시험 전략 요약.
```

🎮 **게임보상: DocumentDB 챔피언 등극! 🏆**
→ MongoDB/NoSQL 문제는 이제 자신감 있게 대응 가능.
