---
title: "방법: 대리자 메서드 호출(Visual Basic)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
ms.assetid: b56866ae-abf9-4a5a-a855-486359455e9c
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: ea94d4bb26e168667fd75c6928e52261f230c85e
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-invoke-a-delegate-method-visual-basic"></a>방법: 대리자 메서드 호출(Visual Basic)
이 예제에는 하는 메서드는 대리자를 연결 하 고 다음 대리자를 통해 해당 메서드를 호출 하는 방법을 보여 줍니다.  
  
### <a name="create-the-delegate-and-matching-procedures"></a>대리자와 일치 하는 프로시저 만들기  
  
1.  라는 대리자를 만들 `MySubDelegate`합니다.  
  
    ```  
    Delegate Sub MySubDelegate(ByVal x As Integer)  
    ```  
  
2.  대리자와 동일한 서명으로 메서드를 포함 하는 클래스를 선언 합니다.  
  
    ```  
    Class class1  
        Sub Sub1(ByVal x As Integer)  
            MsgBox("The value of x is: " & CStr(x))  
        End Sub  
    End Class  
    ```  
  
3.  대리자의 인스턴스를 만들고 기본 제공을 호출 하 여 해당 대리자와 연결 된 메서드를 호출 하는 메서드를 정의 `Invoke` 메서드.  
  
    ```  
    Protected Sub DelegateTest()  
        Dim c1 As New class1  
        ' Create an instance of the delegate.  
        Dim msd As MySubDelegate = AddressOf c1.Sub1  
        ' Call the method.  
        msd.Invoke(10)  
    End Sub  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [Delegate 문](../../../../visual-basic/language-reference/statements/delegate-statement.md)  
 [대리자](../../../../visual-basic/programming-guide/language-features/delegates/index.md)  
 [이벤트](../../../../visual-basic/programming-guide/language-features/events/index.md)  
 [다중 스레드 응용 프로그램](http://msdn.microsoft.com/library/a06a1a56-dd16-44e8-bc01-2c2255511bc6)
