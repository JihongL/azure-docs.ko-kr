---
title: "Azure SQL Database를 사용하는 분할된 다중 테넌트 데이터베이스 SaaS 앱 배포 | Microsoft Docs"
description: "Azure SQL Database를 사용하여 SaaS 패턴을 보여 주는 분할된 Wingtip Tickets SaaS 다중 테넌트 데이터베이스 응용 프로그램을 배포하고 탐색합니다."
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: billgib;MightyPen
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: sstein
ms.openlocfilehash: 1ef4355f7234bc6a534d21a57fa52b480983b99b
ms.sourcegitcommit: f847fcbf7f89405c1e2d327702cbd3f2399c4bc2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2017
---
# <a name="deploy-and-explore-a-sharded-multi-tenant-application-that-uses-azure-sql-database"></a>Azure SQL Database를 사용하는 분할된 다중 테넌트 응용 프로그램 배포 및 탐색

이 자습서에서는 Wingtip Tickets라는 샘플 SaaS 다중 테넌트 데이터베이스 응용 프로그램을 배포하고 탐색합니다. Wingtip 앱은 SaaS 시나리오 구현을 간소화하는 Azure SQL Database의 기능을 보여 주도록 설계되었습니다.

이 Wingtips 구현에는 분할된 다중 테넌트 데이터베이스 패턴이 사용됩니다. 분할은 테넌트 식별자를 기준으로 합니다. 테넌트 데이터는 테넌트 식별자 값에 따라 특정 데이터베이스에 배포됩니다. 지정된 데이터베이스에 포함된 테넌트 수에 관계없이 테이블 스키마에 테넌트 식별자가 포함된다는 점에서 모든 데이터베이스는 다중 테넌트입니다. 

이 데이터베이스 패턴을 사용하여 각 분할 또는 데이터베이스에 하나 이상의 테넌트를 저장할 수 있습니다. 각 데이터베이스를 여러 테넌트에서 공유하여 최저 비용에 대해 최적화할 수 있습니다. 또는 각 데이터베이스에 하나의 테넌트만 저장하여 격리에 대해 최적화할 수 있습니다. 최적화는 각 특정 테넌트에 대해 개별적으로 선택할 수 있습니다. 테넌트가 처음 저장될 때 선택할 수 있고 나중에 변경할 수도 있습니다. 응용 프로그램은 어떤 방식으로도 잘 작동하도록 설계되었습니다.

#### <a name="app-deploys-quickly"></a>빠르게 앱 배포

다음 배포 섹션에서는 **Azure에 배포** 단추를 제공합니다. 단추를 누르면 5분 후에 Wingtip 앱이 완전히 배포됩니다. Wingtip 앱은 Azure 클라우드에서 실행되고 Azure SQL Database를 사용합니다. Wingtip은 Azure 구독에 배포됩니다. 개별 응용 프로그램 구성 요소를 사용할 수 있는 전체 액세스 권한이 있습니다.

응용 프로그램은 세 개의 샘플 테넌트에 대한 데이터를 사용하여 배포됩니다. 테넌트는 하나의 다중 테넌트 데이터베이스에 함께 저장됩니다.

누구나 [GitHub 리포지토리][link-github-wingtip-multitenantdb-55g]에서 Wingtip Tickets에 대한 C# 및 PowerShell 소스 코드를 다운로드할 수 있습니다.

#### <a name="learn-in-this-tutorial"></a>이 자습서에서 알아보기

> [!div class="checklist"]

> - Wingtip SaaS 응용 프로그램을 배포하는 방법.
> - 응용 프로그램 소스 코드 및 관리 스크립트를 가져올 위치.
> - 앱을 구성하는 서버 및 데이터베이스 정보.
> - *카탈로그*를 통해 테넌트가 데이터에 매핑되는 방법.
> - 새 테넌트를 프로비전하는 방법.
> - 앱에서 테넌트 활동을 모니터링하는 방법.

