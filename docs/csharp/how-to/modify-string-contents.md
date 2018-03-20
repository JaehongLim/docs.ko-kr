---
title: "방법: 문자열 내용 수정 - C# 가이드"
ms.date: 02/26/2018
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- strings [C#], modifying
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 830ca207c4cd5bd24dbb667328465cafb2509409
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="how-to-modify-string-contents-in-c"></a><span data-ttu-id="4d7ad-102">방법: C#에서 문자열 내용 수정</span><span class="sxs-lookup"><span data-stu-id="4d7ad-102">How to: Modify string contents in C#</span></span> #

<span data-ttu-id="4d7ad-103">이 문서에서는 기존 `string`을 수정하여 `string`을 생성하는 다양한 기술을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-103">This article demonstrates several techniques to produce a `string` by modifying an existing `string`.</span></span> <span data-ttu-id="4d7ad-104">설명된 모든 기술은 새 `string` 개체로 수정의 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-104">All the techniques demonstrated return the result of the modifications as a new `string` object.</span></span> <span data-ttu-id="4d7ad-105">이를 명확하게 보여 주기 위해 모든 예제는 새 변수에 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-105">To clearly demonstrate this, the examples all store the result in a new variable.</span></span> <span data-ttu-id="4d7ad-106">그런 다음, 기존 `string` 및 각 예제를 실행할 때 수정의 결과인 `string`을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-106">You can then examine both the original `string` and the `string` resulting from the modification when you run each example.</span></span>

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

<span data-ttu-id="4d7ad-107">이 문서에서 설명되는 여러 가지 기술이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-107">There are several techniques demonstrated in this article.</span></span> <span data-ttu-id="4d7ad-108">기존 텍스트를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-108">You can replace existing text.</span></span> <span data-ttu-id="4d7ad-109">패턴을 검색하고 다른 텍스트와 일치하는 텍스트를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-109">You can search for patterns and replace matching text with other text.</span></span> <span data-ttu-id="4d7ad-110">일련의 문자로 문자열을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-110">You can treat a string as a sequence of characters.</span></span> <span data-ttu-id="4d7ad-111">공백을 제거하는 편리한 메서드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-111">You can also use convenience methods that remove white space.</span></span> <span data-ttu-id="4d7ad-112">시나리오에 가장 일치하는 기술을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-112">You should choose the techniques that most closely match your scenario.</span></span>

## <a name="replace-text"></a><span data-ttu-id="4d7ad-113">텍스트 바꾸기</span><span class="sxs-lookup"><span data-stu-id="4d7ad-113">Replace text</span></span>

<span data-ttu-id="4d7ad-114">다음 코드는 기존 텍스트를 대체로 바꿔 새 문자열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-114">The following code creates a new string by replacing existing text with a substitute.</span></span>

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#1)]

<span data-ttu-id="4d7ad-115">위의 코드는 문자열의 이러한 *변경할 수 없는* 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-115">The preceding code demonstrates this *immutable* property of strings.</span></span> <span data-ttu-id="4d7ad-116">앞의 예제에서 원래 문자열, `source`가 수정되지 않는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-116">You can see in the preceding example that the original string, `source`, is not modified.</span></span> <span data-ttu-id="4d7ad-117"><xref:System.String.Replace%2A?displayProperty=nameWithType> 메서드는 수정 내용을 포함하는 새 `string`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-117">The <xref:System.String.Replace%2A?displayProperty=nameWithType> method creates a new `string` containing the modifications.</span></span>

<span data-ttu-id="4d7ad-118"><xref:System.String.Replace%2A> 메서드는 문자열 또는 단일 문자를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-118">The <xref:System.String.Replace%2A> method can replace either strings or single characters.</span></span> <span data-ttu-id="4d7ad-119">두 경우 모두에서 검색된 텍스트의 모든 항목이 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-119">In both cases, every occurrence of the sought text is replaced.</span></span>  <span data-ttu-id="4d7ad-120">다음 예제에서는 모든 ' ' 문자를 '\_'로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-120">The following example replaces all ' ' characters with '\_':</span></span>

[!code-csharp-interactive[replace characters](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#2)]

<span data-ttu-id="4d7ad-121">원본 문자열은 변경되지 않으며, 새 문자열은 교체와 함께 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-121">The source string is unchanged, and a new string is returned with the replacement.</span></span>

## <a name="trim-white-space"></a><span data-ttu-id="4d7ad-122">공백 제거</span><span class="sxs-lookup"><span data-stu-id="4d7ad-122">Trim white space</span></span>

<span data-ttu-id="4d7ad-123"><xref:System.String.Trim%2A?displayProperty=nameWithType>, <xref:System.String.TrimStart%2A?displayProperty=nameWithType> 및 <xref:System.String.TrimEnd%2A?displayProperty=nameWithType> 메서드를 사용하여 선행 또는 후행 공백을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-123">You can use the <xref:System.String.Trim%2A?displayProperty=nameWithType>, <xref:System.String.TrimStart%2A?displayProperty=nameWithType>, and <xref:System.String.TrimEnd%2A?displayProperty=nameWithType> methods to remove any leading or trailing white space.</span></span>  <span data-ttu-id="4d7ad-124">다음 코드에서는 각 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-124">The following code shows an example of each.</span></span> <span data-ttu-id="4d7ad-125">원본 문자열 변경되지 않습니다. 이러한 메서드는 수정된 내용이 포함된 새 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-125">The source string does not change; these methods return a new string with the modified contents.</span></span>

[!code-csharp-interactive[trim white space](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#3)]

## <a name="remove-text"></a><span data-ttu-id="4d7ad-126">텍스트 제거</span><span class="sxs-lookup"><span data-stu-id="4d7ad-126">Remove text</span></span>

<span data-ttu-id="4d7ad-127"><xref:System.String.Remove%2A?displayProperty=nameWithType> 메서드를 사용하여 문자열에서 텍스트를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-127">You can remove text from a string using the <xref:System.String.Remove%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4d7ad-128">이 메서드는 특정 인덱스에서 시작하는 문자 수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-128">This method removes a number of characters starting at a specific index.</span></span> <span data-ttu-id="4d7ad-129">다음 예제에서는 <xref:System.String.Remove%2A>가 뒤에 오는 <xref:System.String.IndexOf%2A?displayProperty=nameWithType>을 사용하여 문자열에서 텍스트를 제거하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-129">The following example shows how to use <xref:System.String.IndexOf%2A?displayProperty=nameWithType> followed by <xref:System.String.Remove%2A> to remove text from a string:</span></span>

[!code-csharp-interactive[remove text](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#4)]

## <a name="replace-matching-patterns"></a><span data-ttu-id="4d7ad-130">일치 패턴 바꾸기</span><span class="sxs-lookup"><span data-stu-id="4d7ad-130">Replace matching patterns</span></span>

<span data-ttu-id="4d7ad-131">[정규식](../../standard/base-types/regular-expressions.md)을 사용하여 패턴에 의해 정의된 새 텍스트로 텍스트 일치 패턴을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-131">You can use [regular expressions](../../standard/base-types/regular-expressions.md) to replace text matching patterns with new text, possibly defined by a pattern.</span></span> <span data-ttu-id="4d7ad-132">다음 예제에서는 <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 클래스를 사용하여 원본 문자열의 패턴을 찾고 적절한 대/소문자로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-132">The following example uses the <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> class to find a pattern in a source string and replace it with proper capitalization.</span></span> <span data-ttu-id="4d7ad-133"><xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.Text.RegularExpressions.MatchEvaluator,System.Text.RegularExpressions.RegexOptions)?displayProperty=nameWithType> 메서드는 해당 인수 중 하나로 대체 논리를 제공하는 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-133">The <xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.Text.RegularExpressions.MatchEvaluator,System.Text.RegularExpressions.RegexOptions)?displayProperty=nameWithType> method takes a function that provides the logic of the replacement as one of its arguments.</span></span> <span data-ttu-id="4d7ad-134">이 예제에서 해당 함수, `LocalReplaceMatchCase`는 샘플 메서드 내에서 선언된 **로컬 함수**입니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-134">In this example, that function, `LocalReplaceMatchCase` is a **local function** declared inside the sample method.</span></span> <span data-ttu-id="4d7ad-135">`LocalReplaceMatchCase`는 <xref:System.Text.StringBuilder?displayProperty=nameWithType> 클래스를 사용하여 적절한 대/소문자로 대체 문자열을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-135">`LocalReplaceMatchCase` uses the <xref:System.Text.StringBuilder?displayProperty=nameWithType> class to build the replacement string with proper capitalization.</span></span>

<span data-ttu-id="4d7ad-136">정규식은 알려진 텍스트가 아닌 패턴을 따르는 텍스트를 검색하고 대체하는 데 가장 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-136">Regular expressions are most useful for searching and replacing text that follows a pattern, rather than known text.</span></span> <span data-ttu-id="4d7ad-137">자세한 내용은 [방법: 문자열 검색](search-strings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-137">See [How to: search strings](search-strings.md) for more details.</span></span> <span data-ttu-id="4d7ad-138">검색 패턴, "the\s"는 공백 문자가 뒤에 오는 문자 "the"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-138">The search pattern, "the\s" searches for the word "the" followed by a white-space character.</span></span> <span data-ttu-id="4d7ad-139">패턴의 해당 부분을 사용하면 원본 문자열의 "there"와 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-139">That part of the pattern ensures that it doesn't match "there" in the source string.</span></span> <span data-ttu-id="4d7ad-140">정규식 언어 요소에 대한 자세한 내용은 [정규식 언어 - 빠른 참조](../../standard/base-types/regular-expression-language-quick-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-140">For more information on regular expression language elements, see [Regular Expression Language - Quick Reference](../../standard/base-types/regular-expression-language-quick-reference.md).</span></span>

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#5)]

<span data-ttu-id="4d7ad-141"><xref:System.Text.StringBuilder.ToString%2A?displayProperty=nameWithType> 메서드는 <xref:System.Text.StringBuilder> 개체의 내용으로 변경할 수 없는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-141">The <xref:System.Text.StringBuilder.ToString%2A?displayProperty=nameWithType> method returns an immutable string with the contents in the <xref:System.Text.StringBuilder> object.</span></span>

## <a name="modifying-individual-characters"></a><span data-ttu-id="4d7ad-142">개별 문자 수정</span><span class="sxs-lookup"><span data-stu-id="4d7ad-142">Modifying individual characters</span></span>

<span data-ttu-id="4d7ad-143">문자열에서 문자 배열을 생성하고, 배열의 내용을 수정한 다음, 수정된 배열의 내용에서 새 문자열을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-143">You can produce a character array from a string, modify the contents of the array, and then create a new string from the modified contents of the array.</span></span>

<span data-ttu-id="4d7ad-144">다음 예제에서는 문자열에서 문자 집합을 대체하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-144">The following example shows how to replace a set of characters in a string.</span></span> <span data-ttu-id="4d7ad-145">먼저 <xref:System.String.ToCharArray?displayProperty=nameWithName> 메서드를 사용하여 문자의 배열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-145">First, it uses the <xref:System.String.ToCharArray?displayProperty=nameWithName> method to create an array of characters.</span></span> <span data-ttu-id="4d7ad-146"><xref:System.String.IndexOf%2A> 메서드를 사용하여 단어 "fox"의 시작 인덱스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-146">It uses the <xref:System.String.IndexOf%2A> method to find the starting index of the word "fox."</span></span> <span data-ttu-id="4d7ad-147">다음 세 개의 문자는 서로 다른 단어로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-147">The next three characters are replaced with a different word.</span></span> <span data-ttu-id="4d7ad-148">마지막으로 새 문자열은 업데이트된 문자 배열에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-148">Finally, a new string is constructed from the updated character array.</span></span>

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#6)]

## <a name="unsafe-modifications-to-string"></a><span data-ttu-id="4d7ad-149">문자열에 대한 안전하지 않은 수정</span><span class="sxs-lookup"><span data-stu-id="4d7ad-149">Unsafe modifications to string</span></span>

<span data-ttu-id="4d7ad-150">**unsafe** 코드를 사용하여 만들어진 후 문자열을 "적절히" 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-150">Using **unsafe** code, you can modify a string "in place" after it has been created.</span></span> <span data-ttu-id="4d7ad-151">안전하지 않은 코드는 코드에서 특정 유형의 버그를 최소화하도록 설계된 .NET의 많은 기능을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-151">Unsafe code bypasses many of the features of .NET designed to minimize certain types of bugs in code.</span></span> <span data-ttu-id="4d7ad-152">문자열 클래스는 **변경할 수 없는** 유형으로 디자인되었으므로 안전하지 않은 코드를 사용하여 문자열을 적절히 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-152">You need to use unsafe code to modify a string in place because the string class is designed as an **immutable** type.</span></span> <span data-ttu-id="4d7ad-153">만들어지면 해당 값은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-153">Once it has been created, its value does not change.</span></span> <span data-ttu-id="4d7ad-154">안전하지 않은 코드는 일반 `string` 메서드를 사용하지 않고 `string`에서 사용되는 메모리에 액세스하고 수정하여 이 속성을 회피합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-154">Unsafe code circumvents this property by accessing and modifying the memory used by a `string` without using normal `string` methods.</span></span>
<span data-ttu-id="4d7ad-155">다음 예제는 안전하지 않은 코드를 사용하여 문자열을 적절히 수정하려는 드문 경우를 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-155">The following example is provided for those rare situations where you want to modify a string in-place using unsafe code.</span></span> <span data-ttu-id="4d7ad-156">이 예제에서는 `fixed` 키워드를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-156">The example shows how to use the `fixed` keyword.</span></span> <span data-ttu-id="4d7ad-157">`fixed` 키워드는 코드가 안전하지 않은 포인터를 사용하여 메모리에 액세스하는 동안 GC(가비지 수집기)가 메모리에서 문자열 개체를 이동하는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-157">The `fixed` keyword prevents the garbage collector (GC) from moving the string object in memory while code accesses the memory using the unsafe pointer.</span></span> <span data-ttu-id="4d7ad-158">또한 문자열에 대한 안전하지 않은 작업의 가능한 부작용 중 하나를 보여 줍니다. 이 부작용은 C# 컴파일러가 문자열을 내부적으로 저장(intern)하는 방식에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-158">It also demonstrates one possible side effect of unsafe operations on strings that results from the way that the C# compiler stores (interns) strings internally.</span></span> <span data-ttu-id="4d7ad-159">일반적으로 이 방식은 반드시 필요한 경우에만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-159">In general, you shouldn't use this technique unless it is absolutely necessary.</span></span> <span data-ttu-id="4d7ad-160">[안전하지 않은](../language-reference/keywords/unsafe.md) 및 [수정 사항](../language-reference/keywords/fixed-statement.md)에 대해 문서에서 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-160">You can learn more in the articles on [unsafe](../language-reference/keywords/unsafe.md) and [fixed](../language-reference/keywords/fixed-statement.md).</span></span> <span data-ttu-id="4d7ad-161"><xref:System.String.Intern%2A>에 대한 API 참조는 문자열 인터닝에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-161">The API reference for <xref:System.String.Intern%2A> includes inforamtion on string interning.</span></span>

[!code-csharp-interactive[unsafe ways to create a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#7)]

<span data-ttu-id="4d7ad-162">[GitHub 리포지토리](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings)의 코드를 확인하여 이러한 샘플을 시험해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-162">You can try these samples by looking at the code in our [GitHub repository](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings).</span></span> <span data-ttu-id="4d7ad-163">또는 샘플을 [zip 파일로](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings.zip) 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d7ad-163">Or you can download the samples [as a zip file](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings.zip).</span></span>

## <a name="see-also"></a><span data-ttu-id="4d7ad-164">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4d7ad-164">See also</span></span>

[<span data-ttu-id="4d7ad-165">.NET Framework 정규식</span><span class="sxs-lookup"><span data-stu-id="4d7ad-165">.NET Framework Regular Expressions</span></span>](../../standard/base-types/regular-expressions.md)  
 [<span data-ttu-id="4d7ad-166">정규식 언어 - 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="4d7ad-166">Regular Expression Language - Quick Reference</span></span>](../../standard/base-types/regular-expression-language-quick-reference.md)  