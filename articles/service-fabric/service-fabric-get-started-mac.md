---
title: "Azure Service Fabric에서 작업하도록 Mac OS X에서 개발 환경 설정 | Microsoft Docs"
description: "런타임, SDK 및 도구를 설치하고 로컬 개발 클러스터를 만듭니다. 이 설정을 완료하면 Mac OS X에서 응용 프로그램을 빌드할 수 있습니다."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/17/2017
ms.author: saysa
ms.openlocfilehash: 328b2778a68e32d95b666124bf7bba969a5f52a6
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Mac OS X에서 개발 환경 설정
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

Mac OS X를 사용하여 Azure Service Fabric 응용 프로그램을 Linux 클러스터에서 실행하도록 빌드할 수 있습니다. 이 문서에서는 개발을 위해 Mac을 설정하는 방법을 설명합니다.

## <a name="prerequisites"></a>필수 조건
Azure Service Fabric은 Mac OS X에서 기본적으로 실행되지 않습니다. 로컬 Service Fabric 클러스터를 실행하기 위해 미리 구성된 Docker 컨테이너 이미지가 제공됩니다. 시작하기 전에 다음 항목이 필요합니다.

* RAM 4GB 이상
* 최신 버전의 [Docker](https://www.docker.com/)
* Service Fabric [onebox Docker 컨테이너 이미지](https://hub.docker.com/r/servicefabricoss/service-fabric-onebox/)에 대한 액세스 권한

>[!TIP]
>
>Docker를 Mac에 설치하려면 [Docker 설명서](https://docs.docker.com/docker-for-mac/install/#what-to-know-before-you-install)의 단계를 따릅니다. 설치 후 [설치를 확인합니다](https://docs.docker.com/docker-for-mac/#check-versions-of-docker-engine-compose-and-machine).
>

## <a name="create-a-local-container-and-set-up-service-fabric"></a>로컬 컨테이너 만들기 및 Service Fabric 설정
로컬 Docker 컨테이너를 설정하고 Service Fabric 클러스터가 실행되도록 하려면 다음 단계를 수행합니다.

1. Docker 허브 리포지토리에서 Service Fabric onebox 컨테이너 이미지를 끌어옵니다.

    ```bash
    docker pull servicefabricoss/service-fabric-onebox
    ```

2. 다음 설정을 사용하여 호스트에서 Docker 디먼 구성을 업데이트하고 Docker 디먼을 다시 시작합니다. 

    ```json
    {
        "ipv6": true,
        "fixed-cidr-v6": "fd00::/64"
    }
    ```
    이러한 설정은 Docker 설치 경로의 daemon.json 파일에서 직접 업데이트할 수 있습니다.
    
    >[!NOTE]
    >
    >daemon.json 파일의 위치는 컴퓨터마다 다를 수 있습니다. 예: ~/Library/Containers/com.docker.docker/Data/database/com.docker.driver.amd64-linux/etc/docker/daemon.json.
    >
    >권장되는 방식은 디먼 구성 설정을 Docker에서 직접 수정하는 것입니다. **Docker 아이콘**을 선택한 다음 **기본 설정** > **디먼** > **고급**을 선택합니다.
    >

3. Service Fabric onebox 컨테이너 인스턴스를 시작하고 첫 번째 단계에서 끌어온 이미지를 사용합니다.

    ```bash
    docker run -itd -p 19080:19080 --name sfonebox servicefabricoss/service-fabric-onebox
    ```
    >[!TIP]
    >읽기 쉬운 방식으로 처리할 수 있도록 컨테이너 인스턴스의 이름을 제공합니다. 
    >
    >응용 프로그램을 특정 포트에서 수신 대기하는 경우 추가 `-p` 태그를 사용하여 포트를 지정해야 합니다. 예를 들어 응용 프로그램이 포트 8080에서 수신 대기하는 경우 다음 `-p` 태그를 추가합니다.
    >
    >`run docker run -itd -p 19080:19080 -p 8080:8080 --name sfonebox servicefabricoss/service-fabric-onebox`
    >

4. 대화형 SSH 모드에서 Docker 컨테이너에 로그인합니다.

    ```bash
    docker exec -it sfonebox bash
    ```

5. 설정 스크립트를 실행하여 필요한 종속성을 가져오고 컨테이너에서 클러스터를 시작합니다.

    ```bash
    ./setup.sh     # Fetches and installs the dependencies required for Service Fabric to run
    ./run.sh       # Starts the local cluster
    ```

6. 5단계가 완료되면 Mac에서 `http://localhost:19080`으로 이동합니다. Service Fabric 탐색기가 표시됩니다.

## <a name="set-up-the-service-fabric-cli-sfctl-on-your-mac"></a>Mac에서 Service Fabric CLI(sfctl) 설정

[Service Fabric CLI](service-fabric-cli.md#cli-mac)의 지침에 따라 Mac에 Service Fabric CLI(`sfctl`)를 설치합니다.
CLI 명령은 클러스터, 응용 프로그램 및 서비스를 비롯한 Service Fabric 엔터티와의 상호 작용을 지원합니다.

## <a name="create-your-application-on-your-mac-by-using-yeoman"></a>Yeoman을 사용하여 Mac에서 응용 프로그램 만들기

Service Fabric은 Yeoman 템플릿 생성기를 사용하여 터미널에서 Service Fabric 응용 프로그램을 만들 수 있는 스캐폴딩 도구를 제공합니다. 컴퓨터에서 Service Fabric Yeoman 템플릿 생성기가 작동하는지 확인하려면 다음 단계를 수행합니다.

1. Node.js 및 NPM(노드 패키지 관리자)가 Mac에 설치되어 있어야 합니다. 다음과 같이 [HomeBrew](https://brew.sh/)를 사용하여 소프트웨어를 설치할 수 있습니다.

    ```bash
    brew install node
    node -v
    npm -v
    ```
2. 컴퓨터에 NPM의 [Yeoman](http://yeoman.io/) 템플릿 생성기를 설치합니다.

    ```bash
    npm install -g yo
    ```
3. 시작 [설명서](service-fabric-get-started-linux.md)의 단계를 수행하여 원하는 Yeoman 생성기를 설치합니다. Yeoman을 사용하여 Service Fabric 응용 프로그램을 만들려면 다음 단계를 수행합니다.

    ```bash
    npm install -g generator-azuresfjava       # for Service Fabric Java Applications
    npm install -g generator-azuresfguest      # for Service Fabric Guest executables
    npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
    ```
4. Mac에서 Service Fabric Java 응용 프로그램을 빌드하려면 JDK 버전 1.8 및 Gradle을 호스트 컴퓨터에 설치해야 합니다. 다음과 같이 [HomeBrew](https://brew.sh/)를 사용하여 소프트웨어를 설치할 수 있습니다. 

    ```bash
    brew update
    brew cask install java
    brew install gradle
    ```

## <a name="deploy-your-application-on-your-mac-from-the-terminal"></a>터미널에서 Mac에 응용 프로그램 배포

Service Fabric 응용 프로그램을 만들고 빌드한 후 [Service Fabric CLI](service-fabric-cli.md#cli-mac)를 사용하여 응용 프로그램을 배포할 수 있습니다.

1. Mac의 컨테이너 인스턴스 내에서 실행 중인 Service Fabric 클러스터에 연결합니다.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. 프로젝트 디렉터리 내부에서 설치 스크립트를 실행합니다.

    ```bash
    cd MyProject
    bash install.sh
    ```

## <a name="set-up-net-core-20-development"></a>.NET Core 2.0 개발 설정

[Mac용 .NET Core 2.0 SDK](https://www.microsoft.com/net/core#macos)를 설치하여 [C# Service Fabric 응용 프로그램을 만들기](service-fabric-create-your-first-linux-application-with-csharp.md) 시작합니다. .NET Core 2.0 Service Fabric 응용 프로그램용 패키지는 현재 미리 보기 상태인 NuGet.org에서 호스트됩니다.

## <a name="install-the-service-fabric-plug-in-for-eclipse-neon-on-your-mac"></a>Mac에 Eclipse Neon용 Service Fabric 플러그 인 설치

Azure Service Fabric은 Java IDE용 Eclipse Neon의 플러그 인을 제공합니다. 플러그 인은 Java 서비스를 만들고 빌드하고 배포하는 프로세스를 간소화합니다. Eclipse용 Service Fabric 플러그 인을 설치하거나 최신 버전으로 업데이트하려면 [다음 단계](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon)를 수행합니다. [Eclipse용 Service Fabric 설명서](service-fabric-get-started-eclipse.md)의 다른 단계도 적용할 수 있습니다. 응용 프로그램 빌드, 응용 프로그램에 서비스 추가, 응용 프로그램 제거 등을 수행할 수 있습니다.

마지막 단계는 호스트와 공유되는 경로로 컨테이너를 인스턴스화하는 것입니다. Mac의 Docker 컨테이너로 작업하려면 플러그인에 이러한 유형의 인스턴스화가 필요합니다. 예:

```bash
docker run -itd -p 19080:19080 -v /Users/sayantan/work/workspaces/mySFWorkspace:/tmp/mySFWorkspace --name sfonebox servicefabricoss/service-fabric-onebox
```

특성은 다음과 같이 정의됩니다.
* `/Users/sayantan/work/workspaces/mySFWorkspace`는 Mac에 있는 작업 영역의 정규화된 경로입니다.
* `/tmp/mySFWorkspace`는 작업 영역을 매핑해야 하는 컨테이너 내부의 경로입니다.

>[!NOTE]
> 
>작업 영역의 이름/경로가 다른 경우 `docker run` 명령에서 이 값을 업데이트합니다.
> 
>`sfonebox`가 아닌 이름으로 컨테이너를 시작하는 경우 Service Fabric 작업자 Java 응용 프로그램의 testclient.sh 파일에서 이름 값을 업데이트합니다.
>

## <a name="next-steps"></a>다음 단계
<!-- Links -->
* [Yeoman을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포](service-fabric-create-your-first-linux-application-with-java.md)
* [Eclipse용 Service Fabric 플러그 인을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포](service-fabric-get-started-eclipse.md)
* [Azure Portal에서 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-via-portal.md)
* [Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-via-arm.md)
* [Service Fabric 응용 프로그램 모델 이해](service-fabric-application-model.md)
* [Service Fabric CLI를 사용하여 응용 프로그램 관리](service-fabric-application-lifecycle-sfctl.md)
* [Windows에서 Linux 개발 환경 준비](service-fabric-local-linux-cluster-windows.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
