---
title: "키보드 이벤트 사용"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- KeyPress event [Windows Forms]
- keyboards [Windows Forms], keyboard events
- KeyUp event
- KeyDown event
- keyboard events
- events [Windows Forms], keyboard
ms.assetid: d3f3e14b-a459-4ee6-9875-8957e34f8ee9
caps.latest.revision: "15"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 394ebc503338ad73001aa9859e0aa0d9c3fa42b4
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="using-keyboard-events"></a>키보드 이벤트 사용
대부분 Windows Forms 프로그램에서는 키보드 이벤트를 처리하는 방식으로 키보드 입력을 처리합니다. 이 항목에서는 각 이벤트를 사용하는 시기 및 각 이벤트에 대해 제공되는 데이터에 대한 세부 정보를 포함하여 키보드 이벤트에 대한 개요를 제공합니다.  또한 참조 [이벤트 처리기 개요 (Windows Forms)](http://msdn.microsoft.com/library/be6fx1bb\(v=vs.110\)), [이벤트 개요 (Windows Forms)](http://msdn.microsoft.com/library/1h12f09z\(v=vs.110\))합니다.  
  
## <a name="keyboard-events"></a>키보드 이벤트  
 Windows Forms에서는 사용자가 키보드 키를 누를 때 발생하는 두 가지 이벤트와 사용자가 키보드 키를 놓을 때 발생하는 한 가지 이벤트를 제공합니다.  
  
-   한 번 발생하는 <xref:System.Windows.Forms.Control.KeyDown> 이벤트.  
  
-   사용자가 같은 키를 누르고 있을 때 여러 번 발생할 수 있는 <xref:System.Windows.Forms.Control.KeyPress> 이벤트.  
  
-   사용자가 키를 놓을 때 한 번 발생하는 <xref:System.Windows.Forms.Control.KeyUp> 이벤트.  
  
 사용자가 키를 누를 때 Windows Forms에서는 키보드 메시지가 문자 키 또는 물리적 키를 지정하는지에 따라 발생할 이벤트를 결정합니다. 문자 및 물리적 키에 대 한 자세한 내용은 참조 [키보드 입력 작동 방식](../../../docs/framework/winforms/how-keyboard-input-works.md)합니다.  
  
 다음 표에서는 세 가지 키보드 이벤트에 대해 설명합니다.  
  
|키보드 이벤트|설명|결과|  
|--------------------|-----------------|-------------|  
|<xref:System.Windows.Forms.Control.KeyDown>|이 이벤트는 사용자가 물리적 키를 누를 때 발생합니다.|<xref:System.Windows.Forms.Control.KeyDown>에 대한 처리기는 다음을 수신합니다.<br /><br /> <ul><li>물리적 키보드 단추를 지정하는 <xref:System.Windows.Forms.KeyEventArgs.KeyCode%2A> 속성을 제공하는 <xref:System.Windows.Forms.KeyEventArgs> 매개 변수.</li><li><xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A> 속성(SHIFT, CTRL 또는 ALT).</li><li>키 코드 및 한정자를 결합하는 <xref:System.Windows.Forms.KeyEventArgs.KeyData%2A> 속성. <xref:System.Windows.Forms.KeyEventArgs> 매개 변수는 다음을 제공합니다.<br /><br /> <ul><li>기본 컨트롤의 키 수신을 방지하도록 설정될 수 있는 <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> 속성.</li><li>해당 키 입력에 대한 <xref:System.Windows.Forms.Control.KeyPress> 및 <xref:System.Windows.Forms.Control.KeyUp> 이벤트를 억제하는 사용될 수 있는 <xref:System.Windows.Forms.KeyEventArgs.SuppressKeyPress%2A> 속성.</li></ul></li></ul>|  
|<xref:System.Windows.Forms.Control.KeyPress>|이 이벤트는 키를 하나 이상 눌러서 문자가 표시될 때 발생합니다. 예를 들어 사용자가 SHIFT 키와 소문자 "a" 키를 누르면 대문자 "A" 문자가 표시됩니다.|<xref:System.Windows.Forms.Control.KeyPress>는 <xref:System.Windows.Forms.Control.KeyDown> 뒤에 발생합니다.<br /><br /> <ul><li><xref:System.Windows.Forms.Control.KeyPress>에 대한 처리기는 다음을 수신합니다.</li><li>눌린 키의 문자 코드가 포함된 <xref:System.Windows.Forms.KeyPressEventArgs> 매개 변수. 이 문자 코드는 모든 문자 키 및 한정자 키 조합에 대해 고유합니다.<br /><br />     예를 들어 "A" 키는 다음을 생성합니다.<br /><br /> <ul><li>문자 코드 65, SHIFT 키와 함께 누른 경우</li><li>또는 CAPS LOCK 키, 97, 키 자체를 누른 경우</li><li>및 1, CTRL 키와 함께 누른 경우.</li></ul></li></ul>|  
|<xref:System.Windows.Forms.Control.KeyUp>|이 이벤트는 사용자가 물리적 키를 놓을 때 발생합니다.|<xref:System.Windows.Forms.Control.KeyUp>에 대한 처리기는 다음을 수신합니다.<br /><br /> <ul><li><xref:System.Windows.Forms.KeyEventArgs> 매개 변수:<br /><br /> <ul><li>물리적 키보드 단추를 지정하는 <xref:System.Windows.Forms.KeyEventArgs.KeyCode%2A> 속성을 제공.</li><li><xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A> 속성(SHIFT, CTRL 또는 ALT).</li><li>키 코드 및 한정자를 결합하는 <xref:System.Globalization.SortKey.KeyData%2A> 속성.</li></ul></li></ul>|  
  
## <a name="see-also"></a>참고 항목  
 [Windows Forms 응용 프로그램의 키보드 입력](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)  
 [키보드 입력 작동 방식](../../../docs/framework/winforms/how-keyboard-input-works.md)  
 [Windows Forms 응용 프로그램의 마우스 입력](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)
