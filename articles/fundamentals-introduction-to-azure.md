---
title: "Microsoft Azure 소개 | Microsoft Docs"
description: "Microsoft Azure를 처음 사용하나요? 이 제품이 제공하는 서비스에 대한 기본적인 개요와 유용하게 사용되는 예제를 확인하시기 바랍니다."
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 69b8ec86f764077a0e6d029f7c540fa25d022a31
ms.sourcegitcommit: 933af6219266cc685d0c9009f533ca1be03aa5e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="introducing-microsoft-azure"></a>Microsoft Azure 소개
Microsoft Azure는 공용 클라우드용 Microsoft 응용 프로그램 플랫폼입니다.  이 문서의 목적은 사용자가 클라우드 컴퓨팅에 관한 지식 없이도 Azure의 기본 개념을 이해할 수 있도록 기반을 제공하는 것입니다.

**이 문서를 읽는 방법**

Azure는 계속 확장되고 있으므로 너무 많은 서비스를 포함할 수 있습니다.  이 문서에서는 먼저 나열되는 기본 서비스를 시작한 다음 추가 서비스를 계속합니다. 그러나 추가 서비스만 단독으로 사용할 수 없다는 의미는 아니며 단지 기본 서비스가 Azure에서 실행되는 응용 프로그램의 핵심을 구성한다는 것입니다.

**사용자 의견 제공**

Microsoft는 사용자의 의견을 소중하게 생각합니다. 이 문서는 Azure의 개요를 효과적으로 제공하기 위해 작성되었습니다. 그렇지 않다고 생각되면 페이지 아래에 있는 의견 섹션에 의견을 남겨 주세요. 추가되었으면 하는 내용이나 문서의 개선 방법에 대해 자세히 적어 주세요.  

