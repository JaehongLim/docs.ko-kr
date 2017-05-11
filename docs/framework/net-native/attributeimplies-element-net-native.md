---
title: "&lt;AttributeImplies&gt; 요소(.NET 네이티브) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 82db7193-a860-418b-84fc-fff2fdf2e025
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# &lt;AttributeImplies&gt; 요소(.NET 네이티브)
포함 특성이 적용되는 코드 요소에 대한 정책을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeImplies Activate="policy_type"  
                  Browse="policy_type"  
                  Dynamic="policy_type"  
                  Serialize="policy_type"   
                  DataContractSerializer="policy_setting"  
                  DataContractJsonSerializer="policy_setting"  
                  XmlSerializer="policy_setting"  
                  MarshalObject="policy_setting"  
                  MarshalDelegate="policy_setting"  
                  MarshalStructure="policy_setting" />  
  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 형식|설명|  
|---------------|--------------------|-----------------|  
|`Activate`|반사|선택적 특성입니다. 인스턴스를 활성화할 수 있도록 생성자에 대한 런타임 액세스를 제어합니다.|  
|`Browse`|반사|선택적 특성입니다. 프로그램 요소에 대한 정보 쿼리를 제어하지만 런타임 액세스를 사용하도록 설정하지는 않습니다.|  
|`Dynamic`|반사|선택적 특성입니다. 동적 프로그래밍을 수행할 수 있도록 생성자, 메서드, 필드, 속성 및 이벤트를 비롯한 모든 형식 멤버에 대한 런타임 액세스를 제어합니다.|  
|`Serialize`|Serialization|선택적 특성입니다. Newtonsoft JSON serializer 등의 라이브러리를 통해 형식 인스턴스를 serialize 및 deserialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.|  
|`DataContractSerializer`|Serialization|선택적 특성입니다. 정책을 사용 하는 serialization에 대 한 제어는 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> 클래스입니다.|  
|`DataContractJsonSerializer`|Serialization|선택적 특성입니다. 정책을 사용 하는 JSON serialization에 대 한 제어는 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> 클래스입니다.|  
|`XmlSerializer`|Serialization|선택적 특성입니다. 정책을 사용 하는 XML serialization에 대 한 제어는 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> 클래스입니다.|  
|`MarshalObject`|Interop|선택적 특성입니다. Windows 런타임 및 COM에 대한 참조 형식을 마샬링하는 정책을 제어합니다.|  
|`MarshalDelegate`|Interop|선택적 특성입니다. 네이티브 코드에 대한 함수 포인터로 대리자 형식을 마샬링하는 정책을 제어합니다.|  
|`MarshalStructure`|Interop|선택적 특성입니다. 값 형식을 네이티브 코드로 마샬링하는 정책을 제어합니다.|  
  
## <a name="all-attributes"></a>모든 특성  
  
|값|설명|  
|-----------|-----------------|  
|*policy_setting*|이 정책 형식에 적용할 설정입니다. 가능한 값은 `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` 및 `Required All`입니다. 자세한 내용은 참조 [런타임 지시문 정책 설정](../../../docs/framework/net-native/runtime-directive-policy-settings.md)합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
  
## <a name="remarks"></a>설명  
 `<AttributeImplies>` 요소는 포함 형식이 특성이 면 사용 됩니다 (즉,에서 파생 된 클래스 <xref:System.Attribute?displayProperty=fullName>). 특성이 특정 프로그램 요소에 적용되면 `<AttributeImplies>` 요소로 정의된 정책이 해당 프로그램 요소에 적용됩니다.  
  
 리플렉션, serialization 및 interop 특성은 모두 선택적 항목이지만 하나 이상 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [<>\>요소](../../../docs/framework/net-native/type-element-net-native.md)   
 [런타임 지시문 (rd.xml) 구성 파일 참조](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [런타임 지시문 요소](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [런타임 지시문 정책 설정](../../../docs/framework/net-native/runtime-directive-policy-settings.md)