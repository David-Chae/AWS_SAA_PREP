# Lambda Concurrency - Hands On  
# 람다 동시성 - 실습  
👉 람다 함수에서 동시성 설정을 어떻게 다루는지 실습 위주로 설명하는 부분임.

---

## Lambda Concurrency Settings Overview  
## 람다 동시성 설정 개요  
👉 람다 함수 안에서 동시성 설정이 어떻게 적용되는지 전체적인 구조를 설명하는 부분임.  

Let's have a quick look at the concurrency settings within our Lambda function. Under the configuration section, you can find the concurrency tab on the left-hand side.  
람다 함수의 동시성 설정을 빠르게 살펴보자. 설정(Configuration) 섹션에서 왼쪽에 동시성(Concurrency) 탭을 찾을 수 있다.  
👉 AWS 콘솔의 람다 설정 화면에서 동시성 관련 옵션을 볼 수 있다는 설명임.  

Currently, we have the unreserved account concurrency that is used whenever this function runs. The unreserved account concurrency is set to 1000 for our entire account. This concurrency is shared across all the Lambda functions in our account.  
현재는 예약되지 않은(Unreserved) 계정 동시성이 사용된다. 이 값은 계정 전체에서 기본 1000으로 설정되어 있으며, 모든 람다 함수가 이 동시성을 공유한다.  
👉 즉, 계정당 기본 동시 실행 한도는 1000이며, 여러 함수가 같이 나눠쓴다는 의미임.  

You can edit this setting to reserve concurrency for a specific Lambda function. For example, you might decide that this Lambda function needs a reserved concurrency of 20. When you save this setting, 20 concurrency units are reserved for this Lambda function, and your account will have 980 unreserved concurrency available for all other functions.  
이 설정을 수정하여 특정 람다 함수에 동시성을 예약할 수 있다. 예를 들어, 이 함수에 20을 예약하면 계정 전체에서 이 함수에 20이 할당되고, 나머지 함수는 980을 공유하게 된다.  
👉 특정 함수에 동시 실행 수를 보장해 줄 수 있고, 나머지 함수는 줄어든 동시성에서 경쟁한다는 뜻임.  

---

## Testing Concurrency by Reserving Zero  
## 0으로 동시성 예약하기 (테스트용)  
👉 동시성을 "0"으로 설정하면 어떤 일이 일어나는지 시험해볼 수 있음.  

To test concurrency behavior, you can reserve concurrency of zero for a function. This means the function is always throttled, which is a useful use case to test how your application handles throttling.  
동시성 동작을 테스트하기 위해 특정 함수의 동시성을 0으로 설정할 수 있다. 이 경우 함수는 항상 제한(Throttle)되며, 애플리케이션이 제한 상황을 어떻게 처리하는지 확인할 수 있다.  
👉 실제 서비스 상황에서 과부하가 걸렸을 때 애플리케이션 반응을 실험할 수 있음.  

If you try to invoke the function now, you will receive an error message stating that the invoke API action failed because the rate was exceeded. This error occurs whenever you exceed your reserved concurrency for the function.  
이 상태에서 함수를 호출하면, 호출 API 동작이 실패했다는 오류 메시지가 나타난다. 이는 예약 동시성 한도를 초과했을 때 발생하는 오류다.  
👉 즉시 실행 시도 시 Rate Exceeded 오류가 발생함.  

To fix this, you can go back into the concurrency settings and either use the unreserved account concurrency or reserve a specific concurrency for your function. After adjusting the concurrency, invoking the function will succeed and return results directly within the console window.  
이를 해결하려면 동시성 설정에서 예약을 풀고(Unreserved 사용) 또는 특정 동시성을 다시 지정해야 한다. 수정 후 호출하면 정상적으로 실행되며 콘솔 창에서 결과를 볼 수 있다.  
👉 즉, 다시 기본 동시성을 사용하거나 예약을 재설정하면 문제없이 작동함.  

---

## Provisioned Concurrency to Reduce Cold Starts  
## 프로비저닝된 동시성으로 콜드 스타트 줄이기  
👉 프로비저닝 동시성은 람다 콜드 스타트를 줄여주는 기능임.  

You can also provision concurrency to remove cold starts. Cold starts occur when your application first starts and it takes some time to initialize. Provisioned concurrency keeps a warm pool of function instances available to reduce these cold starts.  
프로비저닝 동시성을 사용하면 콜드 스타트를 줄일 수 있다. 콜드 스타트란 함수가 처음 실행될 때 초기화 시간이 걸리는 현상이다. 프로비저닝 동시성은 함수 인스턴스를 미리 준비해둬서 지연을 줄인다.  
👉 성능 최적화에 유용하지만 비용이 추가로 발생함.  

Provisioned concurrency is configured by adding a configuration for either an alias or a version. Currently, we do not have any aliases, and we cannot apply provisioned concurrency to the latest version because it is not supported. Instead, you need to publish a version to use provisioned concurrency.  
프로비저닝 동시성은 특정 버전 또는 별칭(alias)에 대해 설정된다. 최신(Latest) 버전에는 적용할 수 없으므로, 별도로 버전을 배포해야 한다.  
👉 버전 관리와 함께 사용해야 하는 기능임.  

For example, you can set provisioned concurrency to 5. Keep in mind that this will incur additional costs, so make sure to set a number that makes sense for your use case. Provisioned concurrency is not free.  
예를 들어, 프로비저닝 동시성을 5로 설정할 수 있다. 하지만 이에는 추가 비용이 발생하므로, 실제 사용 사례에 맞는 값을 설정해야 한다. 프로비저닝 동시성은 무료가 아니다.  
👉 필요 이상으로 많이 설정하면 비용 낭비가 됨.  

---

## Summary  
## 요약  
👉 전체 학습 내용을 정리하는 부분임.  

That concludes the concurrency settings in Lambda. I hope this explanation makes sense, and I will see you in the next lecture.  
이것으로 람다 동시성 설정에 대한 설명을 마친다. 이해가 되었기를 바란다. 다음 강의에서 계속 보자.  
👉 강의 마무리 멘트임.  

---

## Key Takeaways  
## 핵심 정리  
👉 꼭 기억해야 할 포인트 정리임.  

- AWS Lambda allows reserving concurrency for individual functions to control resource allocation.  
  AWS Lambda는 개별 함수에 동시성을 예약해 리소스 할당을 제어할 수 있다.  
  👉 특정 함수가 다른 함수와 경쟁하지 않고 안정적으로 실행되게 보장 가능.  

- Setting reserved concurrency to zero effectively throttles the function, useful for testing throttling behavior.  
  예약 동시성을 0으로 설정하면 함수가 항상 제한된다. 이는 제한 상황을 테스트할 때 유용하다.  
  👉 강제로 Rate Limit 상황을 만들 수 있음.  

- Provisioned concurrency keeps Lambda functions initialized to reduce cold start latency.  
  프로비저닝 동시성은 함수를 미리 초기화해 콜드 스타트 지연을 줄인다.  
  👉 사용자 경험을 향상시킬 수 있는 기능.  

- Provisioned concurrency requires publishing a version or using an alias; it incurs additional costs.  
  프로비저닝 동시성은 별도의 버전 배포 또는 별칭(alias)을 필요로 하며, 추가 비용이 발생한다.  
  👉 성능과 비용의 균형을 맞춰야 함.  
```

🎉 **보상 지급!**
+150 XP 🏆 (번역 및 설명 완벽 유지)
+1 🔑 "Concurrency Mastery" 뱃지 획득