## <a name="the-components-of-azure"></a>Azure 구성 요소
Azure는 [Azure 인포그래픽 정의](https://azure.microsoft.com/documentation/infographics/azure/) 와 같은 다양한 시각적 보조 기능 및 관리 포털의 범주로 서비스를 그룹화합니다. 관리 포털은 전부는 아니지만 대부분의 Azure 서비스를 관리하는 포털입니다.

이 문서에서는 **다른 조직** 을 사용하여 비슷한 기능을 기반으로 하는 서비스에 대해 설명하고 대규모 서비스를 구성하는 중요 하위 서비스에 대해서도 살펴봅니다.  

![Azure 구성 요소](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *그림: Azure는 Azure 데이터 센터에서 실행되는 인터넷 액세스가 가능한 응용 프로그램 서비스를 제공합니다.*

## <a name="management-portal"></a>관리 포털
Azure에는 관리자가 대부분의 Azure 기능(일부 기능 제외)에 액세스하여 관리할 수 있는 [관리 포털](http://manage.windowsazure.com) 이라고 하는 웹 인터페이스가 있습니다.  Microsoft는 일반적으로 이전 버전을 사용 중지하기 전에 베타 버전으로 최신 UI 포털을 릴리스합니다. 최신 버전은 ["Azure Preview 포털"](https://portal.azure.com/)이라고 합니다.

두 포털이 모두 활성 상태이면 보통 오랜 기간 동안 겹침 현상이 발생합니다. 핵심 서비스는 두 포털 모두에 표시되지만, 일부 기능은 두 포털 모두에서 사용할 수 없을 수 있습니다. 최신 서비스는 최신 포털에 먼저 나타날 수 있으며, 이전 서비스와 기능은 이전 버전에만 존재합니다.  따라서 원하는 서비스를 이전 포털에서 찾을 수 없으면 최신 버전을 확인하거나 또는 그 반대로 진행하세요.

## <a name="compute"></a>Compute
클라우드 플랫폼의 기본 역할 중 하나는 응용 프로그램을 실행하는 것입니다. 각 Azure 계산 모델에는 저마다 해야 할 역할이 있습니다.

사용자 응용 프로그램에 맞는 토대를 만들기 위해 이러한 기술을 각자 또는 결합하여 사용할 수 있습니다. 해결하려는 문제가 어떤 것이냐에 따라 접근 방법을 선택하면 됩니다.

### <a name="azure-virtual-machines"></a>Azure Virtual Machines
![Azure Virtual Machines ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*그림: Azure Virtual Machines에서 클라우드의 Virtual Machines 인스턴스를 완벽하게 관리할 수 있습니다.*

표준 이미지 또는 사용자가 제공한 이미지를 사용하여 주문형 가상 컴퓨터를 만드는 기능은 매우 유용합니다. Azure Virtual Machines에서는 일반적으로 IaaS(Infrastructure as a Service)로 알려진 이 방법을 제공합니다. 그림 2에서는 VM(가상 컴퓨터) 실행 방법과 VHD에서 가상 컴퓨터를 만드는 방법을 함께 보여 줍니다.  

VM을 작성하려면 사용할 VHD와 VM의 크기를 지정한 다음  VM을 실행한 시간만큼 결제합니다. VM이 실행되는 시간만 분 단위로 결제하지만 VHD 가용성을 유지하기 위한 최소 저장소 비용도 청구됩니다. Azure는 부팅하는 데 사용할 수 있는 운영 체제를 포함하고 있는 VHD(또는 "이미지")를 모아 놓은 갤러리를 제공합니다. 여기에는 Windows Server, Linux, SQL Server, Oracle 등 Microsoft와 파트너 옵션이 포함됩니다. 자유롭게 VHD와 이미지를 만들어 직접 업로드할 수 있습니다. 데이터만 포함하는 VHD를 업로드한 다음 실행 중인 VM에서 액세스할 수도 있습니다.

VHD를 어디에서 가져오더라도 VM을 실행하는 동안 지속적으로 변경 사항을 저장할 수 있으며, 작업하던 VHD를 가지고 VM을 만드는 경우 이전에 작업했던 부분부터 시작할 수 있습니다. Virtual Machines로 돌린 VHD는 Azure Storage Blob에 저장되며 이 내용은 뒷부분에서 다룹니다.  즉, 하드웨어 및 디스크 오류로 인해 VM을 손실하지 않도록 하는 복제 기능을 갖추게 됩니다. 또한 Azure 밖에서 변경된 VHD도 복사해서 로컬에서 실행할 수 있습니다.

응용 프로그램은 이전에 해당 응용 프로그램을 만든 방법이나 처음부터 만드는 방법에 따라 하나 이상의 Virtual Machines에서 실행됩니다.

다양한 문제를 처리하는데 클라우드 컴퓨팅을 사용하는 것은 매우 일반적이며,

**가상 컴퓨터 시나리오**

1. **개발/테스트** - 이러한 VM을 사용하여 저렴한 비용으로 개발 및 테스트 플랫폼을 만들고 사용을 마치면 플랫폼을 종료할 수 있습니다. 또한 어떤 언어나 라이브러리를 사용해서도 응용 프로그램을 만들고 실행할 수 있습니다. 이러한 응용 프로그램은 Azure가 제공하는 모든 데이터 관리 옵션을 사용할 수 있으며, 하나 이상의 가상 컴퓨터에서 실행되는 SQL Server 또는 다른 DBMS를 사용할 수도 있습니다.
2. **Azure로 응용 프로그램 이동(들어올려서 옮기기)** - "들어올려서 옮기기"는 마치 지게차로 대형 물체를 이동하는 것처럼 응용 프로그램을 이동하는 것을 의미합니다.  로컬 데이터 센터에서 VHD를 "들어올려서" Azure로 "옮긴" 다음 그곳에서 실행합니다.  일반적으로 다른 시스템에 대한 종속성을 제거하기 위해 몇 가지 작업을 수행해야 합니다. 종속성이 너무 많은 경우 옵션 3을 선택할 수도 있습니다.  
3. **데이터 센터 확장** - SharePoint 또는 기타 응용 프로그램을 실행하는 온-프레미스 데이터 센터의 확장으로 Azure VM을 사용하는 것입니다. 이를 지원하기 위해 Azure VM에서 Active Directory를 실행하여 클라우드에 Windows 도메인을 만들 수 있습니다. Azure Virtual Network(나중에 설명)를 사용하여 로컬 네트워크와 Azure의 네트워크를 결합할 수 있습니다.

### <a name="web-apps"></a>Web Apps
![Azure Web Apps ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *그림: Azure Web Apps에서는 기본 웹 서버를 관리하지 않으면서 클라우드에서 웹 사이트 응용 프로그램을 실행합니다.*

클라우드에서 실행하는 가장 일반적인 내용 중 하나는 웹 사이트와 웹 응용 프로그램을 실행하는 것입니다. Azure Virtual Machines에서는 이러한 작업이 허용되지만, 여전히 담당자가 하나 이상의 VM과 기본 운영 체제를 관리해야 합니다. 클라우드 서비스 웹 역할이 이 작업을 수행할 수 있지만 이 역할을 배포하여 관리하는 것도 관리 작업입니다.  다른 사람이 관리를 해주는 웹 사이트를 원한다면 어떨까요?

바로 이것이 Web Apps가 제공하는 정확한 기능입니다. 이 계산 모델은 Azure 관리 포털 및 API를 사용하여 관리되는 웹 환경을 제공합니다. 기존 웹 사이트 응용 프로그램을 변경하지 않고 Web Apps로 이전하거나, 클라우드에 새 웹 사이트 응용 프로그램을 직접 만들 수 있습니다. 웹 사이트가 실행되고 나면 Azure Web Apps의 부하 분산 요청에 따라 동적으로 인스턴스를 추가 또는 제거할 수 있습니다. Azure 웹앱은 한 가상 컴퓨터에 다른 사이트와 함께 웹 사이트를 실행하는 공유 옵션과 한 VM에서 하나의 사이트를 실행하는 표준 옵션을 모두 제공합니다. 또한 표준 옵션을 사용하면 필요에 따라 사용자 인스턴스의 크기(컴퓨팅 기능)를 증가시킬 수 있습니다.

개발을 위해서 Web Apps는 관계형 저장소용 SQL Database 및 Azure Database for MySQL과 함께 .NET, PHP, Node.js, Java 및 Python을 지원합니다. 또한 WordPress, Joomla, Drupal 등의 여러 인기 있는 응용 프로그램을 기본적으로 지원합니다. Azure 웹 사이트의 목표는 경제적이며 확장 가능하고 매우 유용한 플랫폼을 제공하여 공용 클라우드에 웹 사이트와 웹 응용 프로그램을 생성할 수 있도록 하는 것입니다.

**Web Apps 시나리오**

Web Apps는 기업, 개발자, 웹 디자인 회사 등에 유용합니다. 기업에 상태 확인 웹 사이트를 위한 손쉬운 관리, 확장 가능성, 높은 보안, 고도의 가용성 등을 제공하는 솔루션입니다. Website를 설치할 때 Azure Web Apps에서 시작하고, 제공되지 않은 기능이 필요한 경우 Cloud Services로 진행하는 것이 가장 좋습니다. 적합한 옵션을 선택할 수 있도록 돕는 기타 링크에 대해서는 "Compute" 섹션의 끝 부분을 참조하세요.

### <a name="cloud-services"></a>Cloud Services
![Azure Cloud Service](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*그림: Azure Cloud Services는 PaaS(Platform as a Service) 환경에서 확장성이 높은 사용자 지정 코드를 실행할 수 있는 곳입니다.*

다수의 동시 사용자를 지원하면서 관리가 많이 필요하지 않고 가동 중단되지 않는 클라우드 응용 프로그램을 구축한다고 가정합시다. 중견 소프트웨어 공급업체라면 클라우드에 응용 프로그램 중 한 버전을 구축하여 SaaS(Software as a Service)를 도입할 수 있습니다. 빠른 성장을 바라보는 스타트업이라면 소비자 응용 프로그램을 만들 수도 있습니다. Azure에 구축하는 경우 어떤 실행 모델을 사용해야 할까요?

Azure Web Apps를 사용하면 웹 응용 프로그램을 만들 수 있지만 약간의 제약 조건이 따릅니다. 관리자 액세스 권한이 없는 경우 소프트웨어를 임의로 설치할 수 없다는 점이 대표적인 예입니다. Azure Virtual Machines를 사용하면 관리자 액세스 권한 등 유연한 기능을 다양하게 제공하므로 확장 가능한 응용 프로그램을 구축할 때 유용하게 사용할 수 있지만, 안전성 및 관리 측면에서 여러 가지를 직접 처리해야 합니다. 필요한 제어력을 제공하면서도 안정성과 관리 작업을 직접 처리하고 싶다면

Azure Cloud Services가 정답입니다. PaaS(Platform as a Service)의 대표적인 예인 이 기술은 특히 확장 가능하고, 안정적이며, 관리가 적은 응용 프로그램을 지원하도록 설계되었습니다. 클라우드 서비스를 사용하려면 C#, Java, PHP, Python, Node.js 등 선택한 기술을 사용하여 응용 프로그램을 만들어야 합니다. 그렇게 하면 작성한 코드(인스턴스라고 함)가 Windows Server 버전이 실행되는 가상 컴퓨터에서 실행됩니다.

그러나 이러한 VM은 Azure Virtual Machines에서 만든 VM과 구별됩니다. 예를 들면 Azure가 운영 체제 패치를 설치하고 자동으로 새로 패치된 이미지를 사용하는 등 해당 VM을 직접 관리한다는 차이점을 들 수 있습니다. 이는 응용 프로그램이 웹이나 작업자 역할 인스턴스의 상태를 관리하지 않는다는 점을 뜻합니다. 대신 다음 섹션에 설명된 Azure 데이터 관리 옵션 중 하나에서 처리합니다. Azure는 또한 VM을 모니터링하여 오류가 발생하면 VM을 다시 시작합니다. 필요에 따라 자동으로 인스턴스를 더 많이 또는 더 적게 만들도록 클라우드 서비스를 설정할 수 있습니다. 따라서 증가되는 사용량을 관리하고 다시 크기를 조정할 수 있으므로 사용량이 적을 때에는 그에 맞게 결제할 수 있습니다.

인스턴스를 만드는 경우 Windows Server를 기반으로 하는 역할에는 두 가지가 있습니다. 각 역할의 주요 차이점은 웹 역할 인스턴스는 IIS를 실행하지만 작업자 역할 인스턴스는 아니라는 데 있습니다. 하지만 두 가지 모두 같은 방법으로 관리되며, 한 응용 프로그램에서 두 가지를 모두 사용하는 것이 일반적입니다. 웹 역할 인스턴스가 사용자 요청을 수신한 후 이를 처리하도록 작업자 역할 인스턴스에 전달하는 것이 대표적인 예입니다. 응용 프로그램의 크기를 확장 또는 축소하려는 경우 Azure에서 두 역할 인스턴스 중 하나를 더 만들거나 기존 인스턴스를 종료하도록 요청할 수 있습니다. Azure Virtual Machines와 마찬가지로 각 웹 또는 작업자 역할 인스턴스가 실행된 시간에 대한 비용만 청구됩니다.

**Cloud Services 시나리오**

Cloud Services는 Azure Web Apps에서 제공하는 것보다 더 높은 수준으로 플랫폼을 제어하지만 기본 운영 체제는 제어할 필요가 없는 경우 광범위한 확장을 지원하는 데 이상적입니다.

#### <a name="choosing-a-compute-model"></a>Compute 모델 선택
[Azure Web Apps, Cloud Services 및 Virtual Machines 비교](app-service/choose-web-site-cloud-service-vm.md) 페이지에서는 Compute 모델을 선택하는 방법에 대한 자세한 내용을 제공합니다.

## <a name="data-management"></a>데이터 관리
응용 프로그램에는 데이터가 필요하고, 서로 다른 종류의 응용 프로그램에는 서로 다른 종류의 데이터가 필요합니다. Azure는 데이터를 저장하고 관리하는 방법을 다양하게 제공하는 이유가 여기에 있습니다. Azure는 많은 저장소 옵션을 제공하지만 모두 영구 저장소를 위해 설계되었습니다.  이러한 옵션을 사용하면 항상 Azure 데이터 센터에 걸쳐 동기화되는 3개의 복사본이 생성됩니다. Azure에서 지리적 중복성을 사용하여 483km 떨어진 다른 데이터 센터로 백업하도록 설정한 경우에는 6개의 복사본이 생성됩니다.     

### <a name="in-virtual-machines"></a>Virtual Machines에서
Azure Virtual Machines로 만들어진 VM에서 SQL Server 또는 다른 DBMS를 실행할 수 있는 기능으로, 이미 이전에 설명한 내용입니다. 이 옵션은 관계형 시스템에 국한되지 않으며 MongoDB, Cassandra 등과 같은 NoSQL 기술에도 실행할 수 있습니다. 소유한 데이터베이스 시스템을 실행하는 것은 간단(소유한 데이터 센터에서 사용하던 것을 복제)하지만 해당 DBMS 관리가 또한 필요합니다.  다른 옵션에서는 Azure가 더 많은 또는 모든 관리 작업을 처리합니다.

다시 한 번 말하지만, 사용자가 만들거나 업로드한 가상 컴퓨터 및 추가적인 데이터 디스크의 상태는 Blob 저장소(뒷부분에서 논의)를 통해 유지됩니다.  

### <a name="azure-sql-database"></a>Azure SQL Database
![Azure Storage SQL Database](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*그림: Azure SQL Database는 관리되는 관계형 데이터베이스 서비스를 클라우드에서 제공합니다.*

Azure는 관계형 저장소로 추천 SQL Database를 제공합니다. 이름 때문에 혼동하지 마세요. 이 데이터베이스는 Windows Server에서 실행되는 SQL Server에서 제공하는 일반 SQL Database와 다릅니다.  

이전에 SQL Azure라고 불렸던 Azure SQL Database는 관계형 데이터베이스 관리 시스템의 원자성 트랜잭션, 데이터 무결성을 함께 제공하는 여러 사용자의 동시 데이터 액세스, ANSI SQL 쿼리, 친숙한 프로그래밍 모델 등 모든 핵심 기능을 제공합니다. SQL Server와 같이 Entity Framework, ADO.NET, JDBC, 기타 친숙한 데이터 액세스 기술 등을 사용하여 SQL Database에 액세스할 수 있습니다. 또한 SQL Server Management Studio와 같은 SQL Server 도구와 함께 대부분의 T-SQL 언어를 지원합니다. SQL Server(또는 다른 관계형 데이터베이스)에 친숙한 사람은 SQL Database를 쉽게 사용할 수 있을 것입니다.

그러나 SQL Database는 단순히 클라우드에서 제공하는 DBMS가 아니라 PaaS 서비스입니다. 개발자는 데이터와 누가 해당 데이터에 액세스할 수 있는지 계속 제어할 수 있으나, 하드웨어 인프라를 관리하고 자동으로 데이터베이스를 보관하고 운영 체제 소프트웨어를 최신으로 유지하는 등의 단순 관리 작업은 SQL Database가 책임집니다. 또한 SQL Database는 고가용성, 자동 백업, 지정 시간 복원 기능을 제공하며, 여러 지역에 걸쳐 복사본을 복제할 수도 있습니다.  

**SQL Database에 대한 시나리오**

계산 모델을 사용하여 관계형 저장소를 사용하는 Azure 응용 프로그램을 만드는 경우 SQL Database는 좋은 옵션이 될 수 있습니다. 클라우드 외부에서 실행되는 응용 프로그램에서도 사용할 수도 있습니다. 물론 그런 만큼 시나리오가 많은 편이기는 합니다. 예를 들어, 다양한 클라이언트 시스템(데스크 톱, 노트북, 태블릿, 휴대폰 등)에서 SQL Database에 저장된 데이터를 액세스할 수 있습니다. 또한 복제를 통해 기본 제공 고가용성을 제공하기 때문에 SQL Database를 사용하면 가동 중지 시간을 최소화할 수 있습니다.

### <a name="tables"></a>테이블
![Azure Storage 테이블](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*그림: Azure 테이블은 데이터 저장을 위한 플랫 NoSQL 방식을 제공합니다.*

이 기능은 "Azure Storage"라고 하는 대규모 기능의 일부이기 때문에 때때로 다른 용어로 부르기도 합니다. "테이블", "Azure 테이블" 또는 "저장소 테이블"은 모두 같은 기능을 의미합니다.  

이름 때문에 혼동될 수 있지만, 이 기술은 관계형 저장소를 제공하지 않습니다. 사실 키/값 저장소라고 부르는 NoSQL 방식의 하나입니다. Azure 테이블을 사용하면 응용 프로그램을 통해 문자열, 정수, 날짜 등의 다양한 유형 속성을 저장할 수 있습니다. 그런 다음 응용 프로그램에서 해당 그룹의 고유키를 제공하여 속성 그룹을 검색할 수 있습니다. join과 같은 복잡한 계산은 지원하지 않지만, 테이블에서는 입력한 데이터에 빠르게 액세스할 수 있습니다. 또한, 확장이 수월하여 단일 테이블에 테라바이트의 데이터를 저장할 수 있습니다. 구조가 단순한 만큼 테이블은 보통 SQL Database의 관계형 저장소보다 저렴합니다.

**테이블에 대한 시나리오**

입력한 데이터에 빠르게 액세스해야 하지만 대부분의 작업에서 복잡한 SQL 쿼리는 실행하지 않는 Azure 응용 프로그램을 만든다고 가정하겠습니다. 예를 들어 각 고객의 프로필 정보를 저장하는 고객 응용 프로그램을 생각해 봅니다. 작성한 앱의 인기가 높아서 많은 데이터를 처리해야 하지만 실제로는 저장, 검색과 같은 간단한 작업만 필요한 경우가 있습니다. 바로 이럴 때 Azure 테이블이 필요합니다.

### <a name="blobs"></a>Blob
![Azure Storage Blobs](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*그림: Azure Blob은 비구조적 이진 데이터를 제공합니다.*  

Azure Blob("Blob Storage"와 "Storage Blob"은 같은 대상을 의미)은 비구조적 이진 데이터를 저장하도록 설계되었습니다. 테이블 서비스처럼 Blob은 단일 Blob이 최대 1TB(테라바이트)까지 지원되는 저렴한 저장소를 제공합니다. 또한 Azure 응용 프로그램에서 Blob을 통해 Azure 인스턴스에 탑재된 Windows 파일 시스템용 영구적 저장소를 제공하는 Azure 드라이브를 사용할 수도 있습니다. 응용 프로그램에는 일반적인 Windows 파일이 표시되지만 실제 콘텐츠는 Blob에 저장됩니다.

Blob 저장소는 다른 많은 Azure 기능(Virtual Machines 포함)에 사용되므로 특히 사용자의 작업 부담을 줄여 줍니다.

**Blob에 대한 시나리오**

예를 들어 비디오, 광범위한 파일, 기타 이진 정보 등을 저장하는 응용 프로그램에서 간단하고 저렴한 저장소인 Blob을 사용할 수 있습니다. 또한 Blob은 일반적으로 CDN(Content Delivery Network) 등 나중에 다룰 다른 서비스와 함께 사용됩니다.  

### <a name="import--export"></a>가져오기/내보내기
![Azure 가져오기 내보내기 서비스](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*그림: Azure 가져오기/내보내기 서비스는 보다 빠르고 저렴하게 대량 데이터를 가져오거나 내보내기 위해 Azure에 실제 하드 드라이브를 배송하거나 배송받는 기능을 제공합니다.*  

때로 Azure로 대량의 데이터를 이동하는 경우가 있습니다. 며칠 정도 긴 시간이 걸리며 상당한 대역폭을 사용하게 됩니다. 이런 경우 Azure Import/Export를 사용할 수 있습니다. 이 서비스를 통해 Bitlocker 암호화 3.5" SATA 하드 드라이브를 Azure 데이터 센터에 배송하면 Microsoft에서 자동으로 Blob 저장소로 데이터를 전송합니다.  업로드가 완료되면 Microsoft에서 드라이브를 다시 사용자게 배송합니다.  또한 Blob Storage에서 하드 드라이브로 대량의 데이터를 내보내 메일을 통해 전송하도록 요청할 수도 있습니다.

**가져오기/내보내기에 대한 시나리오**

* **대량의 데이터 마이그레이션** - Azure에 대량의 데이터(테라바이트 단위)를 업로드하려는 경우 인터넷을 통한 전송보다 Import/Export 서비스가 보통 훨씬 빠르며 가격도 더 저렴합니다. Blob에 데이터를 저장한 후에는 이 데이터를 테이블 저장소나 SQL Database와 같은 다른 양식으로 처리할 수 있습니다.
* **보관된 데이터 복구** - Import/Export를 사용하면 Microsoft를 통해 Azure Blob Storage에 저장된 대용량 데이터를 보낸 저장 장치에 전송받은 다음 저장 장치를 원하는 위치로 다시 배달할 수 있습니다. 어느 정도 시간이 걸리기 때문에 재해 복구에는 적절한 옵션이 아닙니다. 그러나 빠르게 액세스하지 않아도 되는 보관된 데이터에는 최상의 옵션입니다.

### <a name="file-service"></a>파일 서비스
![Azure File Service](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*그림: Azure 파일 서비스는 클라우드에서 실행 중인 응용 프로그램에 대해 SMB \\\\server\share paths를 제공합니다.*

온-프레미스에서는 \\\\Server\share 형식을 사용하여 SMB(서버 메시지 블록) 프로토콜을 통해 액세스 가능한 대량의 파일 저장소를 사용하는 것이 일반적입니다. 이제 Azure는 클라우드에서 이 프로토콜을 사용하도록 허용하는 서비스를 갖추었습니다. Azure에서 실행되는 응용 프로그램은 이 서비스를 통해 ReadFile 및 WriteFile과 같은 친숙한 파일 시스템을 사용하는 VM 간에 파일을 공유할 수 있습니다. 또한 REST 인터페이스를 통해 파일에 동시에 액세스할 수 있으므로, 가상 네트워크를 설치한 경우에도 온-프레미스에서 공유에 액세스할 수 있습니다. Azure 파일은 Blob service를 기반으로 하므로, Azure Storage에 기본 제공된 가용성, 영속성, 확장성 및 원자성, 일관성, 격리, 지리적 중복성을 동일하게 상속합니다.

**Azure 파일에 대한 시나리오**

* **클라우드로 기존 앱 마이그레이션** - 파일 공유를 사용하여 응용 프로그램의 구성 요소 간에 데이터를 공유하는 온-프레미스 응용 프로그램을 클라우드에 마이그레이션하는 것이 더 쉬워졌습니다. 각 VM은 파일 공유에 연결한 다음 온-프레미스 파일 공유에 있는 것처럼 파일을 읽고 쓸 수 있습니다.
* **공유 응용 프로그램 설정** - 분산 응용 프로그램의 일반적인 패턴은 다양한 가상 컴퓨터에서 액세스할 수 있는 중앙 위치에 구성 파일을 저장하는 것입니다. 이러한 구성 파일을 Azure 파일 공유에 저장하면 모든 응용 프로그램 인스턴스에서 읽을 수 있습니다. 또한 REST 인터페이스를 통해 설정을 관리할 수 있으므로 구성 파일에 대한 전 세계 액세스가 가능합니다.
* **진단 공유** - 로그, 메트릭, 크래시 덤프 등과 같은 진단 파일을 저장하고 공유할 수 있습니다. 이러한 파일을 SMB 및 REST 인터페이스를 통해 사용 가능하도록 설정하면 응용 프로그램에서 진단 데이터를 처리 및 분석하기 위해 다양한 분석 도구를 사용할 수 있습니다.
* **개발/테스트/디버그** - 개발자 또는 관리자가 클라우드의 가상 컴퓨터에서 작업할 경우 보통 도구 또는 유틸리티 집합이 필요합니다. 각 가상 컴퓨터에서 이러한 유틸리티를 설치 및 분산하는 작업은 시간이 많이 걸립니다. Azure 파일을 사용하면 개발자 또는 관리자가 파일 공유에 원하는 도구를 저장하고 어떤 가상 컴퓨터에서든 해당 도구에 연결할 수 있습니다.

## <a name="networking"></a>네트워킹
오늘날 Azure는 전세계에 분산된 많은 데이터 센터에서 실행됩니다. 응용 프로그램을 실행하거나 데이터를 저장할 때 사용할 데이터 센터를 한 개 이상 선택할 수 있습니다. 또한 아래의 서비스를 사용하는 다양한 방식으로 데이터 센터에 연결할 수 있습니다.

### <a name="virtual-network"></a>Virtual Network
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*그림: Virtual Network는 클라우드에서 개인 네트워크를 제공하므로 VPN 프레미스 간 연결을 설정한 경우 여러 서비스가 서로 통신하거나 온-프레미스 리소스와 통신할 수 있습니다.*  

공개 클라우드를 유용하게 사용하는 방법 중 하나는 클라우드를 데이터 센터의 확장으로 생각하는 것입니다.

주문형으로 VM을 만들 수 있기 때문에 더 이상 필요하지 않을 때 제거와 동시에 결제를 중단하여 원할 때만 컴퓨팅 기능을 갖출 수 있습니다. Azure Virtual Machines를 사용하여 SharePoint, Active Directory 및 기타 친숙한 온-프레미스 소프트웨어를 실행하는 VM을 만들 수 있으므로 이 접근 방식은 이미 보유한 응용 프로그램에서 적용할 수 있습니다.

이를 정말 유용하게 활용하려면 사용자가 이러한 응용 프로그램이 원래 데이터 센터에서 실행되고 있는 것처럼 사용할 수 있어야 합니다. Azure Virtual Network가 바로 그러한 서비스를 제공합니다. 관리자는 VPN 게이트웨이 장치를 사용하여 로컬 네트워크와 Azure의 가상 네트워크에 배포된 VM 간에 VPN(가상 사설망)을 설정할 수 있습니다. 클라우드 VM에 자신의 IP v4 주소를 할당하기 때문에 VM이 자신의 네트워크에 있는 것으로 보입니다. 조직에 있는 사용자는 이러한 VM에 포함된 응용 프로그램에 로컬에서 실행되고 있는 것처럼 액세스할 수 있습니다.

사용자에게 적합한 가상 네트워크를 계획 및 생성에 대한 자세한 내용은 [Virtual Network](virtual-network/virtual-networks-overview.md)를 참조하세요.

### <a name="express-route"></a>Express 경로
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*그림: ExpressRoute는 Azure Virtual Network를 사용하지만 공용 인터넷이 아닌 더욱 빠른 전용 회선을 통해 연결을 라우팅합니다.*  

Azure Virtual Network 연결에서 제공할 수 있는 것보다 더 많은 대역폭 또는 보안이 필요한 경우 ExpressRoute를 살펴볼 수 있습니다. 일부 경우에는 ExpressRoute를 통해 비용을 절감할 수도 있습니다. Azure의 가상 네트워크가 필요하지만 Azure와 사이트 간의 링크는 공용 인터넷을 사용하지 않는 전용 연결을 사용합니다. 이 서비스를 사용하려면 네트워크 서비스 공급자 또는 Exchange 공급자와 계약을 맺어야 합니다.

ExpressRoute 연결을 설정하는 데 더 많은 시간과 계획이 필요하므로, 사이트 간 VPN으로 시작한 다음 ExpressRoute 연결로 마이그레이션할 수 있습니다.

ExpressRoute에 대한 자세한 내용은 [ExpressRoute 기술 개요](expressroute/expressroute-introduction.md)를 참조하세요.

### <a name="traffic-manager"></a>Traffic Manager
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*그림: Azure Traffic Manager를 통해 인텔리전스 규칙을 기반으로 서비스로 글로벌 트래픽을 라우팅할 수 있습니다.*

Azure 응용 프로그램이 여러 데이터 센터에서 실행되는 경우 Azure Traffic Manager를 사용하여 사용자 요청을 적절하게 여러 응용 프로그램 인스턴스에 라우팅할 수 있습니다. 또한 인터넷에서 액세스할 수 있는 한 Azure에서 실행되지 않는 서비스로 트래픽을 라우팅할 수 있습니다.  

한 지역의 사용자만 이용하는 Azure 응용 프로그램이 있다면 딱 한 군데의 Azure 데이터 센터에서만 실행될 수도 있을 것입니다. 하지만 전 세계의 사용자들이 이용하는 응용 프로그램은 여러 데이터 센터에서 실행될 가능성이 많습니다. 아마 대부분의 응용 프로그램이 후자에 해당할 것입니다. 이 두 번째 상황에서는 "어떻게 사용자를 적절하게 응용 프로그램 인스턴스에 할당할 것인가?"라는 문제에 직면할 수 있습니다. 대부분의 경우 가장 빠른 응답 시간을 제공하기 위해 각 사용자가 가장 가까운 데이터 센터에 액세스하기를 원할 것입니다. 그러나 응용 프로그램 인스턴스가 오버로드되거나 사용할 수 없게 된다면 어떻겠습니까? 이럴 때에는 사용자 요청을 자동으로 다른 데이터 센터로 리디렉션하면 좋을 것입니다. 이것이 바로 Azure Traffic Manager의 역할입니다.

응용 프로그램 소유자는 사용자 요청을 어떻게 데이터 센터로 리디렉션할지 지정하는 규칙을 정의한 후 Traffic Manager를 사용하여 이러한 규칙을 실행할 수 있습니다. 예를 들어 일반적으로 사용자를 가장 가까운 Azure 데이터 센터로 리디렉션하지만 기본 데이터 센터의 응답 시간이 다른 데이터 센터의 응답 시간을 초과하면 다른 데이터 센터로 이전하도록 설정할 수 있습니다. 사용자가 많으며 전 세계적으로 분산된 응용 프로그램이라면 이러한 문제점을 기본적으로 처리해 주는 서비스가 유용할 것입니다.

Traffic Manager는 DNS(디렉터리 이름 서비스)를 사용하여 사용자를 서비스 끝점으로 라우팅하지만, 연결이 설정되고 나면 추가 트래픽은 Traffic Manager를 통과할 수 없습니다. 그래서 Traffic Manager에서 서비스 통신을 느리게 만들 수 있는 병목 현상이 발생하지 않도록 합니다.

## <a name="developer-services"></a>개발자 서비스
Azure는 개발자 및 IT 전문가가 클라우드에서 응용 프로그램을 만들고 유지할 수 있도록 돕는 많은 도구를 제공합니다.  

### <a name="azure-sdk"></a>Azure SDK
2008년 Azure 첫 번째 시험판 버전에서는 .NET 개발만 지원했습니다. 하지만 이제 Azure 응용 프로그램을 대부분의 언어로 작성할 수 있습니다. 현재 Microsoft는 .NET, Java, PHP, Node.js, Ruby, Python 등의 언어별 SDK를 제공합니다. 또한 C++ 등 모든 언어를 기본적으로 지원하는 일반적인 Azure SDK도 있습니다.  

이러한 SDK는 Azure 응용 프로그램의 구축, 배포, 관리 등을 돕습니다. SDK는 [www.microsoftazure.com](https://azure.microsoft.com/downloads/) 또는 GitHub에 있으며, Visual Studio 및 Eclipse와 함께 사용할 수 있습니다. 또한 Azure는 개발자가 어느 편집기나 개발 환경에서 사용할 수 있는 명령줄 도구를 제공하며, 여기에는 Linux나 Macintosh 시스템의 응용 프로그램을 Azure로 배포하는 도구가 포함됩니다.

Azure 응용 프로그램 빌드를 돕는 것 외에도, 이 SDK는 Azure 서비스를 사용하는 소프트웨어 작성을 돕는 클라이언트 라이브러리를 제공합니다. 예를 들어, Azure Blob을 읽고 쓰는 응용 프로그램을 빌드하거나 Azure 관리 인터페이스를 통해 Azure 응용 프로그램 배포 도구를 만들 수 있습니다.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services는 Azure에서 응용 프로그램을 개발하도록 돕는 다양한 서비스와 관련된 마케팅 이름입니다.

혼동을 피하기 위해 이 서비스는 Visual Studio의 호스티드 또는 웹 기반 버전을 제공하지 않습니다. 따라서 Visual Studio의 로컬 실행 사본이 여전히 필요합니다. 그러나 매우 유용한 다른 많은 도구를 제공합니다.

이 서비스에는 버전 제어 및 작업 항목 추적 기능을 제공하는 Team Foundation Service라고 하는 호스티드 소스 제어 시스템을 포함합니다.  원하는 경우 버전 제어에 Git을 사용할 수 있습니다. 또한 프로젝트에 사용하는 소스 제어 시스템을 달리할 수 있습니다. 세계 어디에서든 액세스 가능한 무제한 개인 팀 프로젝트를 만들 수 있습니다.  

Visual Studio Team Services는 부하 테스팅 서비스를 제공합니다. 클라우드의 VM에서 Visual Studio로 생성된 부하 테스트를 실행할 수 있습니다. 부하 테스트를 원하는 사용자의 총 수를 지정하면 Visual Studio Team Services에서 필요한 에이전트 수를 자동으로 결정하고, 필요한 가상 컴퓨터를 스핀업하고, 부하 테스트를 실행합니다. MSDN 구독자인 경우 매달 부하 테스팅을 할 수 있는 상당한 무료 사용 시간을 받게 됩니다.

또한 Visual Studio Team Services는 연속 통합 빌드, Kanban 보드, 가상 팀 회의실과 같은 기능을 통해 민첩한 개발도 지원합니다.

**Visual Studio Team Services 시나리오**

Visual Studio Team Services는 전 세계적으로 협업해야 하지만 그렇게 할 수 있는 적절한 인프라는 아직 갖추지 못한 회사에 적합한 옵션입니다. 몇 분 안에 설정하고, 소스 제어 시스템을 선택하고 하루 만에 코드 작성과 빌드를 시작할 수 있습니다.  팀 도구는 조정 및 협업을 위한 방법을 제공하며 추가적인 도구는 응용 프로그램을 신속하게 테스트 및 조정하는 데 필요한 분석을 제공합니다.

온-프레미스 시스템을 이미 갖춘 조직은 Visual Studio Team Services에서 새로운 프로젝트를 테스트하여 더 효율적인지 확인할 수 있습니다.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*그림: Application Insights는 라이브 웹 또는 장치 앱의 성능 및 사용 현황을 모니터링합니다.*

모바일 장치, 데스크톱 또는 웹 브라우저에서 실행되는 앱을 게시한 경우 Application Insights는 앱의 작동 방식 및 사용자가 해당 앱으로 수행하는 작업을 알려줍니다. 또한 크래시 및 느린 응답의 수를 계산하고, 해당 수치가 허용하는 임계값을 초과할 경우 경고하고, 문제를 진단하도록 도와줍니다.

새로운 기능을 개발할 때는 사용자의 성공적인 기능 사용 결과를 측정하도록 합니다. 사용 패턴을 분석하여 고객에게 최적으로 작동하는 기능을 이해하고 모든 개발 주기에서 앱을 향상시킵니다.

Azure에 호스트되지만 Application Insights는 Azure 내부 및 외부의 광범위한 앱에 작동합니다. iOS, Android, OSX 및 Windows 응용 프로그램은 물론, J2EE 및 ASP.NET 웹앱을 모두 포괄합니다. Azure의 Application Insights 서비스에서 분석 및 표시되기 위해 앱과 함께 빌드된 SDK에서 원격 분석이 전송됩니다.

보다 구체적인 분석을 원할 경우 원격 분석 스트림을 데이터베이스, Power BI 또는 기타 도구로 내보냅니다.

**Application Insights 시나리오**

앱을 개발 중입니다. 웹앱이나 장치 앱일 수도 있고, 웹 백 엔드가 있는 장치 앱일 수도 있습니다.

* 앱을 게시한 후 또는 부하 테스트 중에 성능을 조정합니다.  Application Insights는 설치된 모든 인스턴스에서 원격 분석을 집계하고, 응답 시간, 요청 및 예외 개수, 종속성 응답 시간 및 기타 성능 표시기에 대한 차트를 제공합니다. 이를 통해 앱 성능을 쉽게 조정할 수 있습니다. 필요한 경우 보다 구체적인 데이터를 보고하기 위해 코드를 삽입할 수 있습니다.
* 라이브 앱에서 문제를 검색하고 진단합니다. 성과 표시기가 허용 가능한 임계값을 초과하거나 못미칠 경우 전자 메일로 경고할 수 있습니다. 예외를 발생시킨 요청을 확인하는 것처럼 특정 사용자 세션을 조사할 수 있습니다.
* 사용 현황을 추적하여 각 새 기능의 성공을 평가합니다. 새 사용자 사례를 디자인할 때는 사용량 및 사용자가 예상 목표를 달성하는지 여부를 측정합니다. Application Insights를 사용하면 웹 페이지 보기와 같은 기본 사용 현황 데이터를 볼 수 있으며 사용자 환경을 보다 자세히 추적하기 위한 코드를 삽입할 수 있습니다.

### <a name="automation"></a>Automation
동일한 수동 프로세스를 반복하는 데 시간을 낭비하고 싶은 사람은 없을 것입니다. Azure Automation은 Azure 환경에서 리소스를 생성, 모니터, 관리 및 배포할 수 있는 방법을 제공합니다.  

Automation은 "runbook"을 사용하며, 이 runbook은 Windows PowerShell 워크플로(단순한 일반 PowerShell 아님)를 사용합니다. Runbook은 사용자 조작 없이 실행됩니다. PowerShell 워크플로를 통해 검사점을 따라 스크립트의 상태를 저장할 수 있습니다. 이렇게 하면 오류가 발생할 경우 처음부터 스크립트를 시작할 필요가 없습니다. 마지막 검사점만 다시 시작하면 됩니다. 따라서 스크립트를 통해 가능한 모든 오류를 처리하도록 설정하는 작업이 상당히 줄어듭니다.

**Automation 시나리오**

Azure Automation은 Azure에서 오류가 발생하기 쉽고 자주 반복되는, 장기적인 수동 작업을 자동화하기 위해 선택할 수 있는 적절한 옵션입니다.

### <a name="api-management"></a>API Management
인터넷에서 API(Application Programmer Interface)를 생성하고 게시하는 것이 응용 프로그램에 서비스를 제공하는 가장 일반적인 방법입니다. 이러한 서비스가 재판매 가능한 경우(예: 날씨 데이터) 조직은 제3자가 유료로 동일한 서비스에 액세스하도록 허용할 수 있습니다. 이러한 서비스를 더 많은 파트너로 확장함에 따라 일반적으로 액세스를 최적화하고 제어해야 합니다.  일부 파트너는 다양한 형식의 데이터를 필요로 할 수 있습니다.

Azure API Management를 통해 조직은 안전하면서 확장 가능한 방식으로 파트너, 직원 및 제3의 개발자에게 API를 쉽게 게시할 수 있습니다. 이 서비스는 다른 API 끝점을 제공하고 실제 끝점을 호출하는 프로젝트 역할을 하면서 캐싱, 변환, 제한, 액세스 제어, 분석 집계 등의 서비스를 제공합니다.

**API Management 시나리오**

어떤 회사에 데이터를 가져오기 위해 중앙 서비스로 콜백해야 하는 장치 집합이 있다고 가정합니다. 이동 중인 모든 트럭에 장치를 설치한 배송 회사를 예로 들 수 있습니다.  특히 이 회사는 배달 시간을 안정적으로 예측하고 업데이트할 수 있도록 자체 트럭을 추적하도록 시스템을 설정하기를 원합니다. 그렇게 하면 보유한 트럭 수를 파악하여 적절히 계획할 수 있기 때문입니다.  각 트럭에는 위치 및 속도 데이터 등을 중앙 위치로 콜백하는 장치가 있어야 합니다.

배송 회사의 고객은 이런 위치 데이터를 통해 이점을 얻을 수 있습니다.  고객은 이 데이터를 사용하여 제품이 어느 정도 이동되었고, 어디에서 정체되고 있으며, 특정 경로를 따라 얼마의 비용이 발생하고 있는지(배송을 위해 결제한 항목과 결합된 경우) 알 수 있습니다. 배송 회사가 이 데이터를 이미 집계한 경우 많은 고객이 그에 대한 비용을 결제할 수 있습니다.  이런 경우 배송 회사는 고객에게 데이터를 제공하는 방법을 마련해야 합니다. 고객에 대한 액세스를 제공한 후에는 데이터의 쿼리 빈도를 제어하지 못할 수 있습니다. 따라서 누가 어떤 데이터에 액세스할 수 있는지에 대한 규칙도 제공해야 합니다. 그리고 이러한 모든 규칙을 외부 API에 기본 제공해야 합니다. 여기가 바로 API Management가 도울 수 있는 지점입니다.  

## <a name="identity-and-access"></a>ID 및 액세스
대부분의 응용 프로그램에는 ID와 관련된 작업이 포함됩니다. 사용자를 식별하면 응용 프로그램에서 해당 사용자와 상호 작용하는 방식을 결정할 수 있습니다. Azure는 ID를 추적할 뿐만 아니라 기존에 사용하던 ID 저장소로 ID를 통합하는 서비스를 제공합니다.

### <a name="active-directory"></a>Active Directory
대부분의 디렉터리 서비스처럼 Azure Active Directory는 사용자와 소속 조직 정보를 저장합니다. 사용자는 사용자 ID를 증명하기 위해 이러한 토큰으로 응용 프로그램에 로그인하고 해당 정보를 제공합니다. 또한 로컬 네트워크에 있는 온-프레미스에서 실행되는 Windows Server Active Directory와 사용자 정보를 동기화할 수 있습니다. Azure Active Directory에서 사용하는 메커니즘이나 데이터 형식이 Windows Server Active Directory와 같지는 않지만 실행하는 기능은 꽤 비슷합니다.

Azure Active Directory가 주로 클라우드 응용 프로그램에서 사용하도록 디자인되었다는 것을 이해하는 것이 중요합니다. 예를 들어 Azure나 다른 클라우드 플랫폼에서 실행하는 응용 프로그램에서 사용할 수 있습니다. 또한 Office 365와 같은 Microsoft 자체 클라우드 응용 프로그램에서도 Azure Active Directory를 사용합니다. 그러나 Azure Virtual Machines와 Azure Virtual Network를 사용하여 자체 데이터 센터를 클라우드로 확장하는 경우 Azure Active Directory는 좋은 선택이 아닙니다. 대신 Virtual Machines에서 Windows Server Active Directory를 실행할 수 있습니다.

Azure Active Directory 정보를 응용 프로그램에서 액세스할 수 있도록 Azure Active Directory에서는 Azure Active Directory Graph라고 하는 RESTful API를 제공합니다. 이 API를 사용하면 어떤 플랫폼에서 실행되는 응용 프로그램이라도 디렉터리 개체와 개체 간 관계에 액세스할 수 있습니다.  예를 들어 인증된 응용 프로그램은 사용자나 소속 그룹, 기타 정보 등에 대해 알기 위해 API를 사용할 수 있습니다. 또한 응용 프로그램에서 사용자 간 관계를 참조할 수 있으므로 사람들 간의 연결 정보를 통해 더욱 적절하게 작동할 수 있습니다.

이 서비스의 다른 기능은 응용 프로그램이 Facebook, Google, Windows Live ID 및 기타 인기 있는 ID 공급자의 ID 정보를 쉽게 사용하도록 해주는 Azure Active Directory Access Control에 있습니다. 응용 프로그램에서 공급자들이 사용하는 다양한 데이터 형식이나 프로토콜을 요청하는 것이 아니라, Access Control이 이 모든 정보를 단일 공용 형식으로 변환합니다. 또한 응용 프로그램에서 하나 이상의 Active Directory 도메인에서의 로그인을 허용할 수 있도록 해줍니다. 예를 들어 SaaS 응용 프로그램을 제공하는 공급업체는 Azure Active Directory Access Control을 사용하여 각 고객의 사용자에게 응용 프로그램에 대한 Single Sign-On 기능을 제공할 수 있습니다.

디렉터리 서비스는 온-프레미스 컴퓨팅의 핵심 토대인 만큼 클라우드에서도 중요한 역할을 맡습니다.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*그림: Multi-Factor Authentication은 응용 프로그램에서 두 개 이상의 ID 형식을 확인할 수 있는 기능을 제공합니다.*

보안은 언제나 중요한 사항입니다. MFA(Multi-factor authentication)는 사용자 본인만 자신의 계정에 액세스하도록 보장하는 데 유용합니다. MFA(2단계 인증 또는 "2FA"라고도 함)를 사용하려면 사용자가 로그인 및 트랜잭션을 위해 다음 3가지 ID 검증 방법 중 2가지를 제공해야 합니다.

* 사용자가 알고 있는 정보(일반적으로 암호)
* 사용자가 보유한 장치(예: 휴대폰과 같이 쉽게 복제되지 않는 신뢰할 수 있는 장치)
* 사용자의 신원 정보(생체 인식)

따라서 사용자가 로그인하면 해당 사용자에게 암호뿐만 아니라 모바일 앱, 전화 통화 또는 문자 메시지를 통해 신분을 확인하도록 요구해야 합니다. 기본적으로, Azure Active Directory는 사용자 로그인의 유일한 인증 방법으로 암호 사용을 지원합니다. MFA SDK를 사용하여 Azure AD 또는 사용자 지정 응용 프로그램 및 디렉터리와 함께 MFA를 사용할 수 있습니다. 또한 Multi-Factor Authentication 서버를 통해 온-프레미스 응용 프로그램과 함께 사용할 수도 있습니다.

**MFA 시나리오**

무단 진입 시 재정적 또는 지적 재산권의 측면에서 높은 비용을 초래할 수 있는 은행 로그인 및 소스 코드 액세스와 같은 중요 계정에 대한 로그인 보호   

## <a name="mobile"></a>모바일
모바일 장치용 앱을 만드는 경우 Azure를 사용하면 상당한 사용자 지정 코드를 사용하지 않고도 클라우드에 데이터를 저장하고, 사용자를 인증하고, 푸시 알림을 보낼 수 있습니다.

Azure 서비스를 사용하면 기본 서비스 구성 요소를 작성하는 데 드는 시간을 절감하면서 특히 Virtual Machines, Cloud Services 또는 Web Apps를 사용하여 모바일 앱을 위한 백 엔드를 빌드할 수 있습니다.

### <a name="mobile-apps"></a>Mobile Apps
![Mobile Apps](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*그림: Mobile Apps는 모바일 장치와 상호 작용하는 응용 프로그램에 일반적으로 필요한 기능을 제공합니다.*

Azure Mobile Apps는 모바일 응용 프로그램용 백엔드를 빌드할 때 시간을 절약할 수 있는 유용한 기능을 많이 제공합니다. 따라서 SQL Database에 저장된 데이터를 간단히 제공하고 관리할 수 있습니다. 서버 쪽 코드를 사용하면 Blob 저장소나 MongoDB와 같은 추가 데이터 저장소 옵션을 쉽게 사용할 수 있습니다. Mobile Apps는 알림을 지원합니다. 물론 특정한 경우에는 다음에 설명하는 Notification Hubs를 사용할 수도 있습니다.  또한 이 서비스에는 모바일 응용 프로그램이 작업을 완료하기 위해 호출할 수 있는 REST API도 있습니다. Mobile Apps를 사용하면 Microsoft 및 Active Directory뿐만 아니라 Facebook, Twitter, Google 등 잘 알려진 기타 ID 공급자를 통해서도 사용자를 인증할 수 있습니다.   

Service Bus나 작업자 역할과 같은 기타 Azure 서비스를 사용하여 온-프레미스 시스템에 연결할 수도 있습니다. 또한 Azure Store의 타사 추가 기능(예: 이메일용 SendGrid)을 사용하여 추가 기능을 제공할 수 있습니다.

Android, iOS, HTML/JavaScript, Windows Phone, Windows 스토어 등 네이티브 클라이언트 라이브러리를 통해 모든 주요 모바일 플랫폼에서 사용할 수 있는 앱을 쉽게 개발할 수 있습니다. REST API를 통해 여러 플랫폼에서 앱에 Mobile Services 데이터 및 인증 기능을 사용할 수 있습니다. 단일 모바일 서비스를 사용하여 복수의 클라이언트 앱을 지원할 수 있으며 장치 간에 일관적인 사용자 경험을 제공할 수 있습니다.

Azure에서 광대한 확장을 지원하므로, 앱이 대중성을 얻어감에 따라 늘어나는 트래픽을 처리할 수 있습니다.  문제 해결과 성능 관리를 위해 모니터링 및 로깅이 지원됩니다.

### <a name="notification-hubs"></a>Notification Hubs
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*그림: Notification Hubs는 모바일 장치와 상호 작용하는 응용 프로그램에 일반적으로 필요한 기능을 제공합니다.*

Azure Mobile Apps에서 알림을 수행하는 코드를 작성할 수도 있지만 Notification Hubs는 몇 분 안에 고도로 사용자 지정된 푸시 알림을 수백만 개 브로드캐스트하도록 최적화되었습니다.  통신 회사나 장치 제조업체와 같은 세세한 사항을 걱정할 필요는 없습니다. 단일 API 호출로 개인 또는 수백만 명의 사용자를 대상으로 할 수 있습니다.

Notification Hubs는 모든 백엔드에 대해 작동하도록 설계되었습니다. 임의의 공급자 또는 온-프레미스 백엔드에서 실행하는 클라우드의 사용자 지정 백엔드인 Azure Mobile Apps를 사용할 수 있습니다.

**알림 허브 시나리오** 플레이어 간 턴 방식의 모바일 게임을 작성한 경우 플레이어 1이 턴을 완료하면 플레이어 2에게 알려줘야 할 수 있습니다. 필요한 게 그것뿐이라면 Mobile Apps를 사용하면 됩니다. 100,000명의 사용자가 게임을 플레이하며 모든 사람에게 시간이 중요한 무료 제안을 전송하려는 경우 Notification Hubs가 더 나은 옵션입니다.

짧은 대기 시간으로 뉴스 속보, 스포츠 행사 및 제품 발표 알림을 수백만 명의 사용자에게 보낼 수 있습니다. 기업에서는 직원에게 시간이 중요한 새로운 내용(예: 잠재 고객)을 알릴 수 있으므로 직원은 최신 정보를 얻기 위해 메일이나 기타 응용 프로그램을 지속적으로 확인하지 않아도 됩니다. 또한 Multi-Factor Authentication에 필요한 1회용 암호도 전송할 수 있습니다.

## <a name="back-up"></a>백업
모든 기업은 데이터를 백업 및 복원해야 합니다. Azure를 사용하여 클라우드 또는 온-프레미스든 응용 프로그램을 백업하고 복원할 수 있습니다. Azure는 백업 유형에 따라 유용한 여러 옵션을 제공합니다.

### <a name="site-recovery"></a>사이트 복구
Azure 사이트 복구(이전의 Hyper-V Recovery Manager)를 사용하면 사이트 간에 복제 및 복구를 조정하여 중요 응용 프로그램을 보호할 수 있습니다. 사이트 복구는 보조 사이트, 호스터의 사이트 또는 Azure에 대한 Hyper-v, VMWare 또는 SAN 기반 응용 프로그램을 보호하고 보조 위치를 직접 구축하고 관리하는 비용 및 복잡성을 방지하는 기능을 제공합니다. Azure는 데이터 및 통신을 암호화하고 저장 데이터에 대한 암호화를 사용하는 옵션도 제공합니다.

이 기능은 서비스의 상태를 지속적으로 모니터하여 기본 데이터 센터에서 사이트 중단 시 순차적인 서비스 복구를 자동화합니다. 가상 컴퓨터를 오케스트레이션된 방식으로 가져오므로 다계층 작업을 위해서도 서비스를 빠르게 복원할 수 있습니다.

사이트 복구는 Hyper-V 복제본, System Center, SQL Server Always On 등의 기존 기술에서도 작동합니다. 자세한 내용은 [Azure 사이트 복구 개요](site-recovery/site-recovery-overview.md) 를 확인합니다.

### <a name="azure-backup"></a>Azure Backup
![Azure Backup](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*그림: Azure Backup은 온-프레미스 Windows Server에서 클라우드로 데이터를 백업합니다.*  

Azure Backup은 Windows Server를 실행하는 온-프레미스 서버에서 클라우드로 데이터를 백업합니다. Windows Server 2012, Windows Server 2012 Essentials 또는 System Center 2012 - Data Protection Manager의 백업 도구에서 직접 백업을 관리할 수 있습니다. 또는 전문 백업 에이전트를 사용할 수 있습니다.

전송 전에 백업이 암호화되며 Azure에 암호화된 상태로 저장되고 사용자가 업로드한 인증서로 보호되므로 데이터가 더 안전합니다. 서비스는 Azure Storage의 메커니즘과 동일한 고가용성의 중복 데이터 보호를 사용합니다.  전체 백업 또는 증분 백업을 실행하여 파일 및 폴더를 정기적으로 또는 즉시 백업할 수 있습니다. 클라우드로 데이터를 백업한 후에는 권한 있는 사용자가 서버로 백업을 쉽게 복구할 수 있습니다. 또한 구성 가능한 데이터 보존 정책, 데이터 압축 및 데이터 전송 제한을 제공하므로 데이터 저장 및 전송 비용을 관리할 수 있습니다.

**Azure Backup에 대한 시나리오**

Windows Server 또는 System Center를 이미 사용하는 경우 Azure 백업은 서버 파일 시스템, 가상 컴퓨터 및 SQL Server 데이터베이스를 백업하는 데 사용할 수 있는 자연스러운 솔루션입니다.  이 솔루션은 암호화된, 스파스 및 압축 파일에 대해 작업합니다. 몇 가지 제한 사항이 있으므로 먼저 [Azure Backup 필수 구성 요소를 확인](http://technet.microsoft.com/library/dn296608.aspx) 해야 합니다.

## <a name="messaging-and-integration"></a>메시징 및 통합
어떤 작업에서건 코드는 자주 다른 코드와 상호 작용하게 됩니다.  상황에 따라서는 기본 대기 중인 메시징이 가장 필요해질 수 있으며, 다른 경우에는 좀 더 복잡한 상호 작용이 필요할 수 있습니다. Azure는 이러한 문제를 해결하기 위해 약간 다른 방법을 제공합니다. 그림 5에서 이러한 옵션을 설명합니다.

### <a name="queues"></a>큐
![Azure Service Bus Relay](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*그림: 큐는 응용 프로그램 내의 부분 간 연결을 느슨하게 하여 크기 조정을 용이하게 해줍니다.*  

큐는 간단한 아이디어입니다. 응용 프로그램이 어떤 메시지를 큐에 보내면 다른 응용 프로그램이 그 메시지를 읽습니다. 응용 프로그램에 이처럼 단순한 서비스만 필요하다면 Azure 큐가 가장 적합한 선택이 될 것입니다.

시간 경과에 따라 Azure가 증가하는 방식으로 인해 Azure Storage 큐 및 Service Bus 큐는 유사한 큐 서비스를 제공합니다. 둘 중 하나를 사용하려는 이유는 기술 문서인 [Azure 큐 및 Service Bus 큐 - 비교 및 대조](http://msdn.microsoft.com/library/azure/hh767287.aspx)에 나와 있습니다.  많은 시나리오에서 두 가지 서비스가 모두 작동합니다.

**큐 시나리오**

현재 큐의 일반적인 사용 예 중 하나는 웹 역할 인스턴스와 작업자 역할 인스턴스가 동일한 Cloud Services 응용 프로그램 내에서 통신하는 것입니다.

예를 들어 비디오를 공유하는 Azure 응용 프로그램을 작성한다고 가정합시다. 응용 프로그램은 PHP 코드로 구성되고 웹 역할에서 실행되어 사용자가 비디오를 업로드하고 볼 수 있도록 해 주며 업로드한 비디오를 다양한 형식으로 변환해주는 C#으로 구현된 작업자 역할과 함께 실행됩니다.

웹 역할 인스턴스가 사용자로부터 새 비디오를 받으면 해당 비디오를 Blob에 저장하고 큐를 통해 새 비디오를 어디서 찾을 수 있는지 작업자 역할로 메시지를 보냅니다. 임의의 작업자 역할 인스턴스가 큐에서 메시지를 읽어 백그라운드에서 필요한 비디오 변환 작업을 수행합니다.

이러한 방법으로 응용 프로그램을 구조화하면 비동기적으로 처리할 수 있고 웹 역할 인스턴스와 작업 역할 인스턴스 수가 각기 달라질 수 있기 때문에 응용 프로그램의 확장이 수월합니다. 또한 큐 크기를 트리거로 사용하여 작업 역할 수를 확장하고 축소할 수 있습니다. 값이 높아질수록 더 많은 역할을 추가할 수 있습니다. 값이 낮아질수록 실행 중인 역할 수를 줄여서 비용을 절감할 수 있습니다.  

웹 또는 작업자 역할을 사용하지 않더라도 응용 프로그램 내의 많은 다른 부분들 간에 이러한 동일한 패턴을 사용할 수 있습니다.  이를 통해 주문 및 처리 시간에 따라 큐의 양 측면에 있는 부분의 크기를 크거나 작게 조정할 수 있습니다.

### <a name="service-bus"></a>Service Bus
클라우드, 자체 데이터 센터, 모바일 장치 등 어디에서 실행되더라도 응용 프로그램에는 상호 작용이 필요합니다. Azure Service Bus의 목표는 응용 프로그램이 어디에서나 데이터를 교환하고 실행될 수 있도록 만드는 데 있습니다.

앞서 설명한 큐(일대일) 외에, Service Bus는 다른 통신 방법도 제공합니다.

#### <a name="service-bus-relay"></a>Service Bus Relay
![Azure Service Bus Relay](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*그림: Service Bus Relay는 방화벽의 다른 쪽에 있는 응용 프로그램 간에 통신을 허용합니다.*

Service Bus를 사용하면 릴레이 서비스를 통해 직접 통신이 가능하며, 방화벽을 통해 안전하게 상호 작용하는 방법을 제공합니다. Service Bus는 로컬보다는 클라우드에서 호스트된 끝점을 통해 메시지를 교환하여 응용 프로그램 통신을 하도록 해줍니다.

**Service Bus Relay 시나리오**

Service Bus를 통해 통신하는 응용 프로그램은 Azure 응용 프로그램 또는 다른 클라우드 플랫폼에서 실행되는 소프트웨어일 수 있습니다. 클라우드 외부에서 실행되는 응용 프로그램도 있을 수 있습니다. 예를 들어 자체 데이터 센터 내부의 컴퓨터에서 예약 서비스를 구현하는 항공사를 생각해 보겠습니다. 항공사에서는 셀프 체크인 기기, 예약 에이전트 터미널, 더 나아가 고객 스마트폰 등에서 체크인할 수 있도록 이 서비스를 많은 클라이언트에게 제공할 필요가 있습니다. 이를 위해 Service Bus를 사용하여 다양한 응용 프로그램 간에 느슨한 결합의 상호 작용을 만들 수 있습니다.

#### <a name="service-bus-topics-and-subscriptions"></a>Service Bus 토픽 및 구독
![Azure Service Bus Topics](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *그림: Service Bus 토픽을 통해 여러 앱에서 메시지를 게시하고 다른 응용 프로그램은 특정 조건을 충족하는 메시지를 받도록 신청할 수 있습니다.*

Service Bus는 토픽 및 구독이라고 하는 게시-구독 메커니즘을 제공합니다. 게시-구독을 사용하면 응용 프로그램이 메시지를 토픽으로 보낼 수 있고, 다른 응용 프로그램이 이 토픽 구독을 만들 수 있습니다. 이렇게 하면 응용 프로그램 집합에서 일대다 통신을 할 수 있어 동일한 메시지를 여러 수신자가 읽을 수 있게 됩니다.

**Service Bus 토픽 및 구독 시나리오**

언제든 모두 중요한 많은 메시지가 있지만 다운스트림 시스템마다 이러한 통신 중 서로 다른 일부만을 수신 대기하도록 설정하는 경우 Service Bus 토픽 및 구독이 적절한 옵션입니다.

### <a name="biztalk-services"></a>BizTalk Services
![BizTalk Services](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *그림: BizTalk Services는 클라우드에서 XML 메시지 형식을 변환하는 기능을 제공합니다.*

때로 서로 다른 메시징 형식을 사용하여 통신하는 시스템을 연결해야 하는 경우가 있습니다. 기업에서는 공통 표준을 사용할 수 있는 경우에도 다양한 데이터베이스 스키마 및 XML 메시징 형식을 사용하는 것이 일반적입니다. 사용자 지정 코드를 상당량 작성하지 않고 BizTalk Server 온-프레미스를 사용하여 다양한 시스템을 통합할 수 있습니다.  Azure BizTalk Services는 동일한 서비스를 클라우드에서 제공합니다. 사용한 만큼만 결제하므로 온-프레미스에서 보유하는 크기에 대해 걱정할 필요가 없습니다.

**BizTalk Services 시나리오**

B2B(Business-to-Business) 상호 작용에는 보통 이 유형의 변환이 필요합니다.  예를 들어 항공기 제조 회사에서 다양한 부품 공급자에게서 부품을 주문해야 합니다. 협력 부품 공급자는 많아질 예정입니다.  이러한 주문은 자동으로 항공기 제조사 시스템에서 공급자 시스템으로 직접 이동됩니다.  핵심 시스템 및 메시지 형식을 변경하기를 원하는 기업은 없지만 이러한 형식이 동일한 경우도 매우 드뭅니다. BizTalk Services는 메시지를 가져가서 두 가지 방법으로 새로운 형식 간에 변환할 수 있습니다. 더 많은 제어력을 원하는 주체가 누구인지와 필요한 변환의 양에 따라 항공기 공급자가 변환을 위한 작업을 하거나 다양한 공급자가 작업을 수행할 수 있습니다.     

## <a name="compute-assistance"></a>Compute 지원
Azure는 항상 실행하지 않아도 되는 서비스에 대한 지원을 제공합니다.  

### <a name="scheduler"></a>Scheduler
![Azure Scheduler](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*그림: Azure Scheduler는 특정 기간 동안 특정 시간에 작업을 예약하는 방법을 제공합니다.*

때로 특정 시간에만 응용 프로그램을 실행하면 되는 경우가 있습니다. Azure에서, 응용 프로그램이 연중무휴로 실행하며 데이터를 처리하도록 하는 대신 이런 유형의 앱에 대한 비용을 절감할 수 있습니다. Azure Scheduler를 통해 시간 간격이나 일정에 따라 응용 프로그램을 실행해야 할 시기를 예약할 수 있습니다. 이렇게 하면 안정적이며 네트워크, 컴퓨터 및 데이터 센터 오류가 발생할 경우에도 프로세스가 실행되는지 확인할 수 있습니다. Scheduler REST API를 사용하여 이러한 작업을 관리합니다.

예약된 알람이 발생하면 Scheduler에서 HTTP 또는 HTTPS 메시지를 특정 끝점으로 보내거나 저장소 큐에 메시지를 넣을 수 있습니다.  따라서 응용 프로그램에서 액세스 가능한 끝점을 포함하거나 저장소 큐를 모니터하도록 설정해야 합니다. 그런 다음, 응용 프로그램이 메시지를 받으면 프로그래밍된 작업을 수행할 수 있습니다.

**Scheduler 시나리오**

* 응용 프로그램 작업 반복: 한 예로, 트위터에서 데이터를 정기적으로 가져오고 정규 피드로 데이터를 수집해 넣는 서비스가 있을 수 있습니다.
* 일일 유지 관리: 로그 처리 또는 잘라내기, 백업 및 기타 일시적인 예약 작업
* 밤에 실행되는 작업
* 일별 로그 잘라내기, 백업 수행, 기타 유지 관리 작업 등의 웹 응용 프로그램 작업. 예를 들어 관리자가 향후 9개월간 매일 오전 1시에 데이터베이스를 백업하도록 선택할 수 있습니다.

Scheduler API를 통해 작업 컬렉션 및 예약된 작업을 프로그래밍 방식으로 만들고, 업데이트하고, 삭제하고, 보고, 관리할 수 있습니다.

## <a name="performance"></a>성능
성능은 항상 응용 프로그램에 중요합니다. 응용 프로그램은 같은 데이터에 반복하여 액세스하는 경향이 있습니다. 성능을 향상하는 한 가지 방법은 가져오는 시간을 최소화하기 위해 데이터 복사본을 응용 프로그램 가까운 곳에 보관하는 것입니다. Azure는 이를 위해 다양한 서비스를 제공합니다.

### <a name="azure-caching"></a>Azure 캐싱
![Azure Caching](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **그림: Azure 응용 프로그램은 메모리에 데이터를 캐시하고 많은 작업 역할에 걸쳐 분할할 수도 있습니다.**

Azure의 데이터 관리 서비스(SQL Database, 테이블, Blob 등)에 저장된 데이터에는 비교적 빠르게 액세스할 수 있습니다. 하지만 메모리 내에 저장된 데이터에 액세스하면 속도가 더 빨라집니다. 자주 액세스하는 데이터의 메모리 내 복사본을 보관할 때 응용 프로그램의 성능이 향상되는 이유가 여기에 있습니다. Azure의 메모리 내 캐싱을 사용하면 이러한 성능 향상을 이룰 수 있습니다.

Cloud Services 응용 프로그램은 영구적 저장소에 액세스할 필요 없이 이 캐시에 데이터를 저장한 다음 직접 가져올 수 있습니다. 캐시는 응용 프로그램 VM 내에 유지 관리될 수도 있고 캐싱 전용 VM이 제공될 수도 있습니다. 어느 경우든지 캐시는 포함된 데이터와 함께 Azure 데이터 센터에 있는 여러 VM에 분산될 수 있습니다.

Azure에는 시간에 따라 전환된 다양한 캐시 기술이 많이 있습니다. 도입된 순서대로 말하면 공유 캐시와 In-Role 캐시, 관리된 캐시, Redis 캐시가 있습니다. 공유 캐싱은 이전 기술이므로 이 기술을 사용하여 새 구현을 만들 필요가 없습니다. 관리된 캐시는 In-Role 캐시와 동일한 기능을 갖지만 Azure 관리 포털 외부에서 관리되는 서비스와 같습니다. Redis 캐시는 미리 보기 상태에 있습니다. Redis 구현은 최대 기능 수를 포함하며 새 캐싱 코드를 쓸 때 권장됩니다.

**Azure 캐시 시나리오**

제품 카탈로그를 반복적으로 읽는 응용 프로그램에서 이러한 캐싱을 사용하면 필요한 데이터를 더 빨리 사용할 수 있어서 더욱 좋은 효과를 얻을 수 있을 것입니다. 이 기술은 또한 읽기/쓰기 뿐만 아니라 읽기 전용 데이터로 사용할 수 있는 잠금 기능을 지원합니다. 또한 ASP.NET 응용 프로그램에서 구성만 변경하면 이 서비스를 사용하여 세션 데이터를 저장할 수 있습니다.

### <a name="content-delivery-network"></a>Content Delivery Network
![Azure CDN](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **그림: 전 세계 사이트에서 Blob의 복사본을 캐시할 수 있습니다.**

전 세계 사용자가 액세스할 Blob 데이터를 저장한다고 가정합니다. 최신 월드컵 경기 비디오, 드라이버 업데이트, 인기 있는 전자책 등이 그 예가 될 수 있습니다. 데이터 복사본을 여러 Azure 데이터 센터에 저장하면 도움이 되겠지만 사용자가 매우 많은 경우에는 충분하지 않을 수 있습니다. 더 좋은 성능을 원한다면 Azure CDN을 사용해 보세요.

CDN은 전 세계에 수십 개의 사이트를 보유하고 있으며 각각 Azure Blob의 복사본을 저장하는 기능을 수행할 수 있습니다. 처음에는 전 세계 일부 지역에 있는 사용자가 특정 Blob에 액세스하면, Blob 안의 정보는 Azure 데이터 센터에서 해당 지역의 CDN 저장소로 복사해 오게 됩니다. 그런 후 해당 지역에서 액세스하면 CDN에 캐시된 Blob 복사본을 사용할 수 있으므로 가장 가까운 Azure 데이터 센터에서 데이터를 수신할 필요가 없습니다. 결과적으로 전 세계 어느 곳이든지 사용자가 자주 액세스하는 데이터에 빠르게 액세스하게 됩니다.

**CDN 시나리오**

Media Services와 함께 CDN을 사용하여 전 세계에 동영상을 제공하는 것이 일반적입니다. 동영상은 일반적으로 대용량이며 상당한 대역폭을 요구합니다.  Media Services는 이 페이지의 다른 부분에서 다룹니다.

## <a name="big-data-and-big-compute"></a>빅 데이터 및 빅 Compute
### <a name="hdinsight-hadoop"></a>HDInsight(Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **그림: HDInsight는 대용량 데이터의 일괄 처리를 지원합니다.**

수년간 관계형 DBMS에 기본 제공되는 데이터 웨어하우스에 저장된 관계형 데이터에 대해 대규모의 데이터 분석이 진행되어 왔습니다. 이러한 종류의 비즈니스 분석은 여전히 중요하고 앞으로도 그럴 것입니다. 그러나 분석하려는 데이터가 너무 커서 관계형 데이터베이스로 처리할 수 없다면 어떻게 하시겠습니까? 그리고 데이터베이스가 관계형이 아니라면 어떻겠습니까? 데이터 센터에 있는 서버 로그, 센서로부터 제공되는 기록 이벤트 데이터 등이 그 예입니다. 이것이 바로 빅데이터의 문제이며 여기에는 새로운 방식이 필요합니다.

현재 빅데이터 분석에 사용하는 지배적인 기술은 Hadoop입니다. 이 Apache 오픈 소스 프로젝트 기술에서는 HDFS(Hadoop Distributed File System)를 사용하여 데이터를 저장한 다음, 데이터 분석을 위해 개발자가 MapReduce 작업을 생성합니다. HDFS는 데이터를 여러 서버에 분산한 후 대량의 MapReduce 작업을 각 서버에서 실행하여 빅데이터를 병렬로 처리합니다.

HDInsight는 Azure의 Apache Hadoop 기반의 서비스 이름입니다. HDInsight를 통해 HDFS는 클러스터에 데이터를 저장하고 여러 VM에 걸쳐 데이터를 분산할 수 있습니다. 이러한 VM에 MapReduce 작업 논리를 배포합니다. 온-프레미스 Hadoop과 마찬가지로 더 좋은 성능을 위해 데이터를 로컬(작업하는 논리와 데이터가 같은 VM 사용)에서 병렬로 처리합니다. HDInsight는 또한 Blob을 사용하는 ASV(Azure Storage Vault)에 데이터를 저장합니다.  ASV를 사용하면 HDInsight 클러스터를 사용하지 않을 때 제거하고 데이터를 계속 클라우드에 보관할 수 있기 때문에 비용을 절약할 수 있습니다.

HDinsight는 Hadoop 에코시스템뿐 아니라 Hive, Pig 등과 같은 기타 구성 요소를 지원합니다. Microsoft는 전통적 BI 도구를 사용하여 HDInsight로 생산된 데이터 작업을 쉽게 만들기 위해 Excel에서 사용할 수 있는 HiveODBC 어댑터와 데이터 탐색기 등의 구성 요소를 제공합니다.

### <a name="high-performance-computing-big-compute"></a>HPC(고성능 컴퓨팅)(빅 Compute)
클라우드 플랫폼을 사용하는 가장 좋은 방법 중 하나는 HPC(고성능 컴퓨팅) 및 기타 "빅 Compute" 응용 프로그램을 실행하는 것입니다. 이러한 예에는 업계 표준 MPI(Message Passing Interface)뿐 아니라 소위 말하는 병렬 응용 프로그램(재무 위험 모델)도 사용하도록 빌드된 전문 엔지니어링 응용 프로그램이 포함됩니다.

빅 Compute의 핵심은 많은 컴퓨터에 코드를 동시에 실행하는 것입니다. Azure에서 이것은 많은 가상 컴퓨터를 동시에 실행하여 문제를 해결하기 위해 모두 병렬로 작동하는 것을 의미합니다. 이를 위해서는 리소스 및 응용 프로그램 예약, 즉 작업을 인스턴스에 분산하는 방법이 필요합니다. Microsoft의 무료 HPC 팩 및 기타 계산 클러스터 솔루션은 Azure 계산 및 인프라 서비스를 활용하여 온-프레미스 계산 클러스터에 필요할 때 용량을 추가하거나 클라우드에서 완전히 빅 Compute 응용 프로그램을 실행하면서 Azure에서 적절히 수행할 수 있습니다.

Azure는 다양한 응용 프로그램의 요구 사항을 충족하는 CPU, 메모리, 디스크 용량 및 기타 특성의 다양한 구성을 갖춘 광범위한 VM 인스턴스 크기를 제공합니다. 최근에 소개된 A8 및 A9 인스턴스는 고속, 멀티 코어 CPU 및 대량의 메모리를 포함하고 있으므로 많은 계산 집약적인 작업 및 특히 병렬 MPI 응용 프로그램에서 적절히 작동합니다. 특정 구성에서 인스턴스는 클라우드에서 병렬 MPI 응용 프로그램의 최대 효율성을 위한 RDMA(원격 직접 메모리 액세스) 기술을 포함하는, 대기 시간이 짧고 처리량이 높은 응용 프로그램 네트워크를 활용합니다.

또한 Azure는 빅 Compute 응용 프로그램 개발자 및 파트너에게 계산 기능, 서비스, 아키텍처 선택 사항 및 개발 도구의 완전한 집합을 제공합니다. Azure는 수천 개의 계산 코어로 확장할 수 있는 전문 데이터 워크플로와 작업 및 태스크 일정 예약과 관련된 사용자 지정 빅 Compute 워크플로를 지원합니다.

## <a name="media"></a>미디어
![Azure Media Services](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **그림: Media Services는 동영상이나 기타 미디어를 전 세계 고객에게 제공하는 응용 프로그램을 위한 플랫폼입니다.**

오늘날 비디오는 인터넷 트래픽의 큰 부분을 차지하고 있고 그 비율은 앞으로 더 늘어날 것입니다. 웹에서 비디오를 제공하는 과정은 단순하지 않습니다. 인코딩 알고리즘, 사용자 화면 해상도 등 여러 가지 변수가 포함되어 있기 때문입니다. 또한 토요일 밤처럼 많은 사람이 온라인 동영상을 시청하는 주문 피크 시간대가 뚜렷한 편이기도 합니다.

인기도를 고려할 때 수많은 새 응용 프로그램이 비디오 기능을 포함하는 것은 안전한 투자로 볼 수 있을 것입니다. 모든 응용 프로그램이 같은 문제들을 해결해야 한다고 해서 당면한 문제들을 각자 해결한다는 것은 좋은 생각이 아닙니다. 많은 응용 프로그램이 사용할 공용 솔루션을 제공하는 플랫폼을 만드는 것이 더 효율적입니다. 또한 이 플랫폼을 클라우드에 구축하는 데는 명확한 장점이 있습니다. 종량제 기반에서 폭넓게 사용할 수 있으며, 비디오 응용 프로그램이 종종 겪는 주문 가변성 문제를 처리할 수 있습니다.

Azure Media Services가 이 문제를 해결해 줍니다. Azure 미디어 서비스는 비디오나 다른 미디어를 사용하여 응용 프로그램을 작성하고 실행하는 사람들의 편의를 위해 클라우드 구성 요소 집합을 제공합니다.

그림에서 알 수 있듯이 Media Services에서는 비디오 및 기타 미디어를 사용하는 응용 프로그램을 위한 구성 요소 집합을 제공합니다. 여기에는 비디오를 Media Services(Azure Blob에 저장됨)로 업로드하는 미디어 수집 구성 요소, 다양한 비디오와 오디오 형식을 지원하는 인코딩 구성 요소, 디지털 권한 관리를 제공하는 콘텐츠 보호 구성 요소, 비디오 스트림에 광고를 넣는 구성 요소, 스트리밍 구성 요소 등이 있습니다. 또한 Microsoft 파트너가 플랫폼을 위한 구성 요소를 제공할 수 있으며, Microsoft에서 파트너 대신 이를 분산하고 요금을 청구해 줍니다.

이 플랫폼을 사용하는 응용 프로그램은 Azure나 다른 서비스에서 실행할 수 있습니다. 예를 들어 비디오 제작 업체용 데스크톱 응용 프로그램에서는 사용자가 비디오를 Media Services에 올리게 한 후 다양한 방법으로 비디오를 처리하도록 할 수 있습니다. 반대로 Azure에서 실행되는 클라우드 기반 콘텐츠 관리 서비스에서는 Media Services가 직접 비디오를 처리하고 분산할 수 있습니다. 어디서 무엇을 실행하든지 각 응용 프로그램은 필요한 구성 요소를 선택하고 RESTful 인터페이스를 통해 구성 요소에 액세스합니다.

각 응용 프로그램은 결과물을 분산하기 위해 Azure CDN 또는 다른 CDN을 사용할 수 있으며, 간단하게 직접 사용자에게 보낼 수도 있습니다. 어떤 방법으로든 배포된 후에는 Media Services를 사용하여 작성된 비디오를 다양한 클라이언트 시스템(Windows, Macintosh, HTML 5, iOS, Android, Windows Phone, Flash, Silverlight 등)에서 사용할 수 있습니다. 이 서비스는 최신 미디어 응용 프로그램을 개발에 편의를 제공하기 위해 제공됩니다.

**참조**

미디어 서비스 방식에 대해 보다 시각적으로 확인하려면 [Azure Media Services Poster][Azure Media Services Poster]를 다운로드하세요.

## <a name="commerce"></a>상거래
SaaS(Software as a Service)의 인기로 응용 프로그램 개발 방법이 혁신적으로 달라지고 있습니다. 이는 응용 프로그램을 판매하는 방법도 달라진다는 의미입니다. SaaS 응용 프로그램은 클라우드에 있으므로 잠재 고객은 온라인에서 솔루션을 찾는 고객이 될 것입니다. 또한 이러한 변경은 응용 프로그램뿐 아니라 데이터에도 적용됩니다. 상거래 가능한 데이터 집합을 위한 공간으로 클라우드는 어떨까요? Microsoft는 [Azure Marketplace](https://azure.microsoft.com/marketplace/)를 통해 두 문제를 모두 해결했습니다.

![Azure Commerce](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **그림: Azure Marketplace 및 Azure Store를 통해 Azure 응용 프로그램 및 상용 데이터 집합을 찾아서 구매하고 Azure 응용 프로그램의 일부로 사용할 수 있습니다.**

이 두 가지 사이에 다른 점은 Marketplace는 Azure 관리 포털 외부에 있지만 스토어는 포털 내부에서 액세스할 수 있다는 데 있습니다. 잠재 고객은 요구를 충족하는 Azure 응용 프로그램을 찾기 위해 검색할 수 있습니다. 고객은 인구 통계 데이터, 경제 데이터, 지리적 데이터 등뿐만 아니 상거래 데이터 집합을 검색할 수 있습니다. 원하는 것을 발견하면 해당 공급업체를 통해 액세스하거나, Marketplace 또는 스토어 웹 위치에서 직접 액세스하거나, 관리 포털에서 액세스할 수도 있습니다. 또한 응용 프로그램에서 Marketplace에 Bing Search API를 사용하여 웹 검색 결과에 액세스할 수도 있습니다.

**상거래 시나리오**

SendGrid는 메일을 보낼 수 있는 Azure 스토어의 응용 프로그램입니다. 이 응용 프로그램은 안정적인 배달 및 통계와 같은 추가 기능을 제공합니다.  이러한 인프라를 직접 빌드하는 대신 이 응용 프로그램 및 관련 서비스를 구매할 수 있습니다.  

## <a name="getting-started"></a>시작하기
이제 Azure의 전체적인 모습에 대해 배워 보았습니다. 다음 단계에서는 첫 Azure 응용 프로그램을 작성해 보겠습니다. 사용할 언어를 선택한 후 [적절한 SDK로](/downloads/) 시작해 보세요. 클라우드 컴퓨팅은 새로운 표준입니다. 지금 시작하세요.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
