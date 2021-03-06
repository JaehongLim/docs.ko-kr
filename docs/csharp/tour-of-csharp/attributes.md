---
title: "C# 특성 - C# 언어 둘러보기"
description: "C#에서 특성을 사용하는 선언적 프로그래밍에 대해 알아보기"
keywords: ".NET, c샵"
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 753bcfe2-7ddd-4487-9513-ba70937fc8e9
ms.openlocfilehash: 6878a408ef892ee47a03bfa04f736b9bf9671696
ms.sourcegitcommit: bbde43da655ae7bea1977f7af7345eb87bd7fd5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2017
---
# <a name="attributes"></a>특성

C# 프로그램의 형식, 멤버 및 기타 엔터티는 동작의 특정 측면을 제어하는 한정자를 지원합니다. 예를 들어 메서드의 액세스 가능성은 `public`, `protected`, `internal` 및 `private` 한정자를 사용하여 제어됩니다. C#은 선언적 정보의 사용자 정의 형식을 프로그램 엔터티에 연결하고 런타임에 검색할 수 있도록 이러한 기능을 일반화합니다. 프로그램은 ***특성***을 정의하고 사용하여 이러한 추가적인 선언적 정보를 지정합니다.

다음 예제에서는 관련 설명서에 대한 링크를 제공하기 위해 프로그램 엔터티에 배치될 수 있는 `HelpAttribute` 특성을 선언합니다.

[!code-csharp[AttributeDefined](../../../samples/snippets/csharp/tour/attributes/Program.cs#L3-L20)]

모든 특성 클래스는 표준 라이브러리에서 제공하는 <xref:System.Attribute> 기본 클래스에서 파생됩니다. 연결된 선언 바로 앞에 대괄호로 묶은 특성 이름을 인수와 함께 적용할 수 있습니다. 특성 이름이 `Attribute`로 끝나는 경우 특성이 참조될 때 이름의 해당 부분을 생략해도 됩니다. 예를 들어 `HelpAttribute` 특성을 다음과 같이 사용할 수 있습니다.

[!code-csharp[AttributeApplied](../../../samples/snippets/csharp/tour/attributes/Program.cs#L22-L28)]

이 예제에서는 `HelpAttribute`를 `Widget` 클래스에 연결합니다. 그런 후 다른 `HelpAttribute`를 클래스의 `Display` 메서드에 추가합니다. 특성 클래스의 공용 생성자는 프로그램 엔터티에 특성을 추가할 때 제공해야 하는 정보를 제어합니다. 특성 클래스의 공용 읽기/쓰기 속성을 참조하여 추가 정보를 제공할 수 있습니다(예: 앞에 나온 `Topic` 속성 참조).

리플렉션을 통해 특정 특성이 요청되면 특성 클래스에 대한 생성자가 프로그램 소스에 제공된 정보와 함께 호출되고 결과 특성 인스턴스가 반환됩니다. 속성을 통해 추가 정보를 제공한 경우 해당 속성은 특성 인스턴스가 반환되기 전에 지정된 값으로 설정됩니다.

>[!div class="step-by-step"]
[이전](delegates.md)
