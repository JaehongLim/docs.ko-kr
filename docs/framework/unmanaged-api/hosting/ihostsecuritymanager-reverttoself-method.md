---
title: "IHostSecurityManager::RevertToSelf 메서드"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostSecurityManager.RevertToSelf
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostSecurityManager::RevertToSelf
helpviewer_keywords:
- RevertToSelf method [.NET Framework hosting]
- IHostSecurityManager::RevertToSelf method [.NET Framework hosting]
ms.assetid: 189f28f8-f9a1-4192-aedc-91084e4f8b99
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 0fad325bc3df54f412a797e9944f5b1f38615786
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="ihostsecuritymanagerreverttoself-method"></a><span data-ttu-id="75ba6-102">IHostSecurityManager::RevertToSelf 메서드</span><span class="sxs-lookup"><span data-stu-id="75ba6-102">IHostSecurityManager::RevertToSelf Method</span></span>
<span data-ttu-id="75ba6-103">현재 사용자 id의 가장을 종료 하 고 원래 스레드 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-103">Terminates impersonation of the current user identity and returns the original thread token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="75ba6-104">구문</span><span class="sxs-lookup"><span data-stu-id="75ba6-104">Syntax</span></span>  
  
```  
HRESULT RevertToSelf ();  
```  
  
## <a name="return-value"></a><span data-ttu-id="75ba6-105">반환 값</span><span class="sxs-lookup"><span data-stu-id="75ba6-105">Return Value</span></span>  
  
|<span data-ttu-id="75ba6-106">HRESULT</span><span class="sxs-lookup"><span data-stu-id="75ba6-106">HRESULT</span></span>|<span data-ttu-id="75ba6-107">설명</span><span class="sxs-lookup"><span data-stu-id="75ba6-107">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="75ba6-108">S_OK</span><span class="sxs-lookup"><span data-stu-id="75ba6-108">S_OK</span></span>|<span data-ttu-id="75ba6-109">`RevertToSelf`성공적으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-109">`RevertToSelf` returned successfully.</span></span>|  
|<span data-ttu-id="75ba6-110">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="75ba6-110">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="75ba6-111">공용 언어 런타임 (CLR) 프로세스에 로드 되지 않았습니다 또는 CLR 중인 상태를 관리 코드를 실행 하거나 호출을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-111">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="75ba6-112">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="75ba6-112">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="75ba6-113">호출 시간이 초과 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-113">The call timed out.</span></span>|  
|<span data-ttu-id="75ba6-114">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="75ba6-114">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="75ba6-115">호출자에 게 잠금을 소유 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-115">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="75ba6-116">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="75ba6-116">HOST_E_ABANDONED</span></span>|<span data-ttu-id="75ba6-117">차단 된 스레드 이벤트 취소 되었습니다 또는 파이버가 기다리던 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-117">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="75ba6-118">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="75ba6-118">E_FAIL</span></span>|<span data-ttu-id="75ba6-119">알 수 없는 치명적인 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-119">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="75ba6-120">메서드가 E_FAIL을 반환 하는 경우 CLR을 하는 프로세스 내에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-120">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="75ba6-121">호스팅 방법에 대 한 후속 호출 HOST_E_CLRNOTAVAILABLE를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-121">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="75ba6-122">설명</span><span class="sxs-lookup"><span data-stu-id="75ba6-122">Remarks</span></span>  
 <span data-ttu-id="75ba6-123">`RevertToSelf`에 대 한 이전 호출 후 원래 스레드 토큰을 반환 하기 위해 호출 됩니다는 [ImpersonateLoggedOnUser](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-impersonateloggedonuser-method.md) 메서드.</span><span class="sxs-lookup"><span data-stu-id="75ba6-123">`RevertToSelf` is called to return to the original thread token, after an earlier call to the [ImpersonateLoggedOnUser](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-impersonateloggedonuser-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="75ba6-124">요구 사항</span><span class="sxs-lookup"><span data-stu-id="75ba6-124">Requirements</span></span>  
 <span data-ttu-id="75ba6-125">**플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75ba6-125">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="75ba6-126">**헤더:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="75ba6-126">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="75ba6-127">**라이브러리:** MSCorEE.dll에 리소스로 포함</span><span class="sxs-lookup"><span data-stu-id="75ba6-127">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="75ba6-128">**.NET framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="75ba6-128">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="75ba6-129">참고 항목</span><span class="sxs-lookup"><span data-stu-id="75ba6-129">See Also</span></span>  
 [<span data-ttu-id="75ba6-130">IHostSecurityContext 인터페이스</span><span class="sxs-lookup"><span data-stu-id="75ba6-130">IHostSecurityContext Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md)  
 [<span data-ttu-id="75ba6-131">IHostSecurityManager 인터페이스</span><span class="sxs-lookup"><span data-stu-id="75ba6-131">IHostSecurityManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-interface.md)  
 [<span data-ttu-id="75ba6-132">ImpersonateLoggedOnUser 메서드</span><span class="sxs-lookup"><span data-stu-id="75ba6-132">ImpersonateLoggedOnUser Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-impersonateloggedonuser-method.md)