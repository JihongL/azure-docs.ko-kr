---
title: "자습서: Salesforce와 Azure Active Directory 통합 | Microsoft 문서"
description: "Azure Active Directory와 Salesforce 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: jeedes
ms.openlocfilehash: 93f3912e2405a4ebeee26e3741d6412a75410b7f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전을 위한 Salesforce 구성

이 자습서의 목적은 사용자 계정을 Azure AD에서 Salesforce로 자동 프로비전 및 프로비전 해제하도록 Salesforce 및 Azure AD에서 수행해야 하는 단계를 설명하는 것입니다.

## <a name="prerequisites"></a>필수 조건

이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.

*   Azure Active Directory 테넌트.
*   Salesforce for Work 또는 Salesforce for Education에 대한 유효한 테넌트가 있어야 합니다. 어느 서비스에나 평가판 계정을 사용할 수 있습니다.
*   팀 관리자 권한이 있는 Salesforce의 사용자 계정.

## <a name="assigning-users-to-salesforce"></a>Salesforce에 사용자 할당

Azure Active Directory는 "할당"이라는 개념을 사용하여 어떤 사용자가 선택한 앱에 대한 액세스를 받아야 하는지를 판단합니다. 자동 사용자 계정 프로비전의 컨텍스트에서는 Azure AD의 응용 프로그램에 "할당된" 사용자 및 그룹만 동기화됩니다.

프로비전 서비스를 구성하고 사용하도록 설정하려면 먼저 Salesforce 앱에 대한 액세스가 필요한 Azure AD의 사용자 또는 그룹을 결정해야 합니다. 결정했으면 [엔터프라이즈 앱에 사용자 또는 그룹 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)의 지침에 따라 사용자를 Salesforce 앱에 할당할 수 있습니다.

### <a name="important-tips-for-assigning-users-to-salesforce"></a>Salesforce에 사용자를 할당하기 위한 주요 팁

*   프로비전 구성을 테스트하기 위해 단일 Azure AD 사용자를 Salesforce에 할당하는 것이 좋습니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.

*  Salesforce에 사용자를 할당할 때 유효한 사용자 역할을 선택해야 합니다. "기본 액세스" 역할은 프로비전에 작동하지 않습니다.

    > [!NOTE]
    > 이 앱은 프로비전 프로세스에서 Salesforce의 사용자 지정 역할을 가져오며, 고객이 사용자를 할당할 때 선택할 수 있습니다.

## <a name="enable-automated-user-provisioning"></a>자동 사용자 프로비전 사용

이 섹션에서는 사용자의 Azure AD를 Salesforce의 사용자 계정 프로비전 API에 연결하고, Azure AD의 사용자 및 그룹 할당을 기반으로 Salesforce에서 할당된 사용자 계정을 만들고 업데이트하고 비활성화하도록 프로비전 서비스를 구성하는 방법을 안내합니다.

>[!Tip]
>[Azure Portal](https://portal.azure.com)에 제공된 지침에 따라 Salesforce에 SAML 기반 Single Sign-On을 사용하도록 선택할 수도 있습니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.

### <a name="configure-automatic-user-account-provisioning"></a>자동 사용자 계정 프로비전 구성

이 섹션은 Salesforce에 Active Directory 사용자 계정을 사용자 프로비전할 수 있도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.

1. [Azure Portal](https://portal.azure.com)에서 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션으로 이동합니다.

2. 이미 Salesforce에 Single Sign-On을 구성한 경우 검색 필드를 사용하여 Salesforce의 인스턴스를 검색합니다. 그렇지 않은 경우 **추가**를 선택하고 응용 프로그램 갤러리에서 **Salesforce**를 검색합니다. 검색 결과에서 Salesforce를 선택하고 응용 프로그램 목록에 추가합니다.

3. Salesforce의 인스턴스를 선택한 다음 **프로비전** 탭을 선택합니다.

4. **프로비전 모드**를 **자동**으로 설정합니다.

    ![프로비전](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. **관리자 자격 증명** 섹션에서 다음 구성 설정을 제공합니다.
   
    a. **관리 사용자 이름** 텍스트 상자에 Salesforce.com에서 **시스템 관리자** 프로필이 할당된 Salesforce 계정 이름을 입력합니다.
   
    b. **관리자 암호** 텍스트 상자에 이 계정의 암호를 입력합니다.

6. Salesforce 보안 토큰을 얻으려면 새 탭을 열고 동일한 Salesforce 관리자 계정에 로그인합니다. 페이지의 오른쪽 위 모서리에 있는 사용자 이름을 클릭하고 **설정**을 클릭합니다.

     ![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "자동 사용자 프로비저닝 사용")

7. 왼쪽 탐색 패널에서 **내 개인 정보**를 클릭하여 관련 섹션을 확장하고 **내 보안 토큰 재설정**을 클릭합니다.
  
    ![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "자동 사용자 프로비저닝 사용")

8. **보안 토큰 재설정** 페이지에서 **보안 토큰 재설정** 단추를 클릭합니다.

    ![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "자동 사용자 프로비저닝 사용")

9. 이 관리자 계정과 연결된 전자 메일 받은 편지함을 확인합니다. Salesforce.com에서 새 보안 토큰이 포함된 전자 메일을 찾습니다.

10. 토큰을 복사하고 Azure AD 창으로 이동하여 **비밀 토큰** 필드에 붙여넣습니다.

11. Azure Portal에서 **연결 테스트**를 클릭하여 Azure AD가 Salesforce 앱에 연결할 수 있는지 확인합니다.

12. 프로비전 오류 알림을 받을 개인 또는 그룹의 이메일 주소를 **알림 메일** 필드에 입력하고 아래의 확인란을 선택합니다.

13. **저장**을 클릭합니다.  
    
14.  매핑 섹션에서 **Azure Active Directory 사용자를 Salesforce에 동기화**를 선택합니다.

15. **특성 매핑** 섹션에서 Azure AD에서 Salesforce로 동기화할 사용자 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업 시 Salesforce의 사용자 계정을 일치시키는 데 사용됩니다. 저장 단추를 선택하여 변경 내용을 커밋합니다.

16. Salesforce에 대한 Azure AD 프로비전 서비스를 사용하도록 설정하려면 설정 섹션에서 **프로비전 상태**를 **켜기**로 변경합니다.

17. **저장**을 클릭합니다.

사용자 및 그룹 섹션에서 Salesforce에 할당된 모든 사용자 및/또는 그룹의 초기 동기화가 시작됩니다. 초기 동기화는 서비스가 실행되는 동안 약 20분마다 발생하는 차후 동기화보다 더 많은 시간이 걸립니다. **동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 Salesforce 앱에서 프로비전 서비스에서 수행하는 모든 작업을 설명하는 프로비전 작업 보고서에 연결된 링크를 이용할 수 있습니다.

이제 테스트 계정을 만들 수 있습니다. 이제 최대 20분 동안 기다린 후 계정이 Salesforce에 동기화되었는지 확인합니다.

## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [Single Sign-On 구성](https://docs.microsoft.com/azure/active-directory/active-directory-saas-salesforce-tutorial)