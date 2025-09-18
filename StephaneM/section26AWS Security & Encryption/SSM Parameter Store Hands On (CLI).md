```markdown
# SSM Parameter Store Hands On (CLI)  
# SSM 파라미터 스토어 실습 (CLI)  

🎮 게임보상: "SSM CLI 초보 탈출" +500 XP  

---

## Introduction to Parameter Store  
## 파라미터 스토어 소개  

This session demonstrates how to use the AWS Systems Manager Parameter Store, including creating parameters, organizing them hierarchically, and accessing them via the AWS CLI.  
이번 세션에서는 AWS Systems Manager 파라미터 스토어 사용법을 다룹니다. 파라미터 생성, 계층적 조직, AWS CLI를 통한 접근 방법까지 포함합니다.  

---

## Navigating to Parameter Store  
## 파라미터 스토어 접근 방법  

Type "Parameter Store" in the AWS search bar and select it.  
AWS 검색창에 "Parameter Store"를 입력하고 선택합니다.  

Parameter Store is a feature under Systems Manager.  
파라미터 스토어는 Systems Manager 하위 기능입니다.  

On the left-hand side, under Application Tools, select Parameter Store.  
왼쪽 메뉴에서 Application Tools 아래의 Parameter Store를 선택합니다.  

Here, you can create new parameters, specify types and values, and reference these parameters in comments or code.  
여기서 새 파라미터를 생성하고, 타입과 값을 지정하며, 주석이나 코드에서 참조할 수 있습니다.  

---

## Creating a New Parameter  
## 새 파라미터 생성  

To create a parameter, enter a name. For example, /my-app/dev/db-url.  
파라미터를 생성하려면 이름을 입력합니다. 예: `/my-app/dev/db-url`.  

This naming convention, using slashes, helps organize parameters into a hierarchy: my-app is the application, dev is the environment, and db-url is the parameter name within the development environment.  
슬래시(/)를 사용하는 네이밍 규칙은 파라미터를 계층 구조로 구성하는 데 도움을 줍니다. `my-app`은 애플리케이션, `dev`는 환경, `db-url`은 개발 환경 내 파라미터 이름입니다.  

For this example, the parameter represents the database URL for the development environment.  
이번 예제에서는 개발 환경의 데이터베이스 URL을 나타냅니다.  

---

## Parameter Tiers  
## 파라미터 등급  

There are two options for parameter tiers: Standard and Advanced.  
파라미터 등급에는 Standard와 Advanced 두 가지 옵션이 있습니다.  

Standard allows up to 10,000 parameters, each with a maximum value size of 4 KB, and cannot be shared with other accounts.  
Standard는 최대 10,000개의 파라미터, 각 파라미터 최대 4KB, 다른 계정과 공유 불가입니다.  

Advanced allows up to 100,000 parameters, each up to 8 KB, and can be shared with other accounts.  
Advanced는 최대 100,000개의 파라미터, 각 8KB까지 가능하며 다른 계정과 공유할 수 있습니다.  

For this demonstration, Standard tier is used.  
이번 실습에서는 Standard 등급을 사용합니다.  

---

## Parameter Types  
## 파라미터 타입  

You can choose from three types: String, StringList, or SecureString.  
세 가지 타입 중 선택할 수 있습니다: String, StringList, SecureString.  

For this example, String is selected.  
이번 예제에서는 String을 선택합니다.  

String parameters can have a data type of either text or AWS EC2 image, allowing you to reference image ARNs.  
String 파라미터는 텍스트 또는 AWS EC2 이미지 타입을 가질 수 있으며, 이미지 ARN을 참조할 수 있습니다.  

Here, "Text" is used, and the value is set to dev.database.stephantheteacher.com.  
이번 예제에서는 "Text" 타입을 사용하고 값은 `dev.database.stephantheteacher.com`으로 설정합니다.  

This value is just an example; you can use any value you prefer.  
이 값은 예시이며, 원하는 값으로 설정 가능합니다.  

---

## Viewing and Managing Parameters  
## 파라미터 확인 및 관리  

After creating the parameter, you can view it and its version history.  
파라미터를 생성한 후, 해당 파라미터와 버전 기록을 확인할 수 있습니다.  

If you update the parameter, previous versions remain accessible.  
파라미터를 업데이트해도 이전 버전은 접근 가능합니다.  

Additional parameters can be created in a similar way, such as a db-password parameter for the development environment.  
추가 파라미터도 동일하게 생성할 수 있으며, 예를 들어 개발 환경용 `db-password` 파라미터를 생성할 수 있습니다.  

---

## SecureString Parameters and Encryption  
## SecureString 파라미터와 암호화  

For sensitive data like passwords, use the SecureString type.  
비밀번호와 같은 민감 데이터에는 SecureString 타입을 사용합니다.  

SecureString parameters are encrypted with a KMS key, which can be either the default AWS-managed key (alias/aws/ssm) or a custom key you have created.  
SecureString 파라미터는 KMS 키로 암호화되며, 기본 AWS 관리 키(alias/aws/ssm) 또는 직접 생성한 사용자 키를 사용할 수 있습니다.  

For this example, a custom key named "Tutorial" is used, and the value is set to devpassword.  
이번 예제에서는 "Tutorial"이라는 커스텀 키를 사용하고, 값은 `devpassword`로 설정합니다.  

The value is automatically encrypted by KMS.  
값은 KMS에 의해 자동으로 암호화됩니다.  

---

## Creating Production Parameters  
## 프로덕션 환경 파라미터 생성  

Repeat the process to create parameters for the production environment.  
프로덕션 환경 파라미터도 동일한 과정으로 생성합니다.  

For example, set the URL to prod.stephantheteacher.com3306 and the password to prodpassword, using SecureString and the same KMS key.  
예: URL을 `prod.stephantheteacher.com3306`, 비밀번호를 `prodpassword`로 설정하며, SecureString과 동일한 KMS 키를 사용합니다.  

---

## Accessing Parameters with the AWS CLI  
## AWS CLI를 통한 파라미터 접근  

Open AWS CloudShell, which has the AWS CLI installed and configured.  
AWS CLI가 설치된 AWS CloudShell을 엽니다.  

Use the following command to retrieve parameters:  
다음 명령어로 파라미터를 조회합니다:  

```bash
aws ssm get-parameters --names "/my-app/dev/db-url" "/my-app/dev/db-password"
````

