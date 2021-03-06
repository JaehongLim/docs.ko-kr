---
title: "방법: 낮은 수준의 동기화에 SpinLock 사용"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinLock, how to use
ms.assetid: a9ed3e4e-4f29-4207-b730-ed0a51ecbc19
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 11d41a1fd04039fd08d945a72a37a479f79449a5
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/23/2017
---
# <a name="how-to-use-spinlock-for-low-level-synchronization"></a>방법: 낮은 수준의 동기화에 SpinLock 사용
다음 예제는 <xref:System.Threading.SpinLock> 사용 방법을 보여줍니다.  
  
## <a name="example"></a>예  
 이 예제에서 중요 섹션은 최소한의 작업을 수행하여 <xref:System.Threading.SpinLock>에 대해 적합한 후보를 만듭니다. 작업을 약간 늘리면 표준 잠금과 비교하여 <xref:System.Threading.SpinLock>의 성능이 향상됩니다. 그러나 SpinLock이 표준 잠금보다 비용이 드는 지점이 있습니다. 프로파일링 도구에서 동시성 프로파일링 기능을 사용하여 어떤 유형의 잠금이 프로그램에서 더 나은 성능을 제공하는지 확인할 수 있습니다. 자세한 내용은 [동시성 시각화 도우미](/visualstudio/profiling/concurrency-visualizer)를 참조하세요.  
  
 [!code-csharp[CDS_SpinLock#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#02)]
 [!code-vb[CDS_SpinLock#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_vb.vb#02)]  
  
 <xref:System.Threading.SpinLock>은 공유 리소스에 대한 잠금을 오랫동안 유지하지 않는 경우에 유용할 수 있습니다. 이러한 경우에 다중 코어 컴퓨터에서 차단된 스레드를 잠금이 해제될 때까지 몇 차례 회전하는 것이 효율적입니다. CPU를 많이 사용하는 프로세스이기 때문에 회전함으로써 스레드가 차단되지 않습니다. <xref:System.Threading.SpinLock>은 특정 조건에서 회전을 중지하여 논리 프로세서의 부족 또는 하이퍼 스레딩을 포함한 시스템에서의 우선 순위 반전을 방지합니다.  
  
 이 예제에서는 다중 스레드 액세스를 위해 사용자 동기화가 필요한 <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> 클래스를 사용합니다. .NET Framework 버전 4를 대상으로 하는 응용 프로그램에서 다른 옵션은 사용자 잠금이 필요하지 않은 <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType>를 사용하는 것입니다.  
  
 <xref:System.Threading.SpinLock.Exit%2A>에 대한 호출에서 `false`(Visual Basic의 경우 `False`)를 사용합니다. 그러면 최상의 성능을 제공합니다. IA64 아키텍처에서 `true`(`True`)을 지정하여 메모리 담장을 사용합니다. 그러면 쓰기 버퍼를 플러시하여 종료할 다른 스레드에서 잠금을 사용할 수 있는지 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [스레딩 개체 및 기능](../../../docs/standard/threading/threading-objects-and-features.md)
