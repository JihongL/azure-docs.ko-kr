---
title: "여러 구독 및 리소스 그룹에 Azure 리소스 배포 | Microsoft Docs"
description: "배포 중에 둘 이상의 Azure 구독 및 리소스 그룹을 대상으로 지정하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2017
ms.author: tomfitz
ms.openlocfilehash: 763f46b9b5be7edf06ee0604bfc51a2482405b60
ms.sourcegitcommit: 7136d06474dd20bb8ef6a821c8d7e31edf3a2820
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="deploy-azure-resources-to-more-than-one-subscription-or-resource-group"></a>둘 이상의 구독 또는 리소스 그룹에 Azure 리소스 배포

일반적으로 단일 리소스 그룹에 템플릿의 모든 리소스를 배포합니다. 그러나 일단의 리소스를 함께 배포하고 다른 리소스 그룹 또는 구독에 배치하려는 시나리오가 있습니다. 예를 들어 Azure Site Recovery의 백업 가상 컴퓨터를 별도의 리소스 그룹과 위치에 배포할 수 있습니다. Resource Manager를 사용하면 중첩된 템플릿을 사용하여 부모 템플릿에 사용된 구독 및 리소스 그룹과 다른 구독 및 리소스 그룹을 대상으로 지정할 수 있습니다.

리소스 그룹은 응용 프로그램 및 해당 리소스 컬렉션에 대한 수명 주기 컨테이너입니다. 템플릿 외부에서 리소스 그룹을 만들고 배포 중에 대상으로 지정할 리소스 그룹을 지정합니다. 리소스 그룹에 대한 소개는 [Azure Resource Manager 개요](resource-group-overview.md)를 참조하세요.

## <a name="specify-a-subscription-and-resource-group"></a>구독 및 리소스 그룹 지정

다른 리소스를 대상으로 지정하려면 배포 중에 중첩되거나 연결된 템플릿을 사용해야 합니다. `Microsoft.Resources/deployments` 리소스 종류는 `subscriptionId` 및 `resourceGroup`에 대한 매개 변수를 제공합니다. 이러한 속성을 사용하여 중첩된 배포에 대해 다른 구독 및 리소스 그룹을 지정할 수 있습니다. 모든 리소스 그룹은 배포를 실행하기 전에 존재해야 합니다. 구독 ID 또는 리소스 그룹을 지정하지 않으면 부모 템플릿의 구독 및 리소스 그룹이 사용됩니다.

다음 예제에서는 배포 중에 지정한 리소스 그룹 및 `secondResourceGroup` 매개 변수에 지정한 리소스 그룹에 각각 하나씩 두 개의 저장소 계정을 배포합니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storagePrefix": {
            "type": "string",
            "maxLength": 11
        },
        "secondResourceGroup": {
            "type": "string"
        },
        "secondSubscriptionID": {
            "type": "string",
            "defaultValue": ""
        },
        "secondStorageLocation": {
            "type": "string",
            "defaultValue": "[resourceGroup().location]"
        }
    },
    "variables": {
        "firstStorageName": "[concat(parameters('storagePrefix'), uniqueString(resourceGroup().id))]",
        "secondStorageName": "[concat(parameters('storagePrefix'), uniqueString(parameters('secondSubscriptionID'), parameters('secondResourceGroup')))]"
    },
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "[parameters('secondResourceGroup')]",
            "subscriptionId": "[parameters('secondSubscriptionID')]",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[variables('secondStorageName')]",
                            "apiVersion": "2017-06-01",
                            "location": "[parameters('secondStorageLocation')]",
                            "sku":{
                                "name": "Standard_LRS"
                            },
                            "kind": "Storage",
                            "properties": {
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[variables('firstStorageName')]",
            "apiVersion": "2017-06-01",
            "location": "[resourceGroup().location]",
            "sku":{
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {
            }
        }
    ]
}
```

`resourceGroup`을 존재하지 않는 리소스 그룹의 이름으로 설정하면 배포에 실패합니다.

## <a name="deploy-the-template"></a>템플릿 배포

예제 템플릿을 배포하려면 2017년 5월 이후의 Azure PowerShell 또는 Azure CLI 릴리스를 사용합니다. 이러한 예제의 경우 GitHub의 [구독 간 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/crosssubscription.json)을 사용하세요.

### <a name="two-resource-groups-in-the-same-subscription"></a>같은 구독의 두 리소스 그룹

PowerShell의 경우 두 개의 저장소 계정을 동일한 구독의 두 리소스 그룹에 배포하려면 다음을 사용합니다.

```powershell
$firstRG = "primarygroup"
$secondRG = "secondarygroup"

New-AzureRmResourceGroup -Name $firstRG -Location southcentralus
New-AzureRmResourceGroup -Name $secondRG -Location eastus

