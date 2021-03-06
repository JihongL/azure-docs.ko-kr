---
title: "Azure AD Connect: Seamless Single Sign-On Single Sign-On - FAQ(질문과 대답) | Microsoft Docs"
description: "Azure Active Directory Seamless Single Sign-On에 대한 질문과 대답입니다."
services: active-directory
keywords: "Azure AD Connect의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: mtillman
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2017
ms.author: billmath
ms.openlocfilehash: 8eb575d6647b123119ceff9452ee8fc4a489f1ca
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Azure Active Directory Seamless Single Sign-On: FAQ(질문과 대답)

이 문서에서는 Azure Active Directory Seamless SSO(Seamless Single Sign-On)에 대한 질문과 대답을 다룹니다. 새로운 내용을 계속 확인해 주세요.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Seamless SSO에서 사용되는 로그인 방법은 무엇인가요?

Seamless SSO는 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 또는 [통과 인증](active-directory-aadconnect-pass-through-authentication.md) 로그인 방법과 결합할 수 있습니다. 그러나 AD FS(Active Directory Federation Services)에는 이 기능을 사용할 수 없습니다.

## <a name="is-seamless-sso-a-free-feature"></a>Seamless SSO는 평가판 체험 기능인가요?

평가판 체험 기능이며, Azure AD 유료 버전으로 이 기능을 사용할 필요가 없습니다. 이 기능은 일반 공급될 때도 추가 비용 없이 제공될 것입니다.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Seamless SSO의 `domain_hint` 또는 `login_hint` 매개 변수 기능을 활용하는 응용 프로그램은 무엇인가요?

이러한 매개 변수를 보내는 응용 프로그램 목록과 그렇지 않은 응용 프로그램 목록을 작성하는 중입니다. 관심 있는 응용 프로그램이 있으시면 의견 섹션에 알려주세요.

## <a name="does-seamless-sso-support-alternate-id-as-the-username-instead-of-userprincipalname"></a>Seamless SSO에서는 사용자 이름으로 `userPrincipalName` 대신 `Alternate ID`를 지원하는가요?

예. Seamless SSO는 [여기서](active-directory-aadconnect-get-started-custom.md) 보여주듯이 Azure AD Connect에서 구성할 때 `Alternate ID`를 사용자 이름으로 지원합니다. 모든 Office 365 응용 프로그램에서 `Alternate ID`를 지원하지는 않습니다. 지원 내용은 특정 응용 프로그램의 설명서를 참조하세요.

## <a name="i-want-to-register-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>AD FS를 사용하지 않고 비Windows 10 장치를 Azure AD에 등록하려고 합니다. Seamless SSO를 대신 사용할 수 있나요?

