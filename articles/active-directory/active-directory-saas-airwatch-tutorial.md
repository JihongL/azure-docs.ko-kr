---
title: "자습서: AirWatch와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 AirWatch 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a0e314aaf59a70107058829ea84dde362f097274
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>자습서: AirWatch와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 AirWatch를 통합하는 방법에 대해 알아봅니다.

AirWatch와 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.

- AirWatch에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
- 사용자가 해당 Azure AD 계정으로 AirWatch에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

AirWatch와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- AirWatch Single Sign-on이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.

이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 AirWatch 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-airwatch-from-the-gallery"></a>갤러리에서 AirWatch 추가
AirWatch의 Azure AD 통합을 구성하려면 갤러리의 AirWatch를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 AirWatch를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다. 

    ![Active Directory][1]

2. **엔터프라이즈 응용 프로그램**으로 이동합니다. 그런 후 **모든 응용 프로그램**으로 이동합니다.

    ![응용 프로그램][2]
    
3. 새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.

    ![응용 프로그램][3]

4. 검색 상자에 **AirWatch**를 입력합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. 결과 패널에서 **AirWatch**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AirWatch에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 AirWatch 사용자가 누구인지 알고 있어야 합니다. 즉, Azure AD 사용자와 AirWatch의 관련 사용자 간에 연결이 형성되어야 합니다.

이 연결 관계는 Azure AD의 **사용자 이름** 값을 AirWatch의 **Username** 값으로 할당하여 설정합니다.

AirWatch에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
3. **[AirWatch 테스트 사용자 만들기](#creating-a-airwatch-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 AirWatch에 만듭니다.
4. **[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 AirWatch 응용 프로그램에서 Single Sign-On을 구성합니다.

**AirWatch에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**

1. Azure Portal의 **AirWatch** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.

    ![Single Sign-on 구성][4]

2. **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. **AirWatch 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    a. **로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. **식별자** 텍스트 상자에 해당 값으로 `AirWatch`을 입력합니다.

    > [!NOTE] 
    > 이 값은 실제 값이 아닙니다. 이 값을 실제 로그온 URL로 업데이트합니다. 이 값을 얻으려면 [AirWatch Client 지원 팀](http://www.air-watch.com/company/contact-us/)에 문의하세요. 
 
4. **SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 XML 파일을 저장합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. **AirWatch 구성** 섹션에서 **AirWatch 구성**을 클릭하여 **로그인 구성** 창을 엽니다. **빠른 참조 섹션**에서 **SAML Single Sign-On 서비스 URL**을 복사합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. 다른 웹 브라우저 창에서 AirWatch 회사 사이트에 관리자로 로그인합니다.

8. 왼쪽 탐색 창에서 **계정**과 **관리자**를 차례로 클릭합니다.
   
   ![관리자](./media/active-directory-saas-airwatch-tutorial/ic791920.png "관리자")

9. **설정** 메뉴를 확장한 다음 **디렉터리 서비스**를 클릭합니다.
   
   ![설정](./media/active-directory-saas-airwatch-tutorial/ic791921.png "설정")

10. **사용자** 탭을 클릭하고 **Base DN** 텍스트 상자에 도메인 이름을 입력한 다음 **저장**을 클릭합니다.
   
   ![사용자](./media/active-directory-saas-airwatch-tutorial/ic791922.png "사용자")

11. **서버** 탭을 클릭합니다.
   
   ![서버](./media/active-directory-saas-airwatch-tutorial/ic791923.png "서버")

12. 다음 단계를 수행합니다.
    
    ![업로드](./media/active-directory-saas-airwatch-tutorial/ic791924.png "업로드")   
    
    a. **디렉터리 유형**으로 **없음**을 선택합니다.

    b. **인증에 SAML 사용**을 선택합니다.

    c. 다운로드한 인증서를 업로드하려면 **업로드**를 클릭합니다.

13. **요청** 섹션에서 다음 단계를 수행합니다.
    
    ![요청](./media/active-directory-saas-airwatch-tutorial/ic791925.png "요청")  

    a. **요청 바인딩 형식**으로 **POST**를 선택합니다.

    b. Azure Portal의 **Airwatch에서 Single Sign-on 구성** 대화 상자 페이지에서 **SAML Single Sign-On 서비스 URL** 값을 복사한 다음 **ID 공급자 Single Sign-On URL** 텍스트 상자에 붙여 넣습니다.

    c. **NameID 형식**으로 **전자 메일 주소**를 선택합니다.

    d. **Save**를 클릭합니다.

14. **사용자** 탭을 다시 클릭합니다.
    
    ![사용자](./media/active-directory-saas-airwatch-tutorial/ic791926.png "사용자")

15. **특성** 섹션에서 다음 단계를 수행합니다.
    
    ![특성](./media/active-directory-saas-airwatch-tutorial/ic791927.png "특성")

    a. **개체 식별자** 텍스트 상자에 **http://schemas.microsoft.com/identity/claims/objectidentifier**를 입력합니다.

    b. **사용자 이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**를 입력합니다.

    c. **표시 이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**을 입력합니다.

    d. **이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**을 입력합니다.

    e. **성** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**을 입력합니다.

    f. **전자 메일** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**를 입력합니다.

    g. **Save**를 클릭합니다.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

![Azure AD 사용자 만들기][100]

**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**

1. **Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. 사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. **사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. **사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    a. **이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.

    b. **사용자 이름** 텍스트 상자에 Britta Simon의 **메일 주소**를 입력합니다.

    c. **암호 표시**를 선택하고 **암호** 값을 적어둡니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-airwatch-test-user"></a>AirWatch 테스트 사용자 만들기

Azure AD 사용자가 AirWatch에 로그인할 수 있도록 하려면 AirWatch로 프로비전되어야 합니다.

* AirWatch의 경우 프로비전은 수동 작업입니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. **AirWatch** 회사 사이트에 관리자 권한으로 로그인합니다.
2. 왼쪽의 탐색 창에서 **계정**과 **사용자**를 차례로 클릭합니다.
   
   ![사용자](./media/active-directory-saas-airwatch-tutorial/ic791929.png "사용자")
3. **사용자** 메뉴에서 **목록 보기**와 **추가 \> 사용자 추가**를 차례로 클릭합니다.
   
   ![사용자 추가](./media/active-directory-saas-airwatch-tutorial/ic791930.png "사용자 추가")
4. **사용자 추가/편집** 대화 상자에서 다음 단계를 수행합니다.

   ![사용자 추가](./media/active-directory-saas-airwatch-tutorial/ic791931.png "사용자 추가")   
   1. 관련된 텍스트 상자에 프로비전할 유효한 Azure Active Directory 계정의 **사용자 이름**, **암호**, **암호 확인**, **이름**, **성**, **전자 메일 주소**를 입력합니다.
   2. **Save**를 클릭합니다.

>[!NOTE]
>다른 AirWatch 사용자 계정 생성 도구 또는 AirWatch가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.
>  

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 AirWatch에 대한 액세스 권한을 부여합니다.

![사용자 할당][200] 

**Britta Simon을 AirWatch에 할당하려면 다음 단계를 수행합니다.**

1. Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.

    ![사용자 할당][201] 

2. 응용 프로그램 목록에서 **AirWatch**를 선택합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. 왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.


## <a name="additional-resources"></a>추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

