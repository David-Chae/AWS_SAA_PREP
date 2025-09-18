```markdown
# Encryption 101  
# 암호화 기초  

In this lecture, we will explore how encryption works at a high level, especially if you are not very familiar with the concept.  
이번 강의에서는 암호화의 기본 원리를 고수준에서 탐구해 보겠습니다. 특히 개념에 익숙하지 않은 분들을 위해 설명합니다.  
(암호화의 전반적 이해를 목표로 함)  

## Encryption in Flight: TLS and SSL  
## 전송 중 암호화: TLS와 SSL  

Encryption in flight refers to securing data as it travels over a network. This is commonly achieved using TLS or SSL protocols. TLS is the newer version of SSL.  
전송 중 암호화는 데이터가 네트워크를 통해 이동할 때 이를 보호하는 것을 말합니다. 일반적으로 TLS 또는 SSL 프로토콜을 사용하며, TLS는 SSL의 최신 버전입니다.  
(네트워크 상 데이터 보호 방식)  

Before sending data, it is encrypted, and upon receiving, it is decrypted. This process secures communication between a client and a server over a network.  
데이터는 전송 전에 암호화되고 수신 시 복호화됩니다. 이 과정은 네트워크 상에서 클라이언트와 서버 간의 통신을 안전하게 합니다.  
(데이터 전송 보호 방식 설명)  

TLS certificates are used to encrypt data. When you visit websites that show HTTPS in the URL, it means the connection between your browser and the server is encrypted using TLS certificates.  
TLS 인증서는 데이터를 암호화하는 데 사용됩니다. 웹사이트 주소(URL)에 HTTPS가 표시된다면, 이는 브라우저와 서버 간 연결이 TLS 인증서를 사용해 암호화되었음을 의미합니다.  
(HTTPS와 TLS 관계 설명)  

### Why Use Encryption in Flight?  
### 전송 중 암호화를 사용하는 이유  

Data sent over networks, especially public ones, passes through many servers. Without encryption, a man-in-the-middle attack could occur, where an intermediary server intercepts and observes the data packets.  
데이터가 네트워크, 특히 공용망을 통해 전송될 때는 여러 서버를 거칩니다. 암호화가 없다면 중간자 공격(Man-in-the-Middle)이 발생하여 중간 서버가 데이터 패킷을 가로채고 볼 수 있습니다.  
(암호화 필요성 설명)  

Using HTTPS or TLS ensures that only the intended target server can decrypt the data sent, protecting it from interception.  
HTTPS 또는 TLS를 사용하면 오직 의도된 대상 서버만 데이터를 복호화할 수 있어, 도청으로부터 보호됩니다.  
(보안 강화 효과)  

### Example: Secure Login  
### 예시: 안전한 로그인  

Consider a client and a server where the client wants to securely log in by sending a username and password.  
클라이언트가 사용자 이름과 비밀번호를 서버에 안전하게 전송하여 로그인하려는 상황을 생각해봅시다.  
(로그인 시나리오 예시)  

The client automatically applies TLS encryption to the credentials before sending them over the network. No intermediary server can decrypt this data.  
클라이언트는 네트워크로 전송하기 전에 TLS 암호화를 자격 증명에 적용합니다. 어떤 중간 서버도 이 데이터를 복호화할 수 없습니다.  
(자격 증명 보호 방식)  

Only the target server can decrypt the package using TLS decryption mechanisms, verify the credentials, and confirm a secure login.  
오직 대상 서버만 TLS 복호화 메커니즘을 사용해 데이터를 해독하고 자격 증명을 확인하여 안전한 로그인을 보장합니다.  
(로그인 과정의 안전성 확보)  

## Server-Side Encryption at Rest  
## 서버 측 저장 데이터 암호화  

Server-side encryption protects data after it has been received by the server, ensuring it is stored securely in encrypted form.  
서버 측 암호화는 데이터가 서버에 도착한 후 암호화된 형태로 안전하게 저장되도록 보호합니다.  
(저장 데이터 보호 개념)  

Data is decrypted before being sent back to clients. Encryption and decryption use a key, typically called a data key, which the server manages.  
데이터는 클라이언트에 다시 전송되기 전에 복호화됩니다. 암호화와 복호화는 보통 데이터 키라 불리는 키를 사용하며, 서버가 이를 관리합니다.  
(서버 관리 키 사용 설명)  

For example, when using a service like Amazon S3, an object is sent over HTTP or HTTPS (for in-flight encryption). The service receives the object in decrypted form.  
예를 들어, Amazon S3 같은 서비스를 사용할 때 객체는 HTTP 또는 HTTPS(전송 중 암호화)를 통해 전송됩니다. 서비스는 객체를 복호화된 상태로 수신합니다.  
(S3 암호화 처리 과정 설명)  

The service then encrypts the object at rest using the data key. When sending the object back to clients, the encrypted object and data key are used to decrypt it, and the decrypted object is sent over HTTPS.  
그 후 서비스는 데이터 키를 사용하여 객체를 저장 시 암호화합니다. 클라이언트로 다시 보낼 때는 암호화된 객체와 데이터 키를 사용해 복호화한 후 HTTPS를 통해 전달합니다.  
(저장 및 전송 과정 설명)  

This process ensures server-side encryption, as all encryption and decryption occur on the server.  
이 과정은 모든 암호화와 복호화가 서버에서 이루어지므로 서버 측 암호화가 보장됩니다.  
(서버 책임 암호화)  

## Client-Side Encryption  
## 클라이언트 측 암호화  

Client-side encryption means that data is encrypted and decrypted on the client side. The server never has the ability to decrypt the data, which is useful when the server is not fully trusted.  
클라이언트 측 암호화는 데이터가 클라이언트 쪽에서 암호화되고 복호화된다는 의미입니다. 서버는 데이터를 복호화할 수 없으며, 서버를 완전히 신뢰할 수 없는 경우 유용합니다.  
(클라이언트 중심 보안)  

In this scenario, the client holds the data key and encrypts the object before sending it to any storage service, such as FTP servers, Amazon S3, or EBS volumes.  
이 경우 클라이언트가 데이터 키를 보유하고 있으며, FTP 서버, Amazon S3, EBS 볼륨 같은 스토리지 서비스에 전송하기 전에 객체를 암호화합니다.  
(전송 전 암호화 과정)  

The server stores the data in encrypted form and cannot decrypt its contents.  
서버는 암호화된 형태의 데이터를 저장할 뿐 복호화할 수는 없습니다.  
(서버 접근 제한)  

When retrieving the data, the client receives the encrypted object and uses the data key to decrypt it locally.  
데이터를 가져올 때 클라이언트는 암호화된 객체를 수신하고, 데이터 키를 사용해 로컬에서 복호화합니다.  
(복호화 권한이 클라이언트에 있음)  

These are the three main encryption mechanisms commonly seen in cloud environments: encryption in flight, server-side encryption at rest, and client-side encryption.  
이것이 클라우드 환경에서 흔히 사용되는 세 가지 주요 암호화 방식입니다: 전송 중 암호화, 서버 측 저장 암호화, 클라이언트 측 암호화.  
(세 가지 암호화 모델 요약)  

I hope this lecture has been helpful in understanding these encryption concepts. See you in the next lecture.  
이번 강의가 이러한 암호화 개념을 이해하는 데 도움이 되었기를 바랍니다. 다음 강의에서 뵙겠습니다.  
(학습 마무리 인사)  

## Key Takeaways  
## 핵심 요약  

- Encryption in flight uses TLS/SSL to secure data transmitted between clients and servers.  
- 전송 중 암호화는 TLS/SSL을 사용하여 클라이언트와 서버 간 데이터 전송을 보호합니다.  

- Server-side encryption at rest protects data stored on servers using data keys managed by the server.  
- 서버 측 저장 암호화는 서버에서 관리하는 데이터 키를 사용해 저장된 데이터를 보호합니다.  

- Client-side encryption ensures data is encrypted and decrypted only on the client, preventing server access to plaintext data.  
- 클라이언트 측 암호화는 데이터가 클라이언트에서만 암호화/복호화되도록 보장하여 서버가 평문 데이터에 접근하지 못하게 합니다.  

- TLS certificates enable HTTPS connections, preventing man-in-the-middle attacks during data transmission.  
- TLS 인증서는 HTTPS 연결을 가능하게 하여 데이터 전송 중 중간자 공격을 방지합니다.  
```

🎮 게임보상: 🏆 "암호화 삼총사 마스터!" (전송 중, 서버 측, 클라이언트 측 암호화 모두 이해 완료!) 🔐✨
