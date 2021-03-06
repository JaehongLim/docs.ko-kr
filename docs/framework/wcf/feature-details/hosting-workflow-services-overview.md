---
title: "워크플로 서비스 호스팅 개요"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 19f3704f-06bf-4eeb-8724-5224e02d7ead
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 06012da95660fb4dc20d034c2d1691afad12037a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="hosting-workflow-services-overview"></a>워크플로 서비스 호스팅 개요
워크플로 서비스를 실행하려면 호스팅해야 합니다. <xref:System.ServiceModel.WorkflowServiceHost>는 여러 인스턴스, 구성 및 WCF 메시징(워크플로가 호스팅되기 위해 메시징을 사용할 필요는 없지만)을 지원하는 즉시 사용 가능한 워크플로 호스트로,  서비스 동작의 집합을 통해 지속성, 추적 및 인스턴스 제어와 통합됩니다.  WCF의 <xref:System.ServiceModel.ServiceHost>와 마찬가지로 <xref:System.ServiceModel.WorkflowServiceHost>는 모든 관리되는 .NET 응용 프로그램에서 자체 호스팅되거나 IIS/WAS에서 .xamlx 파일로 웹 호스팅될 수 있습니다.  이 단원의 항목에서는 워크플로 서비스를 호스팅하는 방법에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [워크플로 서비스 호스팅](../../../../docs/framework/wcf/feature-details/hosting-workflow-services.md)  
 워크플로 서비스 호스팅에 대해 설명합니다.  
  
 [워크플로 서비스 호스트 내부 기능](../../../../docs/framework/wcf/feature-details/workflow-service-host-internals.md)  
 <xref:System.ServiceModel.WorkflowServiceHost>가 들어오는 메시지를 처리하는 방법에 대해 설명합니다.  
  
 [워크플로 서비스 호스트 확장성](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)  
 워크플로 서비스 호스트의 기능을 확장하는 방법에 대해 설명합니다.  
  
 [워크플로 제어 끝점](../../../../docs/framework/wcf/feature-details/workflow-control-endpoint.md)  
 워크플로 인스턴스를 만들 수 있는 끝점을 정의하는 방법에 대해 설명합니다.  
  
 [방법: IIS에서 서비스가 아닌 워크플로 호스팅](../../../../docs/framework/wcf/feature-details/how-to-host-a-non-service-workflow-in-iis.md)  
 IIS에서 워크플로 서비스가 아닌 워크플로를 호스팅하는 방법을 보여 줍니다.  
  
 [방법: Windows Server AppFabric을 사용하여 워크플로 서비스 호스팅](../../../../docs/framework/wcf/feature-details/how-to-host-a-workflow-service-with-windows-server-app-fabric.md)  
 Windows Server AppFabric에서 기존 워크플로 서비스를 호스팅하는 방법을 보여 줍니다.  
  
 [WorkflowServiceHost 구성](../../../../docs/framework/wcf/feature-details/configuring-workflowservicehost.md)  
 지속성, 추적, 유휴 상태 및 처리되지 않은 예외 동작을 제어하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
 <xref:System.ServiceModel.Activities.WorkflowService>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactory>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactoryBase>  
  
 <xref:System.ServiceModel.Activation.WorkflowServiceHostFactory>  
  
## <a name="related-sections"></a>관련 단원  
 [워크플로 서비스](../../../../docs/framework/wcf/feature-details/workflow-services.md)
