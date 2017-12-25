---
title: "Docker 프로덕션 환경 실행, 관리 및 모니터링"
description: "Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 응용 프로그램 수명 주기"
keywords: "Docker, 마이크로 서비스, ASP.NET, 컨테이너"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.openlocfilehash: e377a5ec4b34a1ae25246747cf652a22064b8ffd
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="run-manage-and-monitor-docker-production-environments"></a><span data-ttu-id="8f8f7-104">Docker 프로덕션 환경 실행, 관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="8f8f7-104">Run, manage, and monitor Docker production environments</span></span>

<span data-ttu-id="8f8f7-105">비전: 엔터프라이즈 응용 프로그램은 고가용성 및 고확장성과 함께 실행되어야 합니다. IT 운영팀은 자체적으로 환경과 응용 프로그램을 관리하고 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-105">Vision: Enterprise applications need to run with high availability and high scalability; IT operations need to be able to manage and monitor the environments and the applications themselves.</span></span>

<span data-ttu-id="8f8f7-106">컨테이너화된 Docker 응용 프로그램 수명 주기의 이 마지막 단계에서는 확장 가능한 고가용성(HA) 프로덕션 환경에서 응용 프로그램을 실행, 관리 및 모니터링할 수 있는 방법을 중점적으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-106">This last pillar in the containerized Docker applications life cycle is centered on how you can run, manage, and monitor your applications in scalable, high availability (HA) production environments.</span></span>

<span data-ttu-id="8f8f7-107">프로덕션 환경(인프라 아키텍처 및 플랫폼 기술)에서 컨테이너화된 응용 프로그램을 실행하는 방법은 이 전자책의 챕터 1에서 살펴본 선택된 아키텍처와 개발 플랫폼에 따라 완전히 달라지며, 매우 깊은 연관성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-107">How you run your containerized applications in production (infrastructure architecture and platform technologies) is also very much related and completely founded on the chosen architecture and development platforms that we looked at in the Chapter 1 of this e-book.</span></span> <span data-ttu-id="8f8f7-108">이 챕터에서는 고확장성, HA를 지원하는 분산 응용 프로그램을 효과적으로 실행하는 데 사용할 수 있는 Microsoft 및 다른 공급업체의 특정 제품 및 기술을 살펴보고, 이러한 제품 및 기술을 관리하고 모니터링하는 방법을 IT 관점에서 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-108">This chapter examines specific products and technologies from Microsoft and other vendors that you can use to effectively run highly scalable, HA distributed applications plus how you can manage and monitor them from the IT perspective.</span></span>


>[!div class="step-by-step"]
<span data-ttu-id="8f8f7-109">[이전] (../docker-devops-workflow/docker-application-outer-loop-devops-workflow.md) [다음] (run-microservices-based-applications-in-production.md)</span><span class="sxs-lookup"><span data-stu-id="8f8f7-109">[Previous] (../docker-devops-workflow/docker-application-outer-loop-devops-workflow.md) [Next] (run-microservices-based-applications-in-production.md)</span></span>