---
title: "Azure Service Bus 메시지 처리 아키텍처 개요 | Microsoft Docs"
description: "Azure Service Bus의 메시지 처리 아키텍처를 설명합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/21/2017
ms.author: sethm
ms.openlocfilehash: c3bf541c14e6d869f77ca7d7a6e520bd3489fcad
ms.sourcegitcommit: 6f33adc568931edf91bfa96abbccf3719aa32041
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="service-bus-architecture"></a>Service Bus 아키텍처

이 문서에서는 [Azure Service Bus](https://azure.microsoft.com/services/service-bus/)의 메시지 처리 아키텍처에 대해 설명합니다.

## <a name="service-bus-scale-units"></a>Service Bus 배율 단위

Service Bus는 *배율 단위*로 구성됩니다. 배율 단위는 배포의 단위로, 서비스를 실행하는 데 필요한 구성 요소가 포함되어 있습니다. 각 영역은 하나 이상의 Service Bus 배율 단위를 배포합니다.

Service Bus 네임스페이스는 배율 단위에 매핑됩니다. 배율 단위는 모든 유형의 Service Bus 엔터티(큐, 토픽, 구독)를 처리합니다. Service Bus 배율 단위는 다음 구성 요소로 구성됩니다.

* **게이트웨이 노드 집합.** 게이트웨이 노드는 들어오는 요청을 인증합니다. 각 게이트웨이 노드에는 공용 IP 주소가 있습니다.
* **메시징 브로커 노드 집합.** 메시징 브로커 노드는 메시징 엔터티에 관한 요청을 처리합니다.
* **게이트웨이 저장소 1개.** 게이트웨이 저장소는 이 배율 단위로 정의된 모든 엔터티에 대한 데이터를 저장합니다. 게이트웨이 저장소는 SQL Database 인스턴스에 기반하여 구현됩니다.
* **여러 메시징 저장소.** 메시징 저장소는 이 배율 단위로 정의된 모든 큐, 토픽 및 구독 메시지를 저장합니다. 또한 모든 구독 데이터를 포함합니다. [메시징 엔터티 분할](service-bus-partitioning.md)을 사용하지 않으면 큐 또는 토픽이 하나의 메시징 저장소에 매핑됩니다. 구독은 해당 상위 토픽과 동일한 메시징 저장소에 저장됩니다. Service Bus [프리미엄 메시징](service-bus-premium-messaging.md)을 제외하고, 메시지 저장소는 [SQL Database](https://azure.microsoft.com/services/sql-database/) 인스턴스에 기반하여 구현됩니다.

## <a name="containers"></a>컨테이너

각 메시징 엔터티에는 특정 컨테이너가 할당됩니다. 컨테이너는 하나의 메시징 저장소를 사용하여 이 컨테이너에 대한 모든 관련 데이터를 저장하는 논리적 구성체입니다. 각 컨테이너는 메시징 브로커 노드에 할당됩니다. 일반적으로 메시징 브로커 노드 수보다 더 많은 컨테이너가 있습니다. 따라서 각 메시징 브로커 노드는 여러 컨테이너를 로드합니다. 메시징 브로커 노드로의 컨테이너 배포는 모든 메시징 브로커 노드가 균등하게 로드되도록 구성됩니다. 로드 패턴이 변경(예: 컨테이너 중 하나의 사용량이 많아지는 경우)되거나 메시징 브로커 노드를 일시적으로 사용할 수 없게 되는 경우 컨테이너는 메시징 브로커 노드 간에 재배포됩니다.

## <a name="processing-of-incoming-messaging-requests"></a>들어오는 메시징 요청 처리

클라이언트가 Service Bus에 요청을 보내면 Azure 부하 분산 장치가 모든 게이트웨이 노드로 해당 요청을 라우팅합니다. 게이트웨이 노드는 요청 권한을 부여 합니다. 메시징 엔터티(큐, 토픽, 구독)에 관한 요청인 경우 게이트웨이 노드는 게이트웨이 저장소에서 해당 엔터티를 조회하여 해당 엔터티가 위치한 메시징 저장소를 결정합니다. 그런 다음, 현재 이 컨테이너에 서비스를 제공하는 중인 메시징 브로커 노드를 조회하고 해당 메시징 브로커 노드에 요청을 보냅니다. 메시징 브로커 노드는 요청을 처리하고 컨테이너 저장소에서 엔터티 상태를 업데이트합니다. 그 다음, 메시징 브로커 노드는 응답을 게이트웨이 노드로 다시 보내 원래 요청을 실행한 클라이언트에 적절한 응답을 전송합니다.

![들어오는 메시징 요청 처리](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>다음 단계

Service Bus 아키텍처의 개요를 읽었으므로 자세한 내용은 다음 링크를 참조하세요.

* [Service Bus 메시징 개요](service-bus-messaging-overview.md)
* [Service Bus 기본 사항](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus 큐 시작](service-bus-dotnet-get-started-with-queues.md)


