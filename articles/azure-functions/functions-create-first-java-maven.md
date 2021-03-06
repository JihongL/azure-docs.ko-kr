---
title: "Java 및 Maven을 사용하여 Azure에서 첫 번째 함수 만들기 | Microsoft Docs"
description: "Java 및 Maven을 사용하여 Azure에 간단한 HTTP 트리거 함수를 만들어 게시합니다."
services: functions
documentationcenter: na
author: rloutlaw
manager: justhe
keywords: "Azure 함수, 함수, 이벤트 처리, 계산, 서버를 사용하지 않는 아키텍처"
ms.service: functions
ms.devlang: java
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/07/2017
ms.author: routlaw, glenga
ms.custom: mvc, devcenter
ms.openlocfilehash: 3762a6e267540ef79577c3bf94ce27b648bd3534
ms.sourcegitcommit: c7215d71e1cdeab731dd923a9b6b6643cee6eb04
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="create-your-first-function-with-java-and-maven-preview"></a>Java 및 Maven을 사용하여 Azure에서 첫 번째 함수 만들기(미리 보기)

> [!NOTE] 
> Azure Functions용 Java는 현재 미리 보기로 제공되고 있습니다.

이 빠른 시작에서는 Maven을 사용하여 [서버 없는](https://azure.microsoft.com/overview/serverless-computing/) 함수 프로젝트를 만들어 로컬로 테스트하고 Azure Functions에 배포하는 과정을 안내합니다. 마친 후에는 Azure에서 HTTP 트리거 함수 앱이 실행됩니다.

![cURL로 명령줄에서 Hello World 함수 액세스](media/functions-create-java-maven/hello-azure.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>필수 조건
Java 통해 함수 앱을 개발하려면 다음을 설치해야 합니다.

-  [.NET Core](https://www.microsoft.com/net/core) 최신 버전
-  [Java Developer Kit](https://www.azul.com/downloads/zulu/) 버전 8
-  [Azure CLI](https://docs.microsoft.com/cli/azure)
-  [Apache Maven](https://maven.apache.org) 버전 3.0 이상
-  [Node.js](https://nodejs.org/download/) 버전 8.6 이상

> [!IMPORTANT] 
> 이 퀵 스타트를 완료하려면 JAVA_HOME 환경 변수를 JDK 설치 위치로 설정해야 합니다.

## <a name="install-the-azure-functions-core-tools"></a>Azure Functions 핵심 도구 설치

[Azure Functions Core Tools 2.0](https://www.npmjs.com/package/azure-functions-core-tools)는 Azure Functions의 작성, 실행 및 디버그를 위한 로컬 개발 환경을 제공합니다. [Node.js](https://nodejs.org/)에 포함된 [npm](https://www.npmjs.com/)을 사용하여 도구를 설치합니다.

```
npm install -g azure-functions-core-tools@core
```

> [!NOTE]
> Azure Functions Core Tools 버전 2.0 설치에 문제가 있으면 [버전 2.x 런타임](/azure/azure-functions/functions-run-local#version-2x-runtime)을 참조하세요.

## <a name="generate-a-new-functions-project"></a>새 Functions 프로젝트 생성

빈 폴더에서 다음 명령을 실행하여 [Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html)으로부터 Functions 프로젝트를 생성합니다.

### <a name="linuxmacos"></a>Linux/MacOS

```bash
mvn archetype:generate \
    -DarchetypeGroupId=com.microsoft.azure \
    -DarchetypeArtifactId=azure-functions-archetype 
```

### <a name="windows-cmd"></a>Windows(CMD)
```cmd
mvn archetype:generate ^
    -DarchetypeGroupId=com.microsoft.azure ^
    -DarchetypeArtifactId=azure-functions-archetype
```

Maven에 프로젝트 생성 완료를 위해 필요한 값을 입력하라는 메시지가 표시됩니다. _groupId_, _artifactId_ 및 _version_ 값은 [Maven 명명 규칙](https://maven.apache.org/guides/mini/guide-naming-conventions.html) 참고를 참조하세요. _appName_ 값은 Azure 전체에서 고유해야 하므로 기본적으로 Maven이 이전에 입력한 _artifactId_를 기준으로 앱 이름을 생성합니다. _packageName_ 값은 생성된 함수 코드에 대한 Java 패키지를 결정합니다.

```Output
Define value for property 'groupId': com.fabrikam.functions
Define value for property 'artifactId' : fabrikam-functions
Define value for property 'version' 1.0-SNAPSHOT : 
Define value for property 'package': com.fabrikam.functions
Define value for property 'appName' fabrikam-functions-20170927220323382:
Confirm properties configuration: Y
```

Maven은 이름이 _artifactId_인 새 폴더에 프로젝트 파일을 만듭니다. 프로젝트에서 생성된 코드는 요청의 본문을 에코하는 간단한 [HTTP 트리거](/azure/azure-functions/functions-bindings-http-webhook) 함수입니다.

```java
public class Function {
    @FunctionName("hello")
    public String hello(@HttpTrigger(name = "req", methods = {"get", "post"}, authLevel = AuthorizationLevel.ANONYMOUS) String req,
                        ExecutionContext context) {
        return String.format("Hello, %s!", req);
    }
}
```

## <a name="run-the-function-locally"></a>로컬에서 함수 실행

디렉터리를 새로 만든 프로젝트 폴더로 변경하고 Maven으로 함수를 실행합니다.

```
cd fabrikam-function
mvn clean package 
mvn azure-functions:run
```

함수가 실행되면 이 출력이 표시됩니다.

```Output
Listening on http://localhost:7071
Hit CTRL-C to exit...

Http Functions:

   hello: http://localhost:7071/api/hello
```

새 터미널에서 curl을 사용하여 명령줄에서 함수를 트리거합니다.

```
curl -w '\n' -d LocalFunction http://localhost:7071/api/hello
```

```Output
Hello LocalFunction!
```

터미널에서 `Ctrl-C`를 사용하여 함수 코드를 중지합니다.

## <a name="deploy-the-function-to-azure"></a>Azure에 함수 배포

Azure Functions에 대한 배포 프로세스는 Azure CLI의 계정 자격 증명을 사용합니다. [Azure CLI에 로그인하고](/cli/azure/authenticate-azure-cli?view=azure-cli-latest) `azure-functions:deploy` Maven 대상을 사용하여 새 함수 앱에 코드를 배포합니다.

```
az login
mvn azure-functions:deploy
```

배포가 완료되면 Azure 함수 앱에 액세스하는 데 사용할 수 있는 URL이 표시됩니다.

```output
[INFO] Successfully deployed Function App with package.
[INFO] Deleting deployment package from Azure Storage...
[INFO] Successfully deleted deployment package fabrikam-function-20170920120101928.20170920143621915.zip
[INFO] Successfully deployed Function App at https://fabrikam-function-20170920120101928.azurewebsites.net
[INFO] ------------------------------------------------------------------------
```

curl을 사용하여 Azure에서 실행 중인 함수 앱을 테스트합니다.

```
curl -w '\n' https://fabrikam-function-20170920120101928.azurewebsites.net/api/hello -d AzureFunctions
```

```Output
Hello AzureFunctions!
```

## <a name="next-steps"></a>다음 단계

간단한 HTTP 트리거가 있는 Java 함수 앱을 만들어 Azure Functions에 배포했습니다.

- Java 함수 개발에 대한 자세한 내용은 [Java 함수 개발자 가이드](functions-reference-java.md)를 참조합니다.
- `azure-functions:add` Maven 대상을 사용하여 프로젝트에 다른 트리거가 있는 다른 함수를 추가합니다.
- Visual Studio 코드를 사용하여 로컬로 함수를 디버그합니다. [Java 확장 팩](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)을 설치하고 Visual Studio Code에서 Functions 프로젝트를 연 상태에서 [디버거](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)를 포트 5005에 연결합니다. 그런 다음 편집기에서 중단점을 설정하고 로컬로 실행하는 동안 함수를 트리거합니다(![Visual Studio Code에서 함수 디버그](media/functions-create-java-maven/vscode-debug.png)).