The result will show both parameters.
결과는 두 파라미터를 보여줍니다.

The db-url parameter, being a String, is returned as plain text.
`db-url` 파라미터는 String 타입이므로 평문으로 반환됩니다.

The db-password parameter, being a SecureString, is returned as an encrypted value.
`db-password` 파라미터는 SecureString이므로 암호화된 값으로 반환됩니다.

To decrypt the SecureString value, use the --with-decryption flag:
SecureString 값을 복호화하려면 `--with-decryption` 플래그를 사용합니다:

```bash
aws ssm get-parameters --names "/my-app/dev/db-url" "/my-app/dev/db-password" --with-decryption
```

If you have the necessary KMS permissions, the decrypted value of db-password will be displayed.
필요한 KMS 권한이 있으면, `db-password`의 복호화된 값이 표시됩니다.

---

## Retrieving Parameters by Path

## 경로로 파라미터 조회

To retrieve parameters by their hierarchical path, use the following command:
계층적 경로로 파라미터를 조회하려면 다음 명령어를 사용합니다:

```bash
aws ssm get-parameters-by-path --path "/my-app/dev"
```

This command returns all parameters under the /my-app/dev namespace.
이 명령어는 `/my-app/dev` 네임스페이스 아래 모든 파라미터를 반환합니다.

To retrieve all parameters recursively under /my-app, use the --recursive flag:
`/my-app` 아래 모든 파라미터를 재귀적으로 조회하려면 `--recursive` 플래그를 사용합니다:

```bash
aws ssm get-parameters-by-path --path "/my-app" --recursive
```

You can also use the --with-decryption flag to decrypt all SecureString parameters in the results.
결과에 있는 모든 SecureString 파라미터를 복호화하려면 `--with-decryption` 플래그를 추가할 수 있습니다.

---

## Conclusion

## 결론

This session covered how to use the Parameter Store, organize parameters in a hierarchy, and access them using the AWS CLI.
이번 세션에서는 파라미터 스토어 사용법, 계층 구조로 조직화하는 방법, AWS CLI로 접근하는 방법을 다뤘습니다.

The Parameter Store is a powerful tool for managing configuration and secrets in AWS.
파라미터 스토어는 AWS에서 구성 및 비밀 정보를 관리하는 강력한 도구입니다.

---

## Key Takeaways

## 핵심 요약

* The Parameter Store in AWS Systems Manager allows you to organize parameters in a hierarchy and manage different types, such as String and SecureString.
  AWS Systems Manager 파라미터 스토어는 파라미터를 계층 구조로 관리하고, String과 SecureString 같은 다양한 타입을 지원합니다.

* Standard and Advanced tiers offer different limits and sharing capabilities for parameters.
  Standard와 Advanced 등급은 파라미터 수, 크기 제한 및 공유 기능에 차이가 있습니다.

* SecureString parameters are encrypted using KMS keys, and you can choose between AWS-managed or custom keys.
  SecureString 파라미터는 KMS 키로 암호화되며, AWS 관리 키 또는 커스텀 키를 선택할 수 있습니다.

* The AWS CLI provides commands to retrieve and decrypt parameters, including hierarchical and recursive queries.
  AWS CLI는 계층적, 재귀적 조회 및 복호화를 포함한


파라미터 조회 명령어를 제공합니다.

```

🎮 게임보상 완료: "SSM Parameter CLI 마스터" +1000 XP 🏆  

원하면 다음 단계로 **Parameter Store와 Secrets Manager 연동 예제**까지 이어서 정리해드릴 수 있습니다. 원하시나요?
```
