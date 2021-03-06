---
title: "Azure Functions의 Azure Service Bus 바인딩"
description: "Azure Functions에서 Azure Service Bus 트리거 및 바인딩을 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: tdykstra
manager: cfowler
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: tdykstra
ms.openlocfilehash: 6d59b26fa4ab17c17827a8e3450e808e40e5c2dd
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2017
---
# <a name="azure-service-bus-bindings-for-azure-functions"></a>Azure Functions의 Azure Service Bus 바인딩

이 문서에서는 Azure Functions에서 Azure Service Bus 바인딩을 사용하는 방법을 설명합니다. Azure Functions는 Service Bus 큐 및 토픽에 대한 트리거 및 출력 바인딩을 지원합니다.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="trigger"></a>트리거

Service Bus 트리거를 사용하여 Service Bus 큐 또는 토픽의 메시지에 응답합니다. 

## <a name="trigger---example"></a>트리거 - 예제

언어 관련 예제를 참조하세요.

* [미리 컴파일된 C#](#trigger---c-example)
* [C# 스크립트](#trigger---c-script-example)
* [F#](#trigger---f-example)
* [JavaScript](#trigger---javascript-example)

### <a name="trigger---c-example"></a>트리거 - C# 예제

다음 예제에서는 Service Bus 큐 메시지를 기록하는 [미리 컴파일된 C# 함수](functions-dotnet-class-library.md)를 보여줍니다.

```cs
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] 
    string myQueueItem, 
    TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

### <a name="trigger---c-script-example"></a>트리거 - C# 스크립트 예제

다음 예에서는 *function.json* 파일의 Service Bus 트리거 바인딩 및 바인딩을 사용하는 [C# 스크립트 함수](functions-reference-csharp.md)를 보여줍니다. 이 함수는 Service Bus 큐 메시지를 기록합니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

C# 스크립트 코드는 다음과 같습니다.

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

### <a name="trigger---f-example"></a>트리거 - F# 예제

다음 예에서는 *function.json* 파일의 Service Bus 트리거 바인딩 및 바인딩을 사용하는 [F# 함수](functions-reference-fsharp.md)를 보여줍니다. 이 함수는 Service Bus 큐 메시지를 기록합니다. 

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

F# 스크립트 코드는 다음과 같습니다.

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

### <a name="trigger---javascript-example"></a>트리거 - JavaScript 예제

다음 예에서는 *function.json* 파일의 Service Bus 트리거 바인딩 및 바인딩을 사용하는 [JavaScript 함수](functions-reference-node.md)를 보여줍니다. 이 함수는 Service Bus 큐 메시지를 기록합니다. 

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

JavaScript 스크립트 코드는 다음과 같습니다.

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

## <a name="trigger---attributes"></a>트리거 - 특성

[미리 컴파일된 C#](functions-dotnet-class-library.md) 함수의 경우 다음 특성을 사용하여 Service Bus 트리거를 구성합니다.

* [ServiceBusTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusTriggerAttribute.cs)는 [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus) NuGet 패키지에 정의되어 있습니다.

  특성의 생성자는 큐의 이름 또는 토픽과 구독을 사용합니다. 연결의 액세스 권한을 지정할 수도 있습니다. 액세스 권한을 지정하지 않으면 기본값은 `Manage`입니다. 액세스 권한을 설정을 선택하는 방법은 [트리거 - 구성](#trigger---configuration) 섹션에서 설명합니다. 문자열 매개 변수와 함께 사용되는 특성을 보여주는 예제는 다음과 같습니다.

  ```csharp
  [FunctionName("ServiceBusQueueTriggerCSharp")]                    
  public static void Run(
      [ServiceBusTrigger("myqueue")] string myQueueItem, TraceWriter log)
  {
      ...
  }
  ```

  다음 예와 같이 사용할 Service Bus 계정을 지정하도록 `Connection` 속성을 설정할 수 있습니다.

  ```csharp
  [FunctionName("ServiceBusQueueTriggerCSharp")]                    
  public static void Run(
      [ServiceBusTrigger("myqueue", Connection = "ServiceBusConnection")] 
      string myQueueItem, TraceWriter log)
  {
      ...
  }
  ```

  전체 예제는 [트리거 - 미리 컴파일된 C# 예제](#trigger---c-example)를 참조하세요.

* [ServiceBusAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)는 [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus) NuGet 패키지에 정의되어 있습니다.

  사용할 Service Bus 계정을 지정하는 다른 방법을 제공합니다. 생성자는 Service Bus 연결 문자열을 포함하는 앱 설정의 이름을 사용합니다. 매개 변수, 메서드 또는 클래스 수준에서 특성을 적용할 수 있습니다. 다음 예제에서는 클래스 수준 및 메서드 수준을 보여줍니다.

  ```csharp
  [ServiceBusAccount("ClassLevelServiceBusAppSetting")]
  public static class AzureFunctions
  {
      [ServiceBusAccount("MethodLevelServiceBusAppSetting")]
      [FunctionName("ServiceBusQueueTriggerCSharp")]
      public static void Run(
          [ServiceBusTrigger("myqueue", AccessRights.Manage)] 
          string myQueueItem, TraceWriter log)
  {
      ...
  }
  ```

사용할 Service Bus 계정은 다음과 같은 순서로 결정됩니다.

* `ServiceBusTrigger` 특성의 `Connection` 속성
* `ServiceBusTrigger` 특성과 동일한 매개 변수에 적용된 `ServiceBusAccount` 특성
* 함수에 적용된 `ServiceBusAccount` 특성
* 클래스에 적용된 `ServiceBusAccount` 특성
* "AzureWebJobsServiceBus" 앱 설정입니다.

## <a name="trigger---configuration"></a>트리거 - 구성

다음 표에서는 *function.json* 파일 및 `ServiceBusTrigger` 특성에 설정된 바인딩 구성 속성을 설명합니다.

|function.json 속성 | 특성 속성 |설명|
|---------|---------|----------------------|
|**type** | 해당 없음 | "serviceBusTrigger"로 설정해야 합니다. 이 속성은 사용자가 Azure Portal에서 트리거를 만들 때 자동으로 설정됩니다.|
|**direction** | 해당 없음 | "in"으로 설정해야 합니다. 이 속성은 사용자가 Azure Portal에서 트리거를 만들 때 자동으로 설정됩니다. |
|**name** | 해당 없음 | 함수 코드에서 큐 또는 토픽 메시지를 나타내는 변수의 이름입니다. "$return"으로 설정하여 함수 반환 값을 참조합니다. | 
|**queueName**|**QueueName**|모니터링할 큐의 이름입니다.  토픽이 아닌 큐를 모니터링하는 경우에만 설정합니다.
|**topicName**|**TopicName**|모니터링할 토픽의 이름입니다. 큐가 아닌 토픽을 모니터링하는 경우에만 설정합니다.|
|**subscriptionName**|**SubscriptionName**|모니터링할 구독의 이름입니다. 큐가 아닌 토픽을 모니터링하는 경우에만 설정합니다.|
|**연결**|**연결**|이 바인딩에 사용할 Service Bus 연결 문자열을 포함하는 앱 설정의 이름입니다. 앱 설정 이름이 "AzureWebJobs"로 시작하는 경우 이름의 나머지만을 지정할 수 있습니다. 예를 들어 `connection`을 "MyServiceBus"로 설정한 경우 함수 런타임 기능은 "AzureWebJobsMyServiceBus"라는 앱 설정을 찾습니다. `connection`을 비워 두면 함수 런타임 기능은 "AzureWebJobsServiceBus"라는 앱 설정에서 기본 Service Bus 연결 문자열을 사용합니다.<br><br>연결 문자열을 얻으려면 [관리 자격 증명 얻기](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)에 나온 단계에 따릅니다. 연결 문자열은 Service Bus 네임스페이스에 대한 것이어야 하며, 특정 큐 또는 항목으로 제한되지 않습니다. |
|**accessRights**|**Access**|연결 문자열에 대한 액세스 권한입니다. 사용 가능한 값은 `manage` 및 `listen`입니다. 기본값은 `manage`이며, `connection`에 **관리** 권한이 있음을 의미합니다. **관리** 권한이 없는 연결 문자열을 사용하는 경우 `accessRights`을 "listen"으로 설정합니다. 그렇지 않으면 함수 런타임은 관리 권한이 필요한 작업 시도를 실패할 수 있습니다.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---usage"></a>트리거 - 사용

C# 및 C# 스크립트에서는 `string paramName`과 같은 메서드 매개 변수를 사용하여 큐 및 토픽 메시지에 액세스합니다. C# 스크립트에서 `paramName`은 *function.json*의 `name` 속성에 지정된 값입니다. `string` 대신 다음 형식 중 하나를 사용할 수 있습니다.

* `byte[]` - 이진 데이터에 유용합니다.
* 사용자 지정 형식 - 메시지에 JSON이 포함된 경우 Azure Functions는 JSON 데이터를 deserialize하려고 합니다.
* `BrokeredMessage` - [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) 메서드를 사용하는 deserialize된 메시지가 표시됩니다.

JavaScript에서 `context.bindings.<name>`를 사용하여 큐 또는 토픽 메시지에 액세스합니다. `<name>`은 *function.json*의 `name` 속성에 지정된 값입니다. Service Bus 메시지가 문자열 또는 JSON 개체로 함수에 전달됩니다.

## <a name="trigger---poison-messages"></a>트리거 - 포이즌 메시지

포이즌 메시지 처리는 Azure Functions에서 제어되거나 구성될 수 없습니다. Service Bus는 스스로 포이즌 메시지를 처리합니다.

## <a name="trigger---peeklock-behavior"></a>트리거 - PeekLock 동작

Functions 런타임은 [PeekLock 모드](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode)로 메시지를 수신합니다. 함수가 성공적으로 완료된 경우 메시지에서 `Complete`를 호출하고, 함수가 실패한 경우 `Abandon`을 호출합니다. 함수가 `PeekLock` 시간 제한보다 오래 실행되는 경우 잠금이 자동으로 갱신됩니다.

## <a name="trigger---hostjson-properties"></a>트리거 - host.json 속성

[host.json](functions-host-json.md#servicebus) 파일에는 Service Bus 트리거 동작을 제어하는 설정이 포함됩니다.

[!INCLUDE [functions-host-json-event-hubs](../../includes/functions-host-json-service-bus.md)]

## <a name="output"></a>출력

Azure Service Bus 출력 바인딩을 사용하여 큐 또는 토픽 메시지를 보냅니다.

## <a name="output---example"></a>출력 - 예제

언어 관련 예제를 참조하세요.

* [미리 컴파일된 C#](#output---c-example)
* [C# 스크립트](#output---c-script-example)
* [F#](#output---f-example)
* [JavaScript](#output---javascript-example)

### <a name="output---c-example"></a>출력 - C# 예제

다음 예제에서는 Service Bus 큐 메시지를 보내는 [미리 컴파일된 C# 함수](functions-dotnet-class-library.md)를 보여줍니다.

```cs
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```

### <a name="output---c-script-example"></a>출력 - C# 스크립트 예제

다음 예에서는 *function.json* 파일의 Service Bus 출력 바인딩 및 바인딩을 사용하는 [C# 스크립트 함수](functions-reference-csharp.md)를 보여줍니다. 함수는 타이머 트리거를 사용하여 15초마다 큐 메시지를 보냅니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

단일 메시지를 만드는 C# 스크립트 코드는 다음과 같습니다.

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

여러 메시지를 만드는 C# 스크립트 코드는 다음과 같습니다.

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue messages created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

### <a name="output---f-example"></a>출력 - F# 예제

다음 예에서는 *function.json* 파일의 Service Bus 출력 바인딩 및 바인딩을 사용하는 [F# 스크립트 함수](functions-reference-fsharp.md)를 보여줍니다. 함수는 타이머 트리거를 사용하여 15초마다 큐 메시지를 보냅니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

단일 메시지를 만드는 F# 스크립트 코드는 다음과 같습니다.

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

### <a name="output---javascript-example"></a>출력 - JavaScript 예제

다음 예에서는 *function.json* 파일의 Service Bus 출력 바인딩 및 바인딩을 사용하는 [JavaScript 함수](functions-reference-node.md)를 보여줍니다. 함수는 타이머 트리거를 사용하여 15초마다 큐 메시지를 보냅니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

단일 메시지를 만드는 JavaScript 스크립트 코드는 다음과 같습니다.

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

여러 메시지를 만드는 JavaScript 스크립트 코드는 다음과 같습니다.

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="output---attributes"></a>출력 - 특성

[미리 컴파일된 C#](functions-dotnet-class-library.md) 함수의 경우 [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus) NuGet 패키지에 정의되어 있는 [ServiceBusAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs) 특성을 사용합니다.

특성의 생성자는 큐의 이름 또는 토픽과 구독을 사용합니다. 연결의 액세스 권한을 지정할 수도 있습니다. 액세스 권한을 설정을 선택하는 방법은 [출력 - 구성](#output---configuration) 섹션에서 설명합니다. 함수의 반환 값에 적용된 특성을 보여주는 예제는 다음과 같습니다.

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue")]
public static string Run([HttpTrigger] dynamic input, TraceWriter log)
{
    ...
}
```

다음 예와 같이 사용할 Service Bus 계정을 지정하도록 `Connection` 속성을 설정할 수 있습니다.

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string Run([HttpTrigger] dynamic input, TraceWriter log)
{
    ...
}
```

전체 예제는 [출력 - 미리 컴파일된 C# 예제](#output---c-example)를 참조하세요.

`ServiceBusAccount` 특성을 사용하여 클래스, 메서드 또는 매개 변수 수준에서 사용할 Service Bus 계정을 지정합니다.  자세한 내용은 [트리거 - 특성](#trigger---attributes-for-precompiled-c)을 참조하세요.

## <a name="output---configuration"></a>출력 - 구성

다음 표에서는 *function.json* 파일 및 `ServiceBus` 특성에 설정된 바인딩 구성 속성을 설명합니다.

|function.json 속성 | 특성 속성 |설명|
|---------|---------|----------------------|
|**type** | 해당 없음 | "serviceBus"로 설정해야 합니다. 이 속성은 사용자가 Azure Portal에서 트리거를 만들 때 자동으로 설정됩니다.|
|**direction** | 해당 없음 | "out"으로 설정해야 합니다. 이 속성은 사용자가 Azure Portal에서 트리거를 만들 때 자동으로 설정됩니다. |
|**name** | 해당 없음 | 함수 코드에서 큐 또는 토픽을 나타내는 변수의 이름입니다. "$return"으로 설정하여 함수 반환 값을 참조합니다. | 
|**queueName**|**QueueName**|큐의 이름입니다.  토픽이 아닌 큐 메시지를 보내는 경우에만 설정합니다.
|**topicName**|**TopicName**|모니터링할 토픽의 이름입니다. 큐가 아닌 토픽 메시지를 보내는 경우에만 설정합니다.|
|**subscriptionName**|**SubscriptionName**|모니터링할 구독의 이름입니다. 큐가 아닌 토픽 메시지를 보내는 경우에만 설정합니다.|
|**연결**|**연결**|이 바인딩에 사용할 Service Bus 연결 문자열을 포함하는 앱 설정의 이름입니다. 앱 설정 이름이 "AzureWebJobs"로 시작하는 경우 이름의 나머지만을 지정할 수 있습니다. 예를 들어 `connection`을 "MyServiceBus"로 설정한 경우 함수 런타임 기능은 "AzureWebJobsMyServiceBus"라는 앱 설정을 찾습니다. `connection`을 비워 두면 함수 런타임 기능은 "AzureWebJobsServiceBus"라는 앱 설정에서 기본 Service Bus 연결 문자열을 사용합니다.<br><br>연결 문자열을 얻으려면 [관리 자격 증명 얻기](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)에 나온 단계에 따릅니다. 연결 문자열은 Service Bus 네임스페이스에 대한 것이어야 하며, 특정 큐 또는 항목으로 제한되지 않습니다.|
|**accessRights**|**Access** |연결 문자열에 대한 액세스 권한입니다. 사용 가능한 값은 "manage" 및 "listen"입니다. 기본값은 "manage"이며, 연결에 **관리** 권한이 있음을 의미합니다. **관리** 권한이 없는 연결 문자열을 사용하는 경우 `accessRights`을 "listen"으로 설정합니다. 그렇지 않으면 함수 런타임은 관리 권한이 필요한 작업 시도를 실패할 수 있습니다.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a>출력 - 사용

C# 및 C# 스크립트에서는 `out string paramName`과 같은 메서드 매개 변수를 사용하여 큐 및 토픽에 액세스합니다. C# 스크립트에서 `paramName`은 *function.json*의 `name` 속성에 지정된 값입니다. 다음 매개 변수 형식 중 하나를 사용할 수 있습니다.

* `out T paramName` - `T`는 JSON 직렬화 가능 형식일 수 있습니다. 함수가 종료될 때 매개 변수 값이 null이면 함수는 null 개체와 메시지를 만듭니다.
* `out string` - 함수가 종료될 때 매개 변수 값이 null인 경우 함수는 메시지를 만들지 않습니다.
* `out byte[]` - 함수가 종료될 때 매개 변수 값이 null인 경우 함수는 메시지를 만들지 않습니다.
* `out BrokeredMessage` - 함수가 종료될 때 매개 변수 값이 null인 경우 함수는 메시지를 만들지 않습니다.

C# 또는 C# 스크립트 함수에서 여러 메시지를 만들려면, `ICollector<T>` 또는 `IAsyncCollector<T>`를 사용할 수 있습니다. 메시지는 `Add` 메서드를 호출할 때 생성됩니다.

JavaScript에서 `context.bindings.<name>`를 사용하여 큐 또는 토픽에 액세스합니다. `<name>`은 *function.json*의 `name` 속성에 지정된 값입니다. 문자열, 바이트 배열 또는 Javascript 개체(JSON으로 deserialize됨)를 `context.binding.<name>`에 할당할 수 있습니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Azure Functions 트리거 및 바인딩에 대한 자세한 정보](functions-triggers-bindings.md)
