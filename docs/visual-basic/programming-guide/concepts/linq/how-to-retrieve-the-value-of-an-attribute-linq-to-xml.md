---
title: "방법: 검색 (LINQ to XML) 특성의 값 (Visual Basic)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5f4b3790-c83f-4eb3-a889-e3587edf3ca1
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 5eed0c34f79a4a338dda7b26049f2c1510443736
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-visual-basic"></a>방법: 검색 (LINQ to XML) 특성의 값 (Visual Basic)
이 항목에서는 특성의 값을 가져오는 방법을 보여 줍니다. 두 가지 주요 방법이 있습니다. <xref:System.Xml.Linq.XAttribute>를 원하는 형식으로 캐스팅할 수 있습니다. 그러면 명시적 변환 연산자가 요소나 특성의 내용을 지정된 형식으로 변환합니다. 또는 <xref:System.Xml.Linq.XAttribute.Value%2A> 속성을 사용할 수 있습니다. 그러나 일반적으로 캐스팅이 더 나은 방법입니다. 특성을 nullable 형식으로 캐스팅하면 존재하지 않을 수도 있는 특성의 값을 검색하는 경우 코드를 더 간단하게 작성할 수 있습니다. 이 방법의 예 참조 [하는 방법: 요소 (LINQ to XML)의 값을 검색 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md)합니다.  
  
## <a name="example"></a>예제  
 Visual Basic에서는 통합 특성 속성을 사용하여 특성의 값을 검색할 수 있습니다.  
  
```vb  
Dim root As XElement = <Root Attr="abcde"/>  
Console.WriteLine(root)  
Dim str As String = root.@Attr  
Console.WriteLine(str)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>예제  
 Visual Basic에서는 통합 특성 속성을 사용하여 특성의 값을 설정할 수 있습니다. 또한 통합 특성 속성을 사용하여 존재하지 않는 특성의 값을 설정하는 경우 특성이 만들어집니다.  
  
```vb  
Dim root As XElement = <Root Att1="content"/>  
root.@Att1 = "new content"  
root.@Att2 = "new attribute"  
Console.WriteLine(root)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root Att1="new content" Att2="new attribute" />  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 특성이 네임스페이스에 있는 경우 특성의 값을 검색하는 방법을 보여 줍니다. 자세한 내용은 참조 [XML 네임 스페이스 (Visual Basic) 작업](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)합니다.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <aw:Root aw:Attr="abcde"/>  
        Dim str As String = root.@aw:Attr  
        Console.WriteLine(str)  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```  
abcde  
```  
  
## <a name="see-also"></a>참고 항목  
 [LINQ to XML 축(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