New-AzureRmResourceGroupDeployment `
  -ResourceGroupName $firstRG `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crosssubscription.json `
  -storagePrefix storage `
  -secondResourceGroup $secondRG `
  -secondStorageLocation eastus
```

Azure CLI의 경우 두 개의 저장소 계정을 동일한 구독의 두 리소스 그룹에 배포하려면 다음을 사용합니다.

```azurecli-interactive
firstRG="primarygroup"
secondRG="secondarygroup"

az group create --name $firstRG --location southcentralus
az group create --name $secondRG --location eastus
az group deployment create \
  --name ExampleDeployment \
  --resource-group $firstRG \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crosssubscription.json \
  --parameters storagePrefix=tfstorage secondResourceGroup=$secondRG secondStorageLocation=eastus
```

배포가 완료되면 두 개의 리소스 그룹이 표시됩니다. 각 리소스 그룹에는 저장소 계정이 포함되어 있습니다.

### <a name="two-resource-groups-in-different-subscriptions"></a>다른 구독의 두 리소스 그룹

PowerShell의 경우 두 개의 저장소 계정을 두 구독에 배포하려면 다음을 사용합니다.

```powershell
$firstRG = "primarygroup"
$secondRG = "secondarygroup"

$firstSub = "<first-subscription-id>"
$secondSub = "<second-subscription-id>"

Select-AzureRmSubscription -Subscription $secondSub
New-AzureRmResourceGroup -Name $secondRG -Location eastus

Select-AzureRmSubscription -Subscription $firstSub
New-AzureRmResourceGroup -Name $firstRG -Location southcentralus

New-AzureRmResourceGroupDeployment `
  -ResourceGroupName $firstRG `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crosssubscription.json `
  -storagePrefix storage `
  -secondResourceGroup $secondRG `
  -secondStorageLocation eastus `
  -secondSubscriptionID $secondSub
```

Azure CLI의 경우 두 개의 저장소 계정을 두 구독에 배포하려면 다음을 사용합니다.

```azurecli-interactive
firstRG="primarygroup"
secondRG="secondarygroup"

firstSub="<first-subscription-id>"
secondSub="<second-subscription-id>"

az account set --subscription $secondSub
az group create --name $secondRG --location eastus

az account set --subscription $firstSub
az group create --name $firstRG --location southcentralus

az group deployment create \
  --name ExampleDeployment \
  --resource-group $firstRG \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crosssubscription.json \
  --parameters storagePrefix=storage secondResourceGroup=$secondRG secondStorageLocation=eastus secondSubscriptionID=$secondSub
```

## <a name="use-the-resourcegroup-function"></a>resourceGroup() 함수 사용

리소스 그룹 간 배포의 경우 [resourceGroup() 함수](resource-group-template-functions-resource.md#resourcegroup)는 중첩 템플릿 지정 방식에 따라 다르게 확인됩니다. 

하나의 템플릿을 다른 템플릿 내에 포함하는 경우 중첩 템플릿의 resourceGroup()이 부모 리소스 그룹으로 확인됩니다. 포함된 템플릿은 다음 형식을 사용합니다.

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

별도의 템플릿에 연결하는 경우 연결된 템플릿의 resourceGroup()가 중첩된 리소스 그룹으로 확인됩니다. 연결된 템플릿은 다음 형식을 사용합니다.

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

`resourceGroup()`이 확인하는 여러 다른 방법을 테스트하려면 부모 템플릿, 인라인 템플릿 및 연결된 템플릿에 대해 리소스 그룹 개체를 반환하는 [예제 템플릿](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/crossresourcegroupproperties.json)을 배포하세요. 부모 및 인라인 템플릿 둘 다 동일한 리소스 그룹으로 확인됩니다. 연결된 템플릿은 연결된 리소스 그룹으로 확인됩니다.

PowerShell의 경우 다음을 사용합니다.

```powershell
New-AzureRmResourceGroup -Name parentGroup -Location southcentralus
New-AzureRmResourceGroup -Name inlineGroup -Location southcentralus
New-AzureRmResourceGroup -Name linkedGroup -Location southcentralus

New-AzureRmResourceGroupDeployment `
  -ResourceGroupName parentGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crossresourcegroupproperties.json
```

Azure CLI의 경우 

```azurecli-interactive
az group create --name parentGroup --location southcentralus
az group create --name inlineGroup --location southcentralus
az group create --name linkedGroup --location southcentralus

az group deployment create \
  --name ExampleDeployment \
  --resource-group parentGroup \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crossresourcegroupproperties.json 
```

## <a name="next-steps"></a>다음 단계

* 템플릿에서 매개 변수를 정의하는 방법을 이해하려면 [Azure Resource Manager 템플릿의 구조 및 구문 이해](resource-group-authoring-templates.md)를 참조하세요.
* 일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.
* SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.
