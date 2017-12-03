---
title: "일부 오류를 처리 하기 위한 전략"
description: "컨테이너 화 된.NET 응용 프로그램에 대 한.NET Microservices 아키텍처 | 일부 오류를 처리 하기 위한 전략"
keywords: "Docker, 마이크로 서비스, ASP.NET, 컨테이너"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: ff3bed530b13a9b1822c7cccf5a4d47df6fc6239
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="strategies-for-handling-partial-failure"></a><span data-ttu-id="efd79-104">일부 오류를 처리 하기 위한 전략</span><span class="sxs-lookup"><span data-stu-id="efd79-104">Strategies for handling partial failure</span></span>

<span data-ttu-id="efd79-105">부분적인 오류를 처리 하기 위한 전략은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-105">Strategies for dealing with partial failures include the following.</span></span>

<span data-ttu-id="efd79-106">**비동기 통신 (예를 들어 메시지 기반 통신)를 사용 하 여 내부 microservices 걸쳐**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-106">**Use asynchronous communication (for example, message-based communication) across internal microservices**.</span></span> <span data-ttu-id="efd79-107">항상을 잘못 된 해당 디자인에는 잘못 되었습니다. 중단의 주요 원인 결국 때문에 내부 microservices에서 긴 체인 HTTP에 대 한 동기 호출을 만들지 않도록는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-107">It is highly advisable not to create long chains of synchronous HTTP calls across the internal microservices because that incorrect design will eventually become the main cause of bad outages.</span></span> <span data-ttu-id="efd79-108">반대로, 클라이언트 응용 프로그램과 첫 번째 수준의 microservices 또는 세분화 된 API 게이트웨이 간의 통신의 프런트 엔드를 제외 하 고 것이 좋습니다 비동기 (메시지 기반) 통신만 초기 요청을 지 나 한 번만 사용 하도록 / 내부 microservices 걸쳐 응답 주기가</span><span class="sxs-lookup"><span data-stu-id="efd79-108">On the contrary, except for the front-end communications between the client applications and the first level of microservices or fine-grained API Gateways, it is recommended to use only asynchronous (message-based) communication once past the initial request/response cycle, across the internal microservices.</span></span> <span data-ttu-id="efd79-109">결과적 일관성 및 이벤트 기반 아키텍처 ripple 영향을 최소화 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-109">Eventual consistency and event-driven architectures will help to minimize ripple effects.</span></span> <span data-ttu-id="efd79-110">이러한 방법을 사용 더 높은 수준의 자율성 마이크로 서비스를 강제 적용 되 고 따라서 여기서 설명 하는 문제를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-110">These approaches enforce a higher level of microservice autonomy and therefore prevent against the problem noted here.</span></span>

