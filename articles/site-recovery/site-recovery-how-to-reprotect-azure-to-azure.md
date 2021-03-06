---
title: "장애 조치된 Azure Virtual Machines에서 다시 기본 Azure 지역으로 다시 보호하는 방법 | Microsoft Docs"
description: "Azure 지역 간의 VM 장애 조치 후 Azure Site Recovery를 사용하여 역방향으로 컴퓨터를 보호할 수 있습니다. 장애 조치 전에 다시 보호하는 방법에 대해 알아봅니다."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 11/22/2017
ms.author: rajanaki
ms.openlocfilehash: 3e614b6c3c8358585f3b502f301cc659d2088e2f
ms.sourcegitcommit: 651a6fa44431814a42407ef0df49ca0159db5b02
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-to-primary-region"></a>장애 조치된 Azure 지역에서 다시 주 지역으로 다시 보호



>[!NOTE]
>
> Azure Virtual Machines에 대한 Site Recovery 복제는 현재 미리 보기로 제공됩니다.


## <a name="overview"></a>개요
Azure 지역 간에 가상 컴퓨터를 [장애 조치](site-recovery-failover.md)한 경우 가상 컴퓨터는 보호되지 않는 상태가 됩니다. 이러한 가상 컴퓨터를 주 지역으로 다시 가져오려면 먼저 가상 컴퓨터를 보호한 다음 다시 장애 조치해야 합니다. 두 방향 간에 장애 조치 방법에는 차이점이 없습니다. 마찬가지로, 가상 컴퓨터의 보호를 활성화한 후 장애 조치 후 다시 보호와 장애 복구 후 다시 보호 간에도 차이점이 없습니다.
다시 보호 워크플로를 설명하고 혼동을 피하기 위해 보호된 컴퓨터의 기본 사이트를 동아시아 지역으로 참조하고 컴퓨터의 복구 사이트를 동남 아시아 지역으로 참조해 보겠습니다. 장애 조치 중에는 가상 머신이 동남 아시아 지역에서 부팅합니다. 장애 복구 전에 가상 컴퓨터를 다시 동남 아시아에서 동아시아로 다시 보호해야 합니다. 이 문서에서는 다시 보호하는 방법을 설명합니다.

> [!WARNING]
> 가상 머신을 또 다른 리소스 그룹으로 이동했거나 Azure 가상 머신을 삭제하여 [마이그레이션을 완료](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)한 후에는 가싱 머신을 다시 보호하거나 장애 복구(failback)를 수행할 수 없습니다.

다시 보호가 완료되고 보호된 가상 컴퓨터에서 복제하는 경우 가상 컴퓨터에서 장애 조치를 시작하여 동아시아 지역으로 다시 가져올 수 있습니다.

이 문서의 마지막 부분 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에 의견이나 질문을 게시할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
1. 가상 컴퓨터가 커밋되어 있어야 합니다.
2. 대상 사이트(이 예의 경우 동아시아 Azure 지역)가 사용 가능하고 해당 지역에서 새 리소스를 액세스/생성할 수 있어야 합니다.

## <a name="steps-to-reprotect"></a>다시 보호 단계

다음은 기본값을 사용하여 가상 컴퓨터를 다시 보호하는 단계입니다.

1. **자격 증명 모음** > **복제된 항목**에서 장애 조치된 가상 컴퓨터를 마우스 오른쪽 단추로 클릭한 다음 **다시 보호**를 선택합니다. 컴퓨터를 클릭하고 명령 단추에서 **다시 보호**를 선택할 수도 있습니다.

