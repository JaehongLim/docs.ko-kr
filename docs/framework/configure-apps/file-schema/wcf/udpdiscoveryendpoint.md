---
title: "&lt;udpDiscoveryEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f485329-2771-43bc-88de-df8f2faa3bb7
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;udpDiscoveryEndpoint&gt;
이 구성 요소는 UDP 멀티캐스트 바인딩을 통한 검색 작업에 대해 미리 구성된 표준 끝점을 정의합니다.  이 끝점에는 고정된 계약이 있으며 두 가지 버전의 WS\-Discovery 프로토콜을 지원합니다.  또한 WS\-Discovery 사양\(WS\-Discovery April 2005 또는 WS\-Discovery V1.1\)에 지정된 고정된 UDP 바인딩 및 기본 주소가 있습니다.  
  
## 구문  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <discoveryEndpoint>   
          <standardEndpoint  
                  discoveryMode=”Adhoc/Managed”  
                  discoveryVersion=”WSDiscovery11/WSDiscoveryApril2005”  
                  maxResponseDelay=”Timespan”  
                  multicastAddress=”Uri”   
                  name="String" />  
       </discoveryEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## 특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### 특성  
  
|특성|설명|  
|--------|--------|  
|discoveryMode|검색 프로토콜의 모드를 지정하는 문자열입니다.  유효한 값은 "Adhoc" 및 "Managed"입니다.  관리 모드에서는 프로토콜이 검색 가능한 서비스의 리포지토리로 작동하는 검색 프록시를 사용하고,  애드혹 모드에서는 프로토콜이 UDP 멀티캐스트 메커니즘을 사용하여 사용 가능한 서비스를 찾아야 합니다.  이 값은 <xref:System.Servicemodel.Discovery.DiscoveryMode> 형식입니다.|  
|discoveryVersion|WS\-Discovery 프로토콜의 두 버전 중 하나를 지정하는 문자열입니다.  유효한 값은 WSDiscovery11 및 WSDiscoveryApril2005입니다.  이 값은 <xref:System.Servicemodel.Discovery.DiscoveryVersion> 형식입니다.|  
|maxResponseDelay|검색 프로토콜이 Probe Match 또는 Resolve Match 같은 특정 메시지가 전송될 때까지 대기하는 최대 지연 값을 지정하는 Timespan 값입니다.<br /><br /> 모든 Probe Match가 동시에 전송되는 경우 네트워크 폭주가 발생할 수 있습니다.  이러한 현상이 발생하는 것을 방지하기 위해 각 Probe Match 사이에 임의의 지연 간격을 두고 Probe Match가 전송됩니다.  0에서 이 특성에 의해 설정되는 값까지의 범위 내에서 임의의 지연 간격이 설정됩니다.  이 특성이 0으로 설정되면 Probe Match 메시지가 지연 간격 없이 연속하여 전송됩니다.  그렇지 않으면 모든 Probe Match 메시지를 보내는 데 걸리는 총 시간이 maxResponseDelay를 초과하지 않는 범위 내에서 Probe Match 메시지가 약간의 임의의 지연 간격을 두고 전송됩니다.  이 값은 서비스에만 관련된 것으로 클라이언트에서 사용되는 값은 아닙니다.|  
|multicastAddress|검색 메시지를 보내고 받는 데 사용할 멀티캐스트 주소를 지정하는 URI입니다.  기본값은 프로토콜 사양을 따르는 멀티캐스트 주소입니다.|  
|`name`|표준 끝점의 구성 이름을 지정하는 문자열입니다.  이 이름은 서비스 끝점의 `endpointConfiguration` 특성에서 표준 끝점을 해당 구성에 연결하기 위해 사용됩니다.|  
  
### 자식 요소  
  
|요소|설명|  
|--------|--------|  
|[\<udpTransportSettings\>](../../../../../docs/framework/configure-apps/file-schema/wcf/udptransportsettings.md)|UDP 끝점에 대한 UDP 전송을 구성할 수 있도록 하는 설정의 컬렉션입니다.|  
  
### 부모 요소  
  
|요소|설명|  
|--------|--------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|하나 이상의 속성\(주소, 바인딩, 계약\)이 고정된 미리 정의된 끝점인 표준 끝점의 컬렉션입니다.|  
  
## 예제  
 다음 예제에서는 UDP 멀티캐스트 전송을 통해 검색 메시지를 수신하는 서비스를 보여 줍니다.  
  
```  
  
<services>  
    <service name="CalculatorService"  
         behaviorConfiguration="CalculatorServiceBehavior">  
         <endpoint binding="basicHttpBinding"   
           address="calculator" contract="ICalculatorService" />  
         <endpoint name="DiscoveryEndpoint"  
                kind="udpDiscoveryEndpoint" />  
</service>  
<standardEndpoints>  
  <udpDiscoveryEndpoint>  
     <standardEndpoint name="DiscoveryEndpoint"                         
                       version="WSDiscoveryApril2005" />  
   </udpDiscoveryEndpoint>  
</standardEndpoints>  
  
```  
  
## 참고 항목  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>