<span data-ttu-id="efd79-111">**재시도 지 수 백오프를 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-111">**Use retries with exponential backoff**.</span></span> <span data-ttu-id="efd79-112">짧은 하지 않으려면이 방법을 사용 하면 및 호출을 수행 하 여 일시적인 오류가 경우 서비스에서 짧은 시간에만 사용할 수 없습니다. 몇 번의 다시 시도 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-112">This technique helps to avoid short and intermittent failures by performing call retries a certain number of times, in case the service was not available only for a short time.</span></span> <span data-ttu-id="efd79-113">마이크로 서비스/컨테이너를 클러스터의 다른 노드로 이동할 때 또는 일시적인 네트워크 문제로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-113">This might occur due to intermittent network issues or when a microservice/container is moved to a different node in a cluster.</span></span> <span data-ttu-id="efd79-114">그러나 이러한 재시도 없는 경우 제대로 회로 차단기와, 그 수 aggravate ripple 효과 바꾸지 궁극적으로 [서비스 거부 (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack)합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-114">However, if these retries are not designed properly with circuit breakers, it can aggravate the ripple effects, ultimately even causing a [Denial of Service (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack).</span></span>

<span data-ttu-id="efd79-115">**네트워크 제한 시간 까지의 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-115">**Work around network timeouts**.</span></span> <span data-ttu-id="efd79-116">일반적으로 클라이언트를 무기한으로 차단 하지 않도록 하 고 응답을 받기 위해 대기 하는 경우 항상 제한 시간을 사용 하도록 설계 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-116">In general, clients should be designed not to block indefinitely and to always use timeouts when waiting for a response.</span></span> <span data-ttu-id="efd79-117">시간 제한을 사용 하는 리소스는 되지 하느라 정체 무기한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-117">Using timeouts ensures that resources are never tied up indefinitely.</span></span>

<span data-ttu-id="efd79-118">**회로 차단기 패턴을 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-118">**Use the Circuit Breaker pattern**.</span></span> <span data-ttu-id="efd79-119">이 방법에서는 클라이언트 프로세스 실패 한 요청 수를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-119">In this approach, the client process tracks the number of failed requests.</span></span> <span data-ttu-id="efd79-120">오류 비율 즉시 시도가 실패 하는 구성 된 제한 "회로 차단 기가" trips을 초과 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-120">If the error rate exceeds a configured limit, a “circuit breaker” trips so that further attempts fail immediately.</span></span> <span data-ttu-id="efd79-121">(많은 수의 요청 실패 하는 경우 제시 요청을 보낼 무의미 한 인지 하 고 서비스를 사용할 수 없습니다.) 제한 시간 후 클라이언트 해야 다시 시도 하 고, 새 요청은 성공 하는 경우 회로 차단기를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-121">(If a large number of requests are failing, that suggests the service is unavailable and that sending requests is pointless.) After a timeout period, the client should try again and, if the new requests are successful, close the circuit breaker.</span></span>

<span data-ttu-id="efd79-122">**대체 제공**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-122">**Provide fallbacks**.</span></span> <span data-ttu-id="efd79-123">이 방법에서는 클라이언트 프로세스에서 캐시 된 데이터 또는 기본값을 반환 하는 등의 요청이 실패할 경우 대체 논리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-123">In this approach, the client process performs fallback logic when a request fails, such as returning cached data or a default value.</span></span> <span data-ttu-id="efd79-124">쿼리에 대 한 적합 한 접근 방식을 이며 업데이트 또는 명령에 대 한 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-124">This is an approach suitable for queries, and is more complex for updates or commands.</span></span>

<span data-ttu-id="efd79-125">**큐 대기 요청 수가 제한**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-125">**Limit the number of queued requests**.</span></span> <span data-ttu-id="efd79-126">클라이언트는 클라이언트 마이크로 서비스를 특정 서비스에 보낼 수 있는 처리 중인 요청 수에 대 한 상한 값을 입력할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-126">Clients should also impose an upper bound on the number of outstanding requests that a client microservice can send to a particular service.</span></span> <span data-ttu-id="efd79-127">제한에 도달 하면 추가 요청을 만드는 무의미 한 것 이며 재전송 시도 즉시 중단 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-127">If the limit has been reached, it is probably pointless to make additional requests, and those attempts should fail immediately.</span></span> <span data-ttu-id="efd79-128">관 구현 측면에서 [Bulkhead 격리](https://github.com/App-vNext/Polly/wiki/Bulkhead) 정책이 요구이 사항을 충족 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-128">In terms of implementation, the Polly [Bulkhead Isolation](https://github.com/App-vNext/Polly/wiki/Bulkhead) policy can be used to fulfil this requirement.</span></span> <span data-ttu-id="efd79-129">이 방법은와 병렬화 스로틀 [SemaphoreSlim](https://docs.microsoft.com/dotnet/api/system.threading.semaphoreslim?view=netcore-1.1) 구현으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-129">This approach is essentially a parallelization throttle with [SemaphoreSlim](https://docs.microsoft.com/dotnet/api/system.threading.semaphoreslim?view=netcore-1.1) as the implementation.</span></span> <span data-ttu-id="efd79-130">또한는 bulkhead 외부 "queue" 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-130">It also permits a "queue" outside the bulkhead.</span></span> <span data-ttu-id="efd79-131">(예를 들어 때문에 용량 완전 하다 고 판단 되) 실행 하기 전에 초과 부하를 늘리는 사전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-131">You can proactively shed excess load even before execution (for example, because capacity is deemed full).</span></span> <span data-ttu-id="efd79-132">이렇게 하면 특정 오류 시나리오에 대 한 응답 회로 차단기는 오류에 대 한 대기 하므로 회로 차단기 될 것 보다 더 빠르게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-132">This makes its response to certain failure scenarios faster than a circuit breaker would be, since the circuit breaker waits for the failures.</span></span> <span data-ttu-id="efd79-133">관 BulkheadPolicy 개체 노출 사용률이 bulkhead 및 큐는 고 오버플로가 제공 이벤트 하므로 수 있습니다 사용할 수도 자동화 된 수평 확장이 진행 하는 데 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-133">The BulkheadPolicy object in Polly exposes how full the bulkhead and queue are, and offers events on overflow so can also be used to drive automated horizontal scaling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efd79-134">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="efd79-134">Additional resources</span></span>

-   <span data-ttu-id="efd79-135">**복원 력 패턴**
    [*https://docs.microsoft.com/azure/architecture/patterns/category/resiliency*](https://docs.microsoft.com/azure/architecture/patterns/category/resiliency)</span><span class="sxs-lookup"><span data-stu-id="efd79-135">**Resiliency patterns**
[*https://docs.microsoft.com/azure/architecture/patterns/category/resiliency*](https://docs.microsoft.com/azure/architecture/patterns/category/resiliency)</span></span>

-   <span data-ttu-id="efd79-136">**추가 복원 력 및 성능 최적화**
    [*https://msdn.microsoft.com/en-us/library/jj591574.aspx*](https://msdn.microsoft.com/en-us/library/jj591574.aspx)</span><span class="sxs-lookup"><span data-stu-id="efd79-136">**Adding Resilience and Optimizing Performance**
[*https://msdn.microsoft.com/en-us/library/jj591574.aspx*](https://msdn.microsoft.com/en-us/library/jj591574.aspx)</span></span>

-   <span data-ttu-id="efd79-137">**Bulkhead 합니다.**</span><span class="sxs-lookup"><span data-stu-id="efd79-137">**Bulkhead.**</span></span> <span data-ttu-id="efd79-138">GitHub 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd79-138">GitHub repo.</span></span> <span data-ttu-id="efd79-139">관 정책 사용 하 여 구현 합니다. \ \\</span><span class="sxs-lookup"><span data-stu-id="efd79-139">Implementation with Polly policy.\\</span></span>
    [<span data-ttu-id="efd79-140">*https://github.com/App-vNext/Polly/wiki/Bulkhead*</span><span class="sxs-lookup"><span data-stu-id="efd79-140">*https://github.com/App-vNext/Polly/wiki/Bulkhead*</span></span>](https://github.com/App-vNext/Polly/wiki/Bulkhead)

-   <span data-ttu-id="efd79-141">**Azure에 대 한 복원 력 있는 응용 프로그램 디자인**
    [*https://docs.microsoft.com/azure/architecture/resiliency/*](https://docs.microsoft.com/azure/architecture/resiliency/)</span><span class="sxs-lookup"><span data-stu-id="efd79-141">**Designing resilient applications for Azure**
[*https://docs.microsoft.com/azure/architecture/resiliency/*](https://docs.microsoft.com/azure/architecture/resiliency/)</span></span>

-   <span data-ttu-id="efd79-142">**일시적인 오류 처리**
    <https://docs.microsoft.com/azure/architecture/best-practices/transient-faults></span><span class="sxs-lookup"><span data-stu-id="efd79-142">**Transient fault handling**
<https://docs.microsoft.com/azure/architecture/best-practices/transient-faults></span></span>


>[!div class="step-by-step"]
<span data-ttu-id="efd79-143">[이전] (핸들-부분-failure.md) [다음] (구현-다시 시도-지 수-backoff.md)</span><span class="sxs-lookup"><span data-stu-id="efd79-143">[Previous] (handle-partial-failure.md) [Next] (implement-retries-exponential-backoff.md)</span></span>