![마우스 오른쪽 단추를 클릭하여 다시 보호](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. 블레이드에 **동남 아시아에서 동아시아로** 보호 방향이 이미 선택되어 있습니다.

![다시 보호 블레이드](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. **리소스 그룹, 네트워크, 저장소 및 가용성 집합** 정보를 검토하고 확인을 클릭합니다. (신규)가 표시된 리소스가 있는 경우 이러한 리소스는 다시 보호의 일부로 생성됩니다.

다시 보호 작업은 먼저 최신 데이터로 대상 사이트(이 예의 경우 동남 아시아)를 시드하고, 완료되면 동남 아시아로 다시 장애 조치하기 전에 델타를 복제합니다.

### <a name="reprotect-customization"></a>다시 보호 사용자 지정
다시 보호하는 동안 추출 저장소 계정 또는 네트워크를 선택하려면 다시 보호 블레이드에 제공된 사용자 지정 옵션을 사용하여 수행할 수 있습니다.

![옵션 사용자 지정](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

다시 보호하는 동안 대상 가상 컴퓨터의 다음 속성을 사용자 지정할 수 있습니다.

![사용자 지정 블레이드](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|속성 |참고 사항  |
|---------|---------|
|대상 리소스 그룹     | 가상 컴퓨터를 만들 대상 리소스 그룹을 변경할 수 있습니다. 다시 보호의 일부로 대상 가상 컴퓨터가 삭제됩니다. 따라서 장애 조치 후 VM을 만들 수 있는 새 리소스 그룹을 선택할 수 있습니다.         |
|대상 Virtual Network     | 다시 보호 작업 동안 네트워크를 변경할 수 없습니다. 네트워크를 변경하려면 네트워크 매핑을 다시 실행합니다.         |
|대상 저장소     | 장애 조치 후 가상 컴퓨터를 만들 저장소 계정을 변경할 수 있습니다.         |
|캐시 저장소     | 복제하는 동안 사용할 캐시 저장소 계정을 지정할 수 있습니다. 기본값으로 계속 진행하는 경우 새 캐시 저장소 계정이 만들어집니다(아직 없는 경우).         |
|가용성 집합     |동아시아의 가상 컴퓨터가 가용성 집합의 일부인 경우 동남 아시아의 대상 가상 컴퓨터에 대한 가용성 집합을 선택할 수 있습니다. 기본적으로 기존 동남 아시아 가용성 집합을 찾아서 사용하려고 합니다. 사용자 지정하는 동안 완전히 새로운 AV 집합을 지정할 수 있습니다.         |


### <a name="what-happens-during-reprotect"></a>다시 보호하는 동안 어떻게 되나요?

보호를 처음 활성화한 후와 마찬가지로 기본값을 사용하는 경우 다음 아티팩트가 생성됩니다.
1. 동아시아 지역에 캐시 저장소 계정이 생성됩니다.
2. 대상 저장소 계정(동남 아시아 VM의 원래 저장소 계정)이 없는 경우 새로 생성됩니다. 동아시아 가상 컴퓨터의 저장소 계정에 "asr"이 접미사로 붙은 이름이 지정됩니다.
3. 대상 AV 집합이 없고 기본값이 새 AV 집합을 만들어야 함을 감지한 경우 다시 보호 작업의 일부로 대상 AV 집합이 생성됩니다. 다시 보호를 사용자 지정한 경우 선택한 AV 집합이 사용됩니다.
4.

다시 보호 작업을 트리거할 때 발생하는 단계 목록은 다음과 같습니다. 이는 대상 쪽 가상 컴퓨터가 존재하는 경우에 해당합니다.

1. 필요한 아티팩트는 다시 보호의 일부로 생성됩니다. 이미 있는 경우 다시 사용됩니다.
2. 대상 쪽(동남 아시아) 가상 컴퓨터가 먼저 꺼집니다(실행 중인 경우).
3. 대상 쪽 가상 컴퓨터의 디스크가 Azure Site Recovery를 통해 컨테이너에 시드 Blob으로 복사됩니다.
4. 그런 다음 대상 쪽 가상 컴퓨터가 삭제됩니다.
5. 시드 Blob은 현재 원본 쪽(동아시아) 가상 컴퓨터에서 복제하는 데 사용됩니다. 따라서 델타만 복제됩니다.
6. 원본 디스크와 시드 Blob 간의 주요 변경 내용이 동기화됩니다. 이 작업을 완료하는 데 약간의 시간이 걸릴 수 있습니다.
7. 다시 보호 작업이 완료되면 정책에 따라 복구 지점을 만드는 델타 복제가 시작됩니다.

> [!NOTE]
> 복구 계획 수준에서 보호할 수 없습니다. 단위 VM 수준에서만 다시 보호할 수 있습니다.

다시 보호 작업이 성공하면 가상 컴퓨터가 보호된 상태가 됩니다.

## <a name="next-steps"></a>다음 단계

가상 컴퓨터가 보호된 상태가 되면 장애 조치를 시작할 수 있습니다. 장애 조치에서는 동아시아 Azure 지역의 가상 컴퓨터를 종료한 다음 동남 아시아 지역 가상 컴퓨터를 만들고 부팅합니다. 이로 인해 응용 프로그램의 가동 중지 시간이 짧습니다. 따라서 응용 프로그램에서 가동 중지 시간을 허용할 수 있는 경우 장애 조치 시간을 선택합니다. 장애 조치를 시작하기 전에 먼저 가상 컴퓨터에 대한 테스트 장애 조치를 수행하여 올바르게 작동하는지 확인하는 것이 좋습니다.

-   [가상 컴퓨터의 테스트 장애 조치를 시작하는 단계](site-recovery-test-failover-to-azure.md)

-   [가상 컴퓨터의 장애 조치를 시작하는 단계](site-recovery-failover.md)
