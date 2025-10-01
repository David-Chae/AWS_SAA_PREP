# S3 Object Lambda  
# S3 객체 람다  

---

## Introduction to S3 Object Lambda  
## S3 객체 람다 소개  

There is another use case for EFS three access points called S3 Object Lambda.  
EFS 세 개의 접근 포인트와 관련된 또 다른 사용 사례는 S3 객체 람다입니다.  

---

The idea is that you have an S3 bucket, but you want to modify the object just before it is retrieved by a cloud application.  
아이디어는 S3 버킷이 있지만, 클라우드 애플리케이션이 객체를 가져오기 직전에 데이터를 수정하고 싶다는 것입니다.  

---

Instead of duplicating buckets to have different versions of each object, we can use S3 Object Lambda.  
각 객체의 버전을 위해 버킷을 복제하는 대신, S3 객체 람다를 사용할 수 있습니다.  

---

For this, we need the S3 access points that we just saw.  
이를 위해 앞서 살펴본 S3 접근 포인트가 필요합니다.  

---

How does that work?  
이것이 어떻게 작동할까요?  

---

Imagine we have the cloud and an S3 bucket in it.  
클라우드와 그 안의 S3 버킷이 있다고 상상해보세요.  

---

An e-commerce application owns the data in this S3 bucket and can access it directly to put and get the original objects.  
전자상거래 애플리케이션은 이 S3 버킷의 데이터를 소유하며, 원본 객체를 직접 업로드 및 다운로드할 수 있습니다.  

---

However, an analytics application may want to access only a redacted version of the object, meaning some data has been deleted from the object.  
하지만 분석 애플리케이션은 객체의 일부 데이터를 삭제한 편집된 버전에만 접근하고 싶어할 수 있습니다.  

---

Instead of creating a new S3 bucket for this, we create an S3 access point on top of the S3 bucket connected to a Lambda function.  
이를 위해 새 S3 버킷을 만드는 대신, S3 버킷 위에 Lambda 함수와 연결된 S3 접근 포인트를 생성합니다.  

---

A Lambda function allows you to run a bit of code in the cloud very easily.  
Lambda 함수는 클라우드에서 코드를 간단히 실행할 수 있게 해줍니다.  

---

This Lambda function redacts the object as it is being retrieved.  
이 Lambda 함수는 객체가 조회될 때 데이터를 편집합니다.  

---

On top of this Lambda function, we create an S3 Object Lambda access point.  
이 Lambda 함수 위에 S3 객체 람다 접근 포인트를 생성합니다.  

---

This is how the analytics application accesses our S3 buckets.  
이 방식으로 분석 애플리케이션이 S3 버킷에 접근합니다.  

---

To summarize, the analytics application accesses our S3 Object Lambda access points, which invoke our Lambda function.  
정리하면, 분석 애플리케이션은 S3 객체 람다 접근 포인트를 통해 Lambda 함수를 호출합니다.  

---

The Lambda function retrieves data from the S3 bucket and runs code to redact the data.  
Lambda 함수는 S3 버킷에서 데이터를 가져와 편집 코드를 실행합니다.  

---

Therefore, the analytics application obtains a redacted object from the very same S3 bucket as the e-commerce application.  
따라서 분석 애플리케이션은 전자상거래 애플리케이션과 동일한 S3 버킷에서 편집된 객체를 가져옵니다.  

---

Now, a marketing application may want access to an enriched object.  
이제 마케팅 애플리케이션은 강화된 데이터가 포함된 객체에 접근하고 싶어할 수 있습니다.  

---

They have a customer loyalty database to enhance the data.  
이들은 고객 충성도 데이터베이스를 사용해 데이터를 강화합니다.  

---

Instead of creating a new S3 bucket with all enriched objects, we use another Lambda function to enrich the data by looking it up from the customer loyalty database.  
모든 강화 객체를 위한 새 S3 버킷을 만드는 대신, 또 다른 Lambda 함수를 사용해 고객 충성도 데이터베이스에서 데이터를 조회하여 강화합니다.  

---

We create another Object Lambda access point on top of this.  
이 위에 또 다른 객체 람다 접근 포인트를 생성합니다.  

---

Therefore, the marketing application can access this S3 Object Lambda access point to get the enriched objects.  
따라서 마케팅 애플리케이션은 이 S3 객체 람다 접근 포인트를 통해 강화된 객체에 접근할 수 있습니다.  

---

As you can see, we only need one S3 bucket but can create access points and Object Lambda to modify the data as we wish.  
보시다시피, 하나의 S3 버킷만 필요하지만, 접근 포인트와 객체 람다를 통해 데이터를 원하는 대로 수정할 수 있습니다.  

---

## Use Cases for S3 Object Lambda  
## S3 객체 람다 사용 사례  

Redacting personally identifiable information (PII) for analytics or non-production environments.  
분석 또는 비생산 환경에서 개인 식별 정보(PII)를 편집합니다.  

---

Converting data formats, for example, from XML to JSON.  
데이터 형식을 변환합니다. 예: XML에서 JSON으로.  

---

Performing any kind of transformation, such as resizing and watermarking images on the fly, where the watermark is specific to the user who requests the object.  
실시간으로 이미지 크기 조정이나 워터마크 삽입과 같은 변환을 수행하며, 워터마크는 요청한 사용자별로 적용됩니다.  

---

S3 Object Lambda provides a cool usage pattern to modify data dynamically without duplicating storage.  
S3 객체 람다는 저장소를 복제하지 않고도 데이터를 동적으로 수정할 수 있는 훌륭한 사용 패턴을 제공합니다.  

---

This concludes our discussion on S3 Object Lambda.  
이로써 S3 객체 람다에 대한 논의를 마칩니다.  

---

## Key Takeaways  
## 핵심 요약  

S3 Object Lambda allows modification of objects just before retrieval without duplicating buckets.  
S3 객체 람다는 버킷을 복제하지 않고 객체가 조회되기 직전에 수정할 수 있게 합니다.  

---

It uses S3 access points connected to Lambda functions to transform data dynamically.  
S3 접근 포인트와 Lambda 함수를 사용하여 데이터를 동적으로 변환합니다.  

---

Use cases include redacting personally identifiable information, data format conversion, and user-specific image watermarking.  
사용 사례에는 개인 식별 정보 편집, 데이터 형식 변환, 사용자별 이미지 워터마크 적용이 포함됩니다.  

---

Multiple applications can access the same S3 bucket with different data views via Object Lambda access points.  
여러 애플리케이션이 객체 람다 접근 포인트를 통해 동일한 S3 버킷에서 서로 다른 데이터 뷰로 접근할 수 있습니다.  

🎮 **게임보상:**

* S3 Object Lambda 개념 이해 +10 XP
* Lambda 함수와 접근 포인트 연계 이해 +10 XP
* 데이터 편집, 강화, 변환 활용 사례 이해 +10 XP
  총 **30 XP 획득!** 🎉
