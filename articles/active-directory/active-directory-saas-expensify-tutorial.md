---
title: "자습서: Expensify와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Expensify 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/2/2017
ms.author: jeedes
ms.openlocfilehash: 730c1e1eeb9fc1a7037ffa1a5815d5e9d484a52d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a>자습서: Expensify와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Expensify를 통합하는 방법에 대해 알아봅니다.

Expensify를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

- Expensify에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
- 사용자가 해당 Azure AD 계정으로 Expensify에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

Expensify와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- Expensify Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.

이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 Expensify 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-expensify-from-the-gallery"></a>갤러리에서 Expensify 추가
Expensify와 Azure AD의 통합을 구성하려면 갤러리의 Expensify를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Expensify를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다. 

    ![Azure Active Directory 단추][1]

2. **엔터프라이즈 응용 프로그램**으로 이동합니다. 그런 후 **모든 응용 프로그램**으로 이동합니다.

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. 새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.

    ![새 응용 프로그램 단추][3]

4. 검색 상자에서 **Expensify**를 입력하고, 결과 패널에서 **Expensify**를 선택한 다음, **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.

    ![결과 목록의 Expensify](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Expensify에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Expensify 사용자가 누구인지 알고 있어야 합니다. 즉, Azure AD 사용자와 Expensify의 관련 사용자 간에 연결이 설정되어야 합니다.

Expensify에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.

Expensify에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
3. **[Expensify 테스트 사용자 만들기](#create-an-expensify-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Expensify에 만듭니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Expensify 응용 프로그램에서 Single Sign-On을 구성합니다.

**Expensify에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**

1. Azure Portal의 **Expensify** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.

    ![Single Sign-On 구성 링크][4]

2. **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. **Expensify 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.

    ![Expensify 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    a. **로그온 URL** 텍스트 상자에서 URL `https://www.expensify.com/authentication/saml/login`를 입력합니다.

    b. **식별자** 텍스트 상자에서 `https://www.<companyname>.expensify.com` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE] 
    > 식별자 URL의 `<companyname>` 섹션을 회사의 도메인으로 바꿉니다. 위의 `https://contoso.expensify.com` 예를 참조하세요. 이 값을 얻으려면 [Expensify 클라이언트 지원 팀](mailto:help@expensify.com)에 문의하세요.

4. **SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.

    ![인증서 다운로드 링크](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. Expensify에서 SSO를 사용하도록 설정하려면 먼저 응용 프로그램에서 **도메인 컨트롤**을 사용하도록 설정해야 합니다. [여기에](http://help.expensify.com/domain-control) 나열된 단계를 수행하여 응용 프로그램에서 도메인 컨트롤을 사용하도록 설정할 수 있습니다. 추가 지원은 [Expensify 클라이언트 지원 팀](mailto:help@expensify.com)에 문의하세요. 도메인 컨트롤을 사용하도록 설정한 후에는 다음 단계를 따릅니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    a. Expensify 응용 프로그램에 로그인합니다.
    
    b. 위쪽에 도구 모음에서 **관리자**를 클릭합니다.
    
    c. 왼쪽 패널에서 **도메인**을 클릭합니다.
    
    d. 확인된 도메인 이름을 클릭합니다.
    
    e. 왼쪽 패널에서 **SAML**을 클릭한 다음 **사용**을 선택합니다.
    
    f. Azure AD에서 다운로드한 페더레이션 메타데이터를 메모장으로 열고 콘텐츠를 복사하여 **ID 공급자 메타데이터** 텍스트 상자에 붙여넣습니다.

> [!TIP]
> 이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.  **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다. 포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

   ![Azure AD 테스트 사용자 만들기][100]

**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.

    ![Azure Active Directory 단추](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png)

2. 사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png)

3. **사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.

    ![추가 단추](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png)

4. **사용자** 대화 상자에서 다음 단계를 수행합니다.

    ![사용자 대화 상자](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png)

    a. **이름** 상자에 **BrittaSimon**을 입력합니다.

    b. **사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.

    c. **암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.

    d. **만들기**를 클릭합니다.
 
### <a name="create-an-expensify-test-user"></a>Expensify 테스트 사용자 만들기

이 섹션에서는 Expensify에서 Britta Simon이라는 사용자를 만듭니다. Expensify 플랫폼에서 사용자를 추가하려면 [Expensify 클라이언트 지원 팀](mailto:help@expensify.com)에 문의하세요.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Expensify에 대한 액세스 권한을 부여합니다.

![사용자 역할 할당][200] 

**Britta Simon을 Expensify에 할당하려면 다음 단계를 수행합니다.**

1. Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.

    ![사용자 할당][201] 

2. 응용 프로그램 목록에서 **Expensify**를 선택합니다.

    ![응용 프로그램 목록의 Expensify 링크](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png)  

3. 왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.

    !["사용자 및 그룹" 링크][202]

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![할당 추가 창][203]

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Expensify 타일을 클릭하면 Expensify 응용 프로그램에 자동으로 로그온됩니다.
액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요. 

## <a name="additional-resources"></a>추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