이 초기 배포 시 생성되는 일련의 관련 자습서를 이용할 수 있습니다. 자습서에서는 다양한 SaaS 디자인 및 관리 패턴을 살펴봅니다. 이 자습서를 진행하는 동안 제공된 스크립트를 단계별로 수행하여 다양한 SaaS 패턴 구현 방법을 확인하는 것이 좋습니다.

## <a name="prerequisites"></a>필수 조건

이 자습서를 수행하려면 다음 필수 조건이 완료되었는지 확인합니다.

- 최신 Azure PowerShell SDK가 설치되어 있습니다. 자세한 내용은 [Azure PowerShell 시작][link-azure-get-started-powershell-41q]을 참조하세요.

## <a name="deploy-the-wingtip-tickets-app"></a>Wingtip Tickets 앱 배포

1. 다음 **Azure에 배포** 단추를 클릭합니다.
    - Wingtip Tickets SaaS 배포 템플릿이 포함된 Azure Portal이 열립니다. 이 템플릿에는 새 리소스 그룹의 이름 및 앱의 다른 배포와 이 배포를 구별하는 ‘user’ 값이 매개 변수 값으로 필요합니다. 다음 단계에서는 이러한 매개 변수 값을 설정하는 방법을 자세히 설명합니다.
        - 나중에 구성 파일에 필요하므로 사용할 정확한 값을 기록해 두어야 합니다.

    [![Azure에 배포 단추.][image-deploy-to-azure-blue-48d]][link-aka-ms-deploywtp-mtapp-52k]

2. 배포에 필요한 매개 변수 값을 입력합니다.

    > [!IMPORTANT]
    > 일부 인증 및 서버 방화벽 설정은 데모를 이용하기 위해 의도적으로 보호되지 않습니다. **새 리소스 그룹 만들기**를 선택하고, 기존 리소스 그룹, 서버 또는 풀은 사용하지 마세요. 이 응용 프로그램이나 여기에서 만든 리소스를 프로덕션에 사용하지 마세요. 관련된 결제를 중지하려면 응용 프로그램을 완료할 때 이 리소스 그룹을 삭제합니다.

    리소스 이름에는 소문자, 숫자 및 하이픈만 사용하는 것이 가장 좋습니다.

    - **리소스 그룹** - **새로 만들기**를 선택한 후 리소스 그룹의 **이름**(대/소문자 구분)을 입력합니다.
        - 리소스 그룹 이름의 모든 문자는 소문자를 사용하는 것이 좋습니다.
        - 대시를 추가하고 이니셜을 더한 다음 숫자를 추가하는 것이 좋습니다(예: *wingtip-af1*).
        - 드롭다운 목록에서 **위치**를 선택합니다.
    - **사용자** - 이니셜에 숫자를 더한 짧은 **사용자** 값을 선택하는 것이 좋습니다(예: *af1*).

3. **응용 프로그램을 배포**합니다.

    - 사용 약관에 동의하려면 클릭합니다.
    - **구매**를 클릭합니다.

4. **알림**(검색 상자 오른쪽의 벨 아이콘)을 클릭하여 배포 상태를 모니터링합니다. Wingtip 앱을 배포하는 데는 5분 정도 걸립니다.

   ![배포 성공](media/saas-multitenantdb-get-started-deploy/succeeded.png)

## <a name="download-and-unblock-the-management-scripts"></a>관리 스크립트 다운로드 및 차단 해제

응용 프로그램이 배포되는 동안 응용 프로그램 소스 코드 및 관리 스크립트를 다운로드합니다.

> [!IMPORTANT]
> zip 파일이 외부 원본에서 다운로드되고 추출될 때 Windows에서 실행 가능한 콘텐츠(스크립트, dll)를 차단할 수 있습니다. Zip 파일에서 스크립트를 추출할 경우 다음 단계에 따라 추출하기 전에 .zip 파일을 차단 해제하세요. .zip 파일을 차단 해제하면 스크립트를 실행할 수 있습니다.

1. [WingtipTicketsSaaS-MultiTenantDb GitHub 리포지토리](https://github.com/Microsoft/WingtipTicketsSaaS-MultiTenantDb)로 이동합니다.
2. **복제 또는 다운로드**를 클릭합니다.
3. **ZIP 다운로드**를 클릭하고 파일을 저장합니다.
4. **WingtipTicketsSaaS-MultiTenantDb-master.zip** 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
5. **일반** 탭에서 **차단 해제**를 선택하고 **적용**을 클릭합니다.
6. **확인**을 클릭합니다.
7. 파일의 압축을 풉니다.

스크립트는 *..\\WingtipTicketsSaaS-MultiTenantDb-master\\Learning Modules\\* 폴더에 있습니다.

## <a name="update-the-configuration-file-for-this-deployment"></a>이 배포에 대한 구성 파일 업데이트

스크립트를 실행하기 전에 **UserConfig.psm1**에서 *리소스 그룹* 및 *사용자* 값을 설정합니다. 이러한 변수를 배포 중에 설정한 동일한 값으로 설정합니다.

1. *PowerShell ISE*에서 ...\\Learning Modules\\*UserConfig.psm1*을 엽니다.
2. 배포에 대한 특정 값(줄 10 및 11에서만)으로 *ResourceGroupName* 및 *Name*을 업데이트합니다.
3. 변경 내용을 저장합니다.

이 파일에 설정된 값은 모든 스크립트에서 사용되므로 정확한 정보가 중요합니다. 앱을 다시 배포할 경우 다른 리소스 그룹 및 사용자 값을 선택해야 합니다. 그런 다음 새 값으로 UserConfig를 업데이트합니다.

## <a name="run-the-application"></a>응용 프로그램 실행

이 앱에서는 이벤트를 개최하는 콘서트 홀, 재즈 클럽, 스포츠 클럽 등의 장소를 보여 줍니다. 장소는 간단한 방법으로 이벤트를 나열하고 티켓을 판매할 수 있도록 Wingtip 플랫폼의 고객(또는 테넌트)으로 등록됩니다. 각 장소에는 다른 테넌트와 격리되어 독립적으로 해당 이벤트를 관리 및 나열하고 티켓을 판매하는 맞춤형 웹앱이 있습니다. 내부적으로 각 테넌트의 데이터는 기본적으로 분할된 다중 테넌트 데이터베이스에 저장됩니다.

중앙 **이벤트 허브**는 특정 배포에 있는 테넌트의 링크 목록을 제공합니다.

1. 웹 브라우저에서 *이벤트 허브*를 엽니다.
    - http://events.wingtip.&lt;사용자&gt;.trafficmanager.net &nbsp; *(배포의 사용자 값으로 바꿈)*

    ![Events Hub](media/saas-multitenantdb-get-started-deploy/events-hub.png)

2. *이벤트 허브*에서 **Fabrikam Jazz Club**을 클릭합니다.

   ![이벤트](./media/saas-multitenantdb-get-started-deploy/fabrikam.png)

들어오는 요청의 배포를 제어하기 위해 앱에서는 [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)를 사용합니다. 테넌트와 관련된 이벤트 페이지의 경우 테넌트 이름이 URL에 포함됩니다. 또한 URL에는 특정 User 값이 다음과 같은 형식으로 포함됩니다.

- http://events.wingtip.&lt;사용자&gt;.trafficmanager.net/*fabrikamjazzclub*
 
이벤트 앱이 URL에서 테넌트 이름을 구문 분석하고 이를 해시하여 [분할된 데이터베이스 맵 관리](sql-database-elastic-scale-shard-map-management.md)를 사용하는 카탈로그에 액세스하기 위한 키를 만듭니다. 카탈로그는 테넌트의 데이터베이스 위치에 키를 매핑합니다. **이벤트 허브**는 카탈로그에 등록된 모든 테넌트를 나열합니다. **이벤트 허브**는 URL을 구성하기 위해 카탈로그의 확장 메타데이터를 사용하여 각 매핑과 연결된 테넌트의 이름을 검색합니다.

프로덕션 환경에서는 일반적으로 CNAME DNS 레코드를 만들어 [회사 인터넷 도메인](../traffic-manager/traffic-manager-point-internet-domain.md)이 트래픽 관리자 프로필을 가리키도록 합니다.

## <a name="start-generating-load-on-the-tenant-databases"></a>테넌트 데이터베이스에서 부하 생성 시작

이제 앱이 배포되었으므로 작동해 보겠습니다. *Demo-LoadGenerator* PowerShell 스크립트는 각 테넌트에 대해 실행 중인 워크로드를 시작합니다. 많은 SaaS 앱상의 실제 부하는 일반적으로 간헐적이고 예측할 수 없습니다. 이 유형의 부하를 시뮬레이트하기 위해 생성기는 모든 테넌트에 분산된 부하를 생성합니다. 부하에는 임의 간격으로 발생하는 각 테넌트에 대한 임의 버스트가 포함됩니다. 부하 패턴이 나타나는 데는 몇 분 정도 걸리므로 부하를 모니터링하기 전에 생성기를 최소한 3~4분 실행하는 것이 가장 좋습니다.

1. *PowerShell ISE*에서 ...\\Learning Modules\\Utilities\\*Demo-LoadGenerator.ps1* 스크립트를 엽니다.
2. **F5**를 눌러 스크립트를 실행하고 부하 생성기를 시작합니다(지금은 기본 매개 변수 값을 그대로 사용).

> [!IMPORTANT]
> *Demo-LoadGenerator.ps1* 스크립트는 부하 생성기가 실행되는 다른 PowerShell 세션을 엽니다. 부하 생성기는 이 세션에서 각 테넌트에 대해 하나씩 백그라운드 부하 생성 작업을 호출하는 포그라운드 작업으로 실행됩니다.

포그라운드 작업이 시작된 후에는 작업 호출 상태로 유지됩니다. 이 작업은 이후에 프로비전되는 새 테넌트에 대한 추가 백그라운드 작업을 시작합니다.

PowerShell 세션을 닫으면 모든 작업이 중지됩니다.

다른 매개 변수 값을 사용하도록 부하 생성기 세션을 다시 시작할 수 있습니다. 이 경우 PowerShell 생성 세션을 닫은 다음 *Demo-LoadGenerator.ps1*을 다시 실행합니다.

## <a name="provision-a-new-tenant-into-the-sharded-database"></a>새로운 테넌트를 분할된 데이터베이스로 프로비전

초기 배포 시에는 *Tenants1* 데이터베이스에 세 개의 샘플 테넌트가 포함됩니다. 또 다른 테넌트를 만들어 이것이 배포된 응용 프로그램에 어떻게 영향을 미치는지 확인해 보겠습니다. 이 단계에서는 신속하게 새 테넌트를 만들 수 있습니다.

1. *PowerShell ISE*에서 ...\\Learning Modules\Provision and Catalog\\*Demo-ProvisionTenants.ps1*을 엽니다.
2. **F5** 키를 눌러 스크립트를 실행합니다(지금은 기본값을 그대로 사용).

   > [!NOTE]
   > 대부분의 Wingtip Tickets SaaS 스크립트에서는 *$PSScriptRoot*를 사용하여 폴더 탐색을 허용하거나, 다른 스크립트를 호출하거나, 모듈을 가져옵니다. 이 변수는 **F5** 키를 눌러 전체적으로 스크립트를 실행할 경우에만 평가됩니다.  선택 내용을 강조 표시하고 실행(**F8**)하면 오류가 발생할 수 있으므로 스크립트를 실행할 때는 **F5** 키를 누르세요.

새로운 Red Maple Racing 테넌트가 *Tenants1* 데이터베이스에 추가되고 카탈로그에 등록됩니다. 새 테넌트의 티켓 판매 *이벤트* 사이트가 브라우저에 열립니다.

![새 테넌트](./media/saas-multitenantdb-get-started-deploy/red-maple-racing.png)

*이벤트 허브*를 새로 고치면 이제 목록에 새 테넌트가 나타납니다.

## <a name="provision-a-new-tenant-in-its-own-database"></a>새로운 테넌트를 자체 데이터베이스에서 프로비전

분할된 다중 테넌트 모델을 사용하면 다중 테넌트 데이터베이스에서 다른 테넌트가 포함된 데이터베이스에서 새 테넌트를 프로비전할지 아니면 자체 데이터베이스에서 테넌트를 프로비전할지 선택할 수 있습니다. 자체 데이터베이스의 테넌트는 자체 데이터를 다른 테넌트의 데이터에서 격리하는 것이 좋습니다. 격리를 사용하면 다른 테넌트와 독립적으로 해당 테넌트의 성능을 관리할 수 있습니다. 또한 격리된 테넌트의 경우 데이터를 이전 시간으로 복원하는 것이 더 쉽습니다. 다중 테넌트 데이터베이스에 평가판 고객 또는 정규 고객을 배치하고 개별 데이터베이스에 프리미엄 고객을 배치할 수 있습니다. 각각 테넌트가 하나만 포함된 많은 데이터베이스를 만들 경우 모든 데이터베이스를 탄력적 풀에서 함께 관리하여 리소스 비용을 최적화할 수 있습니다.  

이번에는 자체 데이터베이스에서 다른 테넌트를 프로비전합니다.

1. ...\\Learning Modules\\Provision and Catalog\*Demo-ProvisionTenants.ps1*에서 *$TenantName*을 **Salix Salsa**로 수정하고, *$VenueType*을 **dance**로 수정하고, *$Scenario*를 **2**로 수정합니다.

2. **F5** 키를 눌러 스크립트를 다시 실행합니다.
    - 이 F5 키를 누르면 새 테넌트가 별도의 데이터베이스에서 프로비전됩니다. 데이터베이스 및 테넌트가 카탈로그에 등록됩니다. 그러면 브라우저가 테넌트의 이벤트 페이지로 열립니다.

   ![Salix Salsa 이벤트 페이지](./media/saas-multitenantdb-get-started-deploy/salix-salsa.png)

   - 페이지 아래쪽으로 스크롤합니다. 배너에 테넌트 데이터가 저장된 데이터베이스 이름이 표시됩니다.

3. 이벤트 허브를 새로 고치면 이제 목록에 새 테넌트가 나타납니다.



## <a name="explore-the-servers-and-tenant-databases"></a>서버 및 테넌트 데이터베이스 탐색

이제 배포된 리소스 중 일부를 살펴봅니다.

1. [Azure Portal](http://portal.azure.com)에서 리소스 그룹 목록으로 이동합니다. 응용 프로그램을 배포할 때 만든 리소스 그룹을 엽니다.

   ![리소스 그룹](./media/saas-multitenantdb-get-started-deploy/resource-group.png)

2. **catalog-mt&lt;USER&gt;** 서버를 클릭합니다. 카탈로그 서버에는 *tenantcatalog* 및 *basetenantdb*라는 두 개의 데이터베이스가 포함되어 있습니다. *basetenantdb* 데이터베이스는 빈 템플릿 데이터베이스입니다. 다중 테넌트 또는 단일 테넌트에만 사용되는지에 관계없이 이 데이터베이스를 복사하여 새 테넌트 데이터베이스를 만듭니다.

   ![카탈로그 서버](./media/saas-multitenantdb-get-started-deploy/catalog-server.png)

3. 리소스 그룹으로 돌아가서 테넌트 데이터베이스가 있는 *tenants1-mt* 서버를 선택합니다.
    - tenants1 데이터베이스는 원래 세 개의 테넌트와 사용자가 추가한 첫 번째 테넌트가 저장된 다중 테넌트 데이터베이스입니다. 50 DTU 표준 데이터베이스로 구성됩니다.
    - **salixsalsa** 데이터베이스에는 Salix Salsa dance 장소가 유일한 테넌트로 포함됩니다. 기본적으로 50개의 DTU가 있는 표준 버전 데이터베이스로 구성됩니다.

   ![테넌트 서버](./media/saas-multitenantdb-get-started-deploy/tenants-server.png)


## <a name="monitor-the-performance-of-the-database"></a>데이터베이스의 성능 모니터링

몇 분 동안 부하 생성기를 실행한 경우 Portal에 기본 제공되는 데이터베이스 모니터링 기능 중 몇 가지를 확인하기 시작할 정도의 충분한 원격 분석을 이용할 수 있습니다.

1. **tenants1-mt&lt;USER&gt;** 서버로 이동하고 **tenants1**을 클릭하여 네 개의 테넌트가 포함되어 있는 데이터베이스의 리소스 사용률을 확인합니다. 각 테넌트에는 로드 생성기로부터 산발적인 과부하가 발생할 수 있습니다.

   ![tenants1 모니터링](./media/saas-multitenantdb-get-started-deploy/monitor-tenants1.png)

   DTU 사용률 차트는 다중 테넌트 데이터베이스가 많은 테넌트에서 예측할 수 없는 워크로드를 어떻게 지원할 수 있는지 적절하게 설명합니다. 이 경우 부하 생성기는 각 테넌트에 약 30개 DTU의 산발적인 부하를 적용합니다. 이 부하는 50 DTU 데이터베이스의 60% 사용률과 같습니다. 60%를 초과하는 최대값은 동시에 두 개 이상의 테넌트에 부하가 적용될 경우 발생합니다.

2. **tenants1-mt&lt;USER&gt;** 서버로 이동하고 **salixsalsa** 데이터베이스를 클릭하여 하나의 테넌트만 포함된 이 데이터베이스에 대한 리소스 사용률을 확인합니다.

   ![salixsalsa 데이터베이스](./media/saas-multitenantdb-get-started-deploy/monitor-salix.png)

부하 생성기는 각 테넌트가 있는 데이터베이스에 상관없이 각 테넌트에 유사한 부하를 적용하고 있습니다. **salixsalsa** 데이터베이스에 하나의 테넌트만 있는 경우 데이터베이스가 여러 테넌트가 포함된 데이터베이스보다 훨씬 높은 부하를 감당할 수 있음을 확인할 수 있습니다. 

> [!NOTE]
> 부하 생성기에서 생성된 부하는 설명을 위해 제공됩니다.  다중 테넌트 및 단일 테넌트 데이터베이스에 할당된 리소스 및 다중 테넌트 데이터베이스에서 호스트할 수 있는 테넌트 수는 응용 프로그램의 실제 워크로드 패턴에 따라 달라집니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음에 대해 알아보았습니다.

> [!div class="checklist"]

> - Wingtip Tickets SaaS 다중 테넌트 데이터베이스 응용 프로그램을 배포하는 방법
> - 앱을 구성하는 서버 및 데이터베이스 정보
> - *카탈로그*를 사용하여 데이터에 매핑된 테넌트
> - 다중 테넌트 데이터베이스 및 단일 테넌트 데이터베이스로 새 테넌트를 프로비전하는 방법.
> - 풀 사용률을 검토하여 테넌트 작업을 모니터링하는 방법
> - 샘플 리소스를 삭제하여 관련 결제를 중지하는 방법

이제 [프로비전 및 카탈로그 자습서](sql-database-saas-tutorial-provision-and-catalog.md)를 사용해 보세요.



## <a name="additional-resources"></a>추가 리소스

- 다중 테넌트 SaaS 응용 프로그램에 대해 알아보려면 [*다중 테넌트 SaaS 응용 프로그램을 위한 디자인 패턴*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)을 참조하세요.








<!--  Link references.

A [series of related tutorials] is available that build upon this initial deployment.
[link-wtp-overivew-jumpto-saas-tutorials-97j]: saas-multitenantdb-wingtip-app-overview.md#sql-database-wingtip-saas-tutorials

-->

[link-aka-ms-deploywtp-mtapp-52k]: http://aka.ms/deploywtp-mtapp


[link-azure-get-started-powershell-41q]: https://docs.microsoft.com/powershell/azure/get-started-azureps

[link-github-wingtip-multitenantdb-55g]: https://github.com/Microsoft/WingtipTicketsSaaS-MultiTenantDB/





<!--  Image references.

[image-deploy-to-azure-blue-48d]: http://aka.ms/deploywtp-mtapp "Button for Deploy to Azure."

-->

[image-deploy-to-azure-blue-48d]: media/saas-multitenantdb-get-started-deploy/deploy.png