예, 이 시나리오에는 [작업 공간 연결 클라이언트](https://www.microsoft.com/download/details.aspx?id=53554) 버전 2.1 이상이 필요합니다.

## <a name="how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacc-computer-account"></a>`AZUREADSSOACC` 컴퓨터 계정의 Kerberos 암호 해독 키를 롤오버하려면 어떻게 하나요?

온-프레미스 AD 포리스트에 만든 `AZUREADSSOACC` 컴퓨터 계정(Azure AD를 나타냄)의 Kerberos 암호 해독 키를 자주 롤오버하는 것이 중요합니다.

>[!IMPORTANT]
>적어도 30일마다 Kerberos 암호 해독 키를 롤오버하는 것이 좋습니다.

Azure AD Connect를 실행 중인 온-프레미스 서버에서 다음 단계를 따릅니다.

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>1단계. Seamless SSO가 사용하도록 설정된 AD 포리스트 목록을 가져옵니다.

1. 먼저 [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)를 다운로드하여 설치합니다.
2. 그런 다음 [Windows PowerShell 용 64비트 Azure Active Directory 모듈](http://go.microsoft.com/fwlink/p/?linkid=236297)을 다운로드하고 설치합니다.
3. `%programfiles%\Microsoft Azure Active Directory Connect` 폴더로 이동합니다.
4. 다음 명령을 사용하여 Seamless SSO PowerShell 모듈을 가져옵니다. `Import-Module .\AzureADSSO.psd1`
5. 관리자 권한으로 PowerShell을 실행합니다. PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다. 이 명령으로 테넌트의 전역 관리자 자격 증명을 입력하라는 팝업 메시지가 표시됩니다.
6. `Get-AzureADSSOStatus`를 호출합니다. 사용하도록 설정된 AD 포리스트 목록("도메인" 목록에 있음)이 표시됩니다.

### <a name="step-2-update-the-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>2단계. 설정된 각 AD 포리스트에서 Kerberos 암호 해독 키를 업데이트합니다.

1. `$creds = Get-Credential`를 호출합니다. 메시지가 표시되면 의도한 AD 포리스트에 대한 도메인 관리자 자격 증명을 입력합니다.
2. `Update-AzureADSSOForest -OnPremCredentials $creds`를 호출합니다. 이 명령은 이 특정 AD 포리스트에서 `AZUREADSSOACC` 컴퓨터 계정에 대한 Kerberos 암호 해독 키를 업데이트하고 Azure AD에서 키를 업데이트 합니다.
3. 기능을 설정한 각 AD 포리스트에 대해 위의 단계를 반복합니다.

>[!IMPORTANT]
>`Update-AzureADSSOForest` 명령을 두 번 이상 실행하지 _않아야 합니다_. 그렇지 않으면 해당 기능은 사용자의 Kerberos 티켓이 만료되고 온-프레미스 Active Directory에 의해 재발급될 때까지 작동하지 않습니다.

## <a name="how-can-i-disable-seamless-sso"></a>Seamless SSO를 사용하지 않으려면 어떻게 해야 하나요?

Seamless SSO는 Azure AD Connect를 통해 사용하지 않도록 설정할 수 있습니다.

Azure AD Connect를 실행하고 “사용자 로그인 페이지 변경”(Change user sign-in page)을 선택하고 “다음”을 클릭합니다. 그런 다음 “Single Sign-On 사용” 옵션의 선택을 취소합니다. 마법사를 계속 진행합니다. 마법사를 완료하면 테넌트에서 SSO Seamless를 사용하지 않도록 설정됩니다.

그러나 화면에 다음과 같은 메시지가 표시됩니다.

“Single Sign-On을 이제 사용하지 않도록 설정했습니다. 하지만 정리를 완료하기 위해 수행할 추가 수동 단계가 남아 있습니다. 자세한 정보”

이 과정을 완료하려면 Azure AD Connect를 실행 중인 온-프레미스 서버에서 다음 수동 단계를 따릅니다.

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>1단계. Seamless SSO가 사용하도록 설정된 AD 포리스트 목록을 가져옵니다.

1. 먼저 [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)를 다운로드하여 설치합니다.
2. 그런 다음 [Windows PowerShell 용 64비트 Azure Active Directory 모듈](http://go.microsoft.com/fwlink/p/?linkid=236297)을 다운로드하고 설치합니다.
3. `%programfiles%\Microsoft Azure Active Directory Connect` 폴더로 이동합니다.
4. 다음 명령을 사용하여 Seamless SSO PowerShell 모듈을 가져옵니다. `Import-Module .\AzureADSSO.psd1`
5. 관리자 권한으로 PowerShell을 실행합니다. PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다. 이 명령으로 테넌트의 전역 관리자 자격 증명을 입력하라는 팝업 메시지가 표시됩니다.
6. `Get-AzureADSSOStatus`를 호출합니다. 사용하도록 설정된 AD 포리스트 목록("도메인" 목록에 있음)이 표시됩니다.

### <a name="step-2-manually-delete-the-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>2단계. 나열된 각 AD 포리스트에서 `AZUREADSSOACCT` 컴퓨터 계정을 수동으로 삭제합니다.

## <a name="next-steps"></a>다음 단계

- [**빠른 시작**](active-directory-aadconnect-sso-quick-start.md) - Azure AD Seamless SSO를 준비하고 실행합니다.
- [**기술 심층 분석**](active-directory-aadconnect-sso-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.
- [**문제 해결**](active-directory-aadconnect-troubleshoot-sso.md) - 기능과 관련된 일반적인 문제를 해결하는 방법에 대해 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
