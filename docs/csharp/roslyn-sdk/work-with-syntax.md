---
title: ".NET Compiler Platform SDK 구문 모델 사용"
description: "이 개요에서는 구문 노드를 이해하고 조작하는 데 사용하는 형식에 대한 이해를 제공합니다."
author: billwagner
ms.author: wiwagn
ms.date: 10/15/2017
ms.topic: conceptual
ms.prod: .net
ms.devlang: devlang-csharp
ms.custom: mvc
ms.openlocfilehash: fa3b7af871380d4f18ebe7ef4f5bc5963cc247c4
ms.sourcegitcommit: 2142a4732bb4ff519b9817db4c24a237b9810d4b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="work-with-syntax"></a><span data-ttu-id="0a7f9-103">구문 작업</span><span class="sxs-lookup"><span data-stu-id="0a7f9-103">Work with syntax</span></span>

<span data-ttu-id="0a7f9-104">**구문 트리**는 컴파일러 API에서 노출하는 기본 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-104">The **syntax tree** is a fundamental data structure exposed by the compiler APIs.</span></span> <span data-ttu-id="0a7f9-105">이러한 트리는 소스 코드의 어휘 및 구문 구조를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-105">These trees represent the lexical and syntactic structure of source code.</span></span> <span data-ttu-id="0a7f9-106">두 가지 중요한 용도를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-106">They serve two important purposes:</span></span>

1. <span data-ttu-id="0a7f9-107">사용자의 프로젝트에서 소스 코드의 구문 구조를 보고 처리하도록 IDE, 추가 기능, 코드 분석 도구 및 리팩터링과 같은 도구 허용</span><span class="sxs-lookup"><span data-stu-id="0a7f9-107">To allow tools - such as an IDE, add-ins, code analysis tools, and refactorings - to see and process the syntactic structure of source code in a user’s project.</span></span>
2. <span data-ttu-id="0a7f9-108">직접 텍스트 편집을 사용하지 않고 자연스러운 방식으로 소스 코드를 만들고, 수정하고, 다시 정렬하도록 리팩터링 및 IDE와 같은 도구 활성화</span><span class="sxs-lookup"><span data-stu-id="0a7f9-108">To enable tools - such as refactorings and an IDE - to create, modify, and rearrange source code in a natural manner without having use direct text edits.</span></span> <span data-ttu-id="0a7f9-109">트리를 만들고 조작하여 도구는 쉽게 소스 코드를 만들고 다시 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-109">By creating and manipulating trees, tools can easily create and rearrange source code.</span></span>

## <a name="syntax-trees"></a><span data-ttu-id="0a7f9-110">구문 트리</span><span class="sxs-lookup"><span data-stu-id="0a7f9-110">Syntax trees</span></span>

<span data-ttu-id="0a7f9-111">구문 트리는 컴파일, 코드 분석, 바인딩, 리팩터링, IDE 기능 및 코드 생성에 사용되는 기본 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-111">Syntax trees are the primary structure used for compilation, code analysis, binding, refactoring, IDE features, and code generation.</span></span> <span data-ttu-id="0a7f9-112">소스 코드의 어떠한 부분도 먼저 식별되고 잘 알려진 많은 구조적 언어 요소 중 하나로 분류되지 않고 인식되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-112">No part of the source code is understood without it first being identified and categorized into one of many well-known structural language elements.</span></span> 

<span data-ttu-id="0a7f9-113">구문 트리에는 세 가지 주요 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-113">Syntax trees have three key attributes.</span></span> <span data-ttu-id="0a7f9-114">첫 번째 특성은 구문 트리가 최고의 충실도로 모든 원본 정보를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-114">The first attribute is that syntax trees hold all the source information in full fidelity.</span></span> <span data-ttu-id="0a7f9-115">즉 구문 트리가 공백, 설명 및 전처리기 지시문을 포함하여 원본 텍스트에서 발견되는 모든 정보, 모든 문법 구문, 모든 어휘 토큰 및 사이의 모든 다른 것을 포함하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-115">This means that the syntax tree contains every piece of information found in the source text, every grammatical construct, every lexical token, and everything else in between, including whitespace, comments, and preprocessor directives.</span></span> <span data-ttu-id="0a7f9-116">예를 들어 원본에서 언급된 각 리터럴은 입력된 대로 정확하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-116">For example, each literal mentioned in the source is represented exactly as it was typed.</span></span> <span data-ttu-id="0a7f9-117">구문 트리는 프로그램이 불완전하거나 형식이 잘못된 경우 구문 트리에 건너뛰거나 누락된 토큰을 표시하여 소스 코드의 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-117">The syntax trees also represent errors in source code when the program is incomplete or malformed by representing skipped or missing tokens in the syntax tree.</span></span>  

<span data-ttu-id="0a7f9-118">이는 두 번째 구문 트리의 특성을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-118">This enables the second attribute of syntax trees.</span></span> <span data-ttu-id="0a7f9-119">파서에서 가져온 구문 트리는 구문 분석된 정확한 텍스트를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-119">A syntax tree obtained from the parser can produce the exact text it was parsed from.</span></span> <span data-ttu-id="0a7f9-120">구문 노드에서 해당 노드를 기반으로 하는 하위 트리의 텍스트 표현을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-120">From any syntax node, it is possible to get the text representation of the sub-tree rooted at that node.</span></span> <span data-ttu-id="0a7f9-121">구문 트리가 원본 텍스트를 생성하고 편집하는 방법으로 사용될 수 있다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-121">This means that syntax trees can be used as a way to construct and edit source text.</span></span> <span data-ttu-id="0a7f9-122">암시적으로 해당 텍스트를 만든 트리를 만들고, 변경 내용에서 새 트리를 기존 트리로 만들어 구문 트리를 편집하여 텍스트를 효과적으로 편집했습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-122">By creating a tree you have by implication created the equivalent text, and by editing a syntax tree, making a new tree out of changes to an existing tree, you have effectively edited the text.</span></span> 

<span data-ttu-id="0a7f9-123">구문 트리의 세 번째 특성은 변경할 수 없으며 스레드로부터 안전하다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-123">The third attribute of syntax trees is that they are immutable and thread-safe.</span></span>  <span data-ttu-id="0a7f9-124">즉, 트리를 얻으면 이는 코드의 현재 상태의 스냅숏이며 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-124">This means that after a tree is obtained, it is a snapshot of the current state of the code, and never changes.</span></span> <span data-ttu-id="0a7f9-125">따라서 여러 사용자는 잠금 또는 중복 없이 서로 다른 스레드에서 동시에 동일한 구문 트리와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-125">This allows multiple users to interact with the same syntax tree at the same time in different threads without locking or duplication.</span></span> <span data-ttu-id="0a7f9-126">트리를 변경할 수 없으며 트리에 직접 수정을 만들 수 없으므로 팩터리 메서드는 트리의 추가 스냅숏을 만들어 구문 트리를 만들고 수정하도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-126">Because the trees are immutable and no modifications can be made directly to a tree, factory methods help create and modify syntax trees by creating additional snapshots of the tree.</span></span> <span data-ttu-id="0a7f9-127">트리는 기본 노드를 다시 사용하는 방법에서 효율적이므로 빠르게 작은 추가 메모리로 새 버전을 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-127">The trees are efficient in the way they reuse underlying nodes, so a new version can be rebuilt fast and with little extra memory.</span></span>

<span data-ttu-id="0a7f9-128">구문 트리는 비터미널 구조 요소가 다른 요소를 부모로 삼는 문자 그대로 트리 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-128">A syntax tree is literally a tree data structure, where non-terminal structural elements parent other elements.</span></span> <span data-ttu-id="0a7f9-129">각 구문 트리는 노드, 토큰 및 기타 정보로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-129">Each syntax tree is made up of nodes, tokens, and trivia.</span></span>  

## <a name="syntax-nodes"></a><span data-ttu-id="0a7f9-130">구문 노드</span><span class="sxs-lookup"><span data-stu-id="0a7f9-130">Syntax nodes</span></span>

<span data-ttu-id="0a7f9-131">구문 노드는 구문 트리의 기본 요소 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-131">Syntax nodes are one of the primary elements of syntax trees.</span></span> <span data-ttu-id="0a7f9-132">이러한 노드는 선언, 명령문, 절 및 식과 같은 구문 구조를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-132">These nodes represent syntactic constructs such as declarations, statements, clauses, and expressions.</span></span> <span data-ttu-id="0a7f9-133">구문 노드의 각 범주는 <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType>에서 파생되는 별도 클래스로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-133">Each category of syntax nodes is represented by a separate class derived from <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType>.</span></span> <span data-ttu-id="0a7f9-134">노드 클래스의 집합은 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-134">The set of node classes is not extensible.</span></span> 

<span data-ttu-id="0a7f9-135">모든 구문 노드는 구문 트리에서 비터미널 노드입니다. 즉, 항상 다른 노드 및 토큰을 자식으로 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-135">All syntax nodes are non-terminal nodes in the syntax tree, which means they always have other nodes and tokens as children.</span></span> <span data-ttu-id="0a7f9-136">다른 노드의 자식으로 각 노드는 <xref:Microsoft.CodeAnalysis.SyntaxNode.Parent?displayProperty=nameWithType> 속성을 통해 액세스할 수 있는 부모 노드를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-136">As a child of another node, each node has a parent node that can be accessed through the <xref:Microsoft.CodeAnalysis.SyntaxNode.Parent?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="0a7f9-137">노드 및 트리를 변경할 수 없기 때문에 부모 노드는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-137">Because nodes and trees are immutable, the parent of a node never changes.</span></span> <span data-ttu-id="0a7f9-138">트리의 루트는 null 부모를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-138">The root of the tree has a null parent.</span></span>  

<span data-ttu-id="0a7f9-139">각 노드에는 원본 텍스트에서의 위치에 따라 순서대로 자식 노드의 목록을 반환하는 <xref:Microsoft.CodeAnalysis.SyntaxNode.ChildNodes?displayProperty=nameWithType> 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-139">Each node has a <xref:Microsoft.CodeAnalysis.SyntaxNode.ChildNodes?displayProperty=nameWithType> method, which returns a list of child nodes in sequential order based on their position in the source text.</span></span> <span data-ttu-id="0a7f9-140">이 목록은 토큰을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-140">This list does not contain tokens.</span></span> <span data-ttu-id="0a7f9-141">각 노드에는 해당 노드를 기반으로 하는 하위 트리에 존재하는 모든 노드, 토큰 또는 기타 정보의 목록을 나타내는 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A>, <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTokens%2A> 또는 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTrivia%2A> 등의 하위 목록을 검사하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-141">Each node also has methods to examine Descendants, such as <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A>, <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTokens%2A>, or <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantTrivia%2A> - that represent a list of all the nodes, tokens, or trivia, that exist in the sub-tree rooted by that node.</span></span>  

<span data-ttu-id="0a7f9-142">또한 각 구문 노드 하위 클래스는 강력한 형식의 속성을 통해 동일한 모든 자식을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-142">In addition, each syntax node subclass exposes all the same children through strongly typed properties.</span></span> <span data-ttu-id="0a7f9-143">예를 들어 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> 노드 클래스에는 이진 연산자, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> 및 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>에 해당하는 3개의 추가 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-143">For example, a <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> node class has three additional properties specific to binary operators: <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken>, and <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>.</span></span> <span data-ttu-id="0a7f9-144"><xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left> 및 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>의 형식은 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ExpressionSyntax>이며 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken>의 형식은 <xref:Microsoft.CodeAnalysis.SyntaxToken>입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-144">The type of <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left> and <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right> is <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ExpressionSyntax>, and the type of <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> is <xref:Microsoft.CodeAnalysis.SyntaxToken>.</span></span>

<span data-ttu-id="0a7f9-145">일부 구문 노드에는 선택적 자식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-145">Some syntax nodes have optional children.</span></span> <span data-ttu-id="0a7f9-146">예를 들어 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.IfStatementSyntax>에는 선택적 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ElseClauseSyntax>가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-146">For example, an <xref:Microsoft.CodeAnalysis.CSharp.Syntax.IfStatementSyntax> has an optional <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ElseClauseSyntax>.</span></span> <span data-ttu-id="0a7f9-147">자식이 없는 경우 속성은 null을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-147">If the child is not present, the property returns null.</span></span> 

## <a name="syntax-tokens"></a><span data-ttu-id="0a7f9-148">구문 토큰</span><span class="sxs-lookup"><span data-stu-id="0a7f9-148">Syntax tokens</span></span>

<span data-ttu-id="0a7f9-149">구문 토큰은 코드의 가장 작은 구문 조각을 나타내는 언어 문법의 터미널입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-149">Syntax tokens are the terminals of the language grammar, representing the smallest syntactic fragments of the code.</span></span> <span data-ttu-id="0a7f9-150">다른 노드 또는 토큰의 부모가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-150">They are never parents of other nodes or tokens.</span></span> <span data-ttu-id="0a7f9-151">구문 토큰은 키워드, 식별자, 리터럴 및 문장 부호로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-151">Syntax tokens consist of keywords, identifiers, literals, and punctuation.</span></span> 

<span data-ttu-id="0a7f9-152">효율성 향상을 위해 <xref:Microsoft.CodeAnalysis.SyntaxToken> 형식은 CLR 값 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-152">For efficiency purposes, the <xref:Microsoft.CodeAnalysis.SyntaxToken> type is a CLR value type.</span></span> <span data-ttu-id="0a7f9-153">따라서 구문 노드와 달리 표시되는 토큰의 종류에 따라 의미가 있는 속성을 조합하여 모든 종류의 토큰에 대해 하나의 구문만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-153">Therefore, unlike syntax nodes, there is only one structure for all kinds of tokens with a mix of properties that have meaning depending on the kind of token that is being represented.</span></span>

<span data-ttu-id="0a7f9-154">예를 들어 정수 리터럴 토큰은 숫자 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-154">For example, an integer literal token represents a numeric value.</span></span> <span data-ttu-id="0a7f9-155">토큰이 포괄하는 원시 원본 텍스트 이외에 리터럴 토큰에는 디코딩된 정확한 정수 값을 알려 주는 <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-155">In addition to the raw source text the token spans, the literal token has a <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> property that tells you the exact decoded integer value.</span></span> <span data-ttu-id="0a7f9-156">많은 기본 형식 중 하나일 수 있으므로 이 속성은 <xref:System.Object>로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-156">This property is typed as <xref:System.Object> because it may be one of many primitive types.</span></span>

<span data-ttu-id="0a7f9-157"><xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 속성은 <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> 속성과 동일한 정보를 알려 주지만 이 속성은 항상 <xref:System.String>으로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-157">The <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> property tells you the same information as the <xref:Microsoft.CodeAnalysis.SyntaxToken.Value> property; however this property is always typed as <xref:System.String>.</span></span> <span data-ttu-id="0a7f9-158">C# 원본 텍스트에서 식별자는 유니코드 이스케이프 문자를 포함할 수 있지만 이스케이프 시퀀스 자체의 구문은 식별자 이름의 일부로 간주되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-158">An identifier in C# source text may include Unicode escape characters, yet the syntax of the escape sequence itself is not considered part of the identifier name.</span></span> <span data-ttu-id="0a7f9-159">따라서 토큰에 포함되는 원시 텍스트는 이스케이프 시퀀스를 포함하지만 <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 속성은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-159">So although the raw text spanned by the token does include the escape sequence, the <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> property does not.</span></span> <span data-ttu-id="0a7f9-160">대신 이스케이프로 식별되는 유니코드 문자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-160">Instead, it includes the Unicode characters identified by the escape.</span></span> <span data-ttu-id="0a7f9-161">예를 들어 원본 텍스트가 `\u03C0`으로 작성된 식별자를 포함하는 경우 이 토큰에 대한 <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> 속성은 `π`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-161">For example, if the source text contains an identifier written as `\u03C0`, then the <xref:Microsoft.CodeAnalysis.SyntaxToken.ValueText> property for this token will return `π`.</span></span>

## <a name="syntax-trivia"></a><span data-ttu-id="0a7f9-162">구문 기타 정보</span><span class="sxs-lookup"><span data-stu-id="0a7f9-162">Syntax trivia</span></span>

<span data-ttu-id="0a7f9-163">구문 기타 정보는 공백, 설명 및 전처리기 지시문과 같은 코드의 일반적인 이해에 크게 중요하지 않은 원본 텍스트의 일부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-163">Syntax trivia represent the parts of the source text that are largely insignificant for normal understanding of the code, such as whitespace, comments, and preprocessor directives.</span></span> <span data-ttu-id="0a7f9-164">구문 토큰과 같이 기타 정보는 값 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-164">Like syntax tokens, trivia are value types.</span></span> <span data-ttu-id="0a7f9-165">단일 <xref:Microsoft.CodeAnalysis.SyntaxTrivia?displayProperty=nameWithType> 형식은 모든 종류의 기타 정보를 설명하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-165">The single <xref:Microsoft.CodeAnalysis.SyntaxTrivia?displayProperty=nameWithType> type is used to describe all kinds of trivia.</span></span>

<span data-ttu-id="0a7f9-166">기타 정보는 일반 언어 구문의 일부가 아니며 두 토큰 사이의 아무 곳에나 나타날 수 있으므로 노드의 자식으로 구문 트리에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-166">Because trivia are not part of the normal language syntax and can appear anywhere between any two tokens, they are not included in the syntax tree as a child of a node.</span></span> <span data-ttu-id="0a7f9-167">리팩터링과 같은 기능을 구현하는 경우 및 원본 텍스트로 최고의 충실도를 유지하는 데 중요하므로 구문 트리의 일부로 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-167">Yet, because they are important when implementing a feature like refactoring and to maintain full fidelity with the source text, they do exist as part of the syntax tree.</span></span>

<span data-ttu-id="0a7f9-168">토큰의 <xref:Microsoft.CodeAnalysis.SyntaxToken.LeadingTrivia?displayProperty=nameWithType> 또는 <xref:Microsoft.CodeAnalysis.SyntaxToken.TrailingTrivia?displayProperty=nameWithType> 컬렉션을 검사하여 기타 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-168">You can access trivia by inspecting a token’s <xref:Microsoft.CodeAnalysis.SyntaxToken.LeadingTrivia?displayProperty=nameWithType> or <xref:Microsoft.CodeAnalysis.SyntaxToken.TrailingTrivia?displayProperty=nameWithType> collections.</span></span> <span data-ttu-id="0a7f9-169">원본 텍스트를 구문 분석할 때 기타 정보의 시퀀스는 토큰과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-169">When source text is parsed, sequences of trivia are associated with tokens.</span></span> <span data-ttu-id="0a7f9-170">일반적으로 토큰은 다음 토큰까지 동일한 줄의 다음에 모든 기타 정보를 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-170">In general, a token owns any trivia after it on the same line up to the next token.</span></span> <span data-ttu-id="0a7f9-171">해당 줄 다음의 모든 기타 정보는 다음 토큰으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-171">Any trivia after that line is associated with the following token.</span></span> <span data-ttu-id="0a7f9-172">원본 파일의 첫 번째 토큰은 모든 초기 기타 정보를 가져오고 파일에 있는 기타 정보의 마지막 시퀀스는 파일 끝 토큰으로 고정됩니다. 그렇지 않으면 0의 너비를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-172">The first token in the source file gets all the initial trivia, and the last sequence of trivia in the file is tacked onto the end-of-file token, which otherwise has zero width.</span></span>

<span data-ttu-id="0a7f9-173">구문 노드 및 토큰과 달리 구문 기타 정보는 부모가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-173">Unlike syntax nodes and tokens, syntax trivia do not have parents.</span></span> <span data-ttu-id="0a7f9-174">아직 트리의 일부이며 각각은 단일 토큰에 연결되어 있으므로 <xref:Microsoft.CodeAnalysis.SyntaxTrivia.Token?displayProperty=nameWithType> 속성을 사용하여 연결된 토큰에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-174">Yet, because they are part of the tree and each is associated with a single token, you may access the token it is associated with using the <xref:Microsoft.CodeAnalysis.SyntaxTrivia.Token?displayProperty=nameWithType> property.</span></span>

## <a name="spans"></a><span data-ttu-id="0a7f9-175">범위</span><span class="sxs-lookup"><span data-stu-id="0a7f9-175">Spans</span></span>

<span data-ttu-id="0a7f9-176">각 노드, 토큰 또는 기타 정보는 원본 텍스트 내의 해당 위치와 구성된 문자 수를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-176">Each node, token, or trivia knows its position within the source text and the number of characters it consists of.</span></span> <span data-ttu-id="0a7f9-177">텍스트 위치는 0부터 시작하는 `char` 인덱스인 32비트 정수로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-177">A text position is represented as a 32-bit integer, which is a zero-based `char` index.</span></span> <span data-ttu-id="0a7f9-178"><xref:Microsoft.CodeAnalysis.Text.TextSpan> 개체는 시작 위치 및 문자 수이며 정수로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-178">A <xref:Microsoft.CodeAnalysis.Text.TextSpan> object is the beginning position and a count of characters, both represented as integers.</span></span> <span data-ttu-id="0a7f9-179"><xref:Microsoft.CodeAnalysis.Text.TextSpan>의 길이가 0인 경우 두 문자 사이의 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-179">If <xref:Microsoft.CodeAnalysis.Text.TextSpan> has a zero length, it refers to a location between two characters.</span></span>

<span data-ttu-id="0a7f9-180">각 노드에는 두 개의 <xref:Microsoft.CodeAnalysis.Text.TextSpan> 속성 <xref:Microsoft.CodeAnalysis.SyntaxNode.Span*> 및 <xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan*>이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-180">Each node has two <xref:Microsoft.CodeAnalysis.Text.TextSpan> properties: <xref:Microsoft.CodeAnalysis.SyntaxNode.Span*> and <xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan*>.</span></span> 

<span data-ttu-id="0a7f9-181"><xref:Microsoft.CodeAnalysis.SyntaxNode.Span\*> 속성은 노드의 하위 트리에 있는 첫 번째 토큰의 시작부터 마지막 토큰의 끝에 이르는 텍스트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-181">The <xref:Microsoft.CodeAnalysis.SyntaxNode.Span\*> property is the text span from the start of the first token in the node’s sub-tree to the end of the last token.</span></span> <span data-ttu-id="0a7f9-182">이 범위는 모든 선행 또는 후행 기타 정보를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-182">This span does not include any leading or trailing trivia.</span></span>

<span data-ttu-id="0a7f9-183"><xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan\*> 속성은 노드의 일반 범위와 모든 선행 또는 후행 기타 정보의 범위를 포함하는 텍스트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-183">The <xref:Microsoft.CodeAnalysis.SyntaxNode.FullSpan\*> property is the text span that includes the node’s normal span, plus the span of any leading or trailing trivia.</span></span>

<span data-ttu-id="0a7f9-184">예:</span><span class="sxs-lookup"><span data-stu-id="0a7f9-184">For example:</span></span> 

``` csharp
      if (x > 3)
      {
||        // this is bad
          |throw new Exception("Not right.");|  // better exception?||
      }
```

<span data-ttu-id="0a7f9-185">블록 내의 명령문 노드에는 단일 세로 막대(|)로 표시되는 범위가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-185">The statement node inside the block has a span indicated by the single vertical bars (|).</span></span> <span data-ttu-id="0a7f9-186">여기에는 `throw new Exception("Not right.");` 문자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-186">It includes the characters `throw new Exception("Not right.");`.</span></span> <span data-ttu-id="0a7f9-187">전체 범위는 이중 세로 막대(||)로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-187">The full span is indicated by the double vertical bars (||).</span></span> <span data-ttu-id="0a7f9-188">여기에는 범위와 동일한 문자 및 선행 및 후행 기타 정보와 연결된 문자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-188">It includes the same characters as the span and the characters associated with the leading and trailing trivia.</span></span>

## <a name="kinds"></a><span data-ttu-id="0a7f9-189">종류</span><span class="sxs-lookup"><span data-stu-id="0a7f9-189">Kinds</span></span>

<span data-ttu-id="0a7f9-190">각 노드, 토큰 또는 기타 정보에는 표시되는 정확한 구문 요소를 식별하는 <xref:System.Int32?displayProperty=fullName> 형식의 <xref:Microsoft.CodeAnalysis.SyntaxNode.RawKind?displayProperty=nameWithType> 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-190">Each node, token, or trivia has a <xref:Microsoft.CodeAnalysis.SyntaxNode.RawKind?displayProperty=nameWithType> property, of type <xref:System.Int32?displayProperty=fullName>, that identifies the exact syntax element represented.</span></span> <span data-ttu-id="0a7f9-191">이 값은 언어별 열거형으로 캐스팅될 수 있습니다. 각 언어, C# 또는 VB에는 문법에서 가능한 모든 노드, 토큰 및 기타 정보 요소를 나열하는 단일 `SyntaxKind` 열거형(각각 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind?displayProperty=fullName> 및 <xref:Microsoft.CodeAnalysis.VisualBasic.SyntaxKind?displayProperty=fullName>)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-191">This value can be cast to a language-specific enumeration; each language, C# or VB, has a single `SyntaxKind` enumeration  (<xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind?displayProperty=fullName> and <xref:Microsoft.CodeAnalysis.VisualBasic.SyntaxKind?displayProperty=fullName>, respectively) that lists all the possible nodes, tokens, and trivia elements in the grammar.</span></span> <span data-ttu-id="0a7f9-192"><xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind*?displayProperty=nameWithType> 또는 <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicExtensions.Kind*?displayProperty=nameWithType> 확장 메서드에 액세스하여 이 변환을 자동으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-192">This conversion can be done automatically by accessing the <xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind*?displayProperty=nameWithType> or <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicExtensions.Kind*?displayProperty=nameWithType> extension methods.</span></span>

<span data-ttu-id="0a7f9-193"><xref:Microsoft.CodeAnalysis.SyntaxToken.RawKind> 속성은 동일한 노드 클래스를 공유하는 구문 노드 형식의 쉬운 명확성을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-193">The <xref:Microsoft.CodeAnalysis.SyntaxToken.RawKind> property allows for easy disambiguation of syntax node types that share the same node class.</span></span> <span data-ttu-id="0a7f9-194">토큰 및 기타 정보의 경우 이 속성은 요소의 한 형식을 다른 형식에서 구분하는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-194">For tokens and trivia, this property is the only way to distinguish one type of element from another.</span></span> 

<span data-ttu-id="0a7f9-195">예를 들어 단일 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> 클래스에는 자식으로 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken> 및 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right>가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-195">For example, a single <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax> class has <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Left>, <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.OperatorToken>, and <xref:Microsoft.CodeAnalysis.CSharp.Syntax.BinaryExpressionSyntax.Right> as children.</span></span> <span data-ttu-id="0a7f9-196"><xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind\*> 속성은 구문 노드의 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.AddExpression>, <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SubtractExpression> 또는 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.MultiplyExpression> 종류인지를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-196">The <xref:Microsoft.CodeAnalysis.CSharp.CSharpExtensions.Kind\*> property distinguishes whether it is an <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.AddExpression>, <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SubtractExpression>, or <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.MultiplyExpression> kind of syntax node.</span></span>

## <a name="errors"></a><span data-ttu-id="0a7f9-197">오류</span><span class="sxs-lookup"><span data-stu-id="0a7f9-197">Errors</span></span>

<span data-ttu-id="0a7f9-198">원본 텍스트에 구문 오류가 있는 경우에도 원본에 대해 왕복 가능한 전체 구문 트리가 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-198">Even when the source text contains syntax errors, a full syntax tree that is round-trippable to the source is exposed.</span></span> <span data-ttu-id="0a7f9-199">파서가 언어의 정의된 구문에 맞지 않는 코드를 발견하면 두 가지 기술 중 하나를 사용하여 구문 트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-199">When the parser encounters code that does not conform to the defined syntax of the language, it uses one of two techniques to create a syntax tree.</span></span>

<span data-ttu-id="0a7f9-200">먼저 파서에 특정 종류의 토큰이 필요하지만 찾을 수 없는 경우 토큰이 필요한 위치의 구문 트리로 누락된 토큰을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-200">First, if the parser expects a particular kind of token but does not find it, it may insert a missing token into the syntax tree in the location that the token was expected.</span></span> <span data-ttu-id="0a7f9-201">누락된 토큰은 필요한 실제 토큰을 나타내지만 빈 범위를 가지며 해당 <xref:Microsoft.CodeAnalysis.SyntaxNode.IsMissing?displayProperty=nameWithType> 속성은 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-201">A missing token represents the actual token that was expected, but it has an empty span, and its <xref:Microsoft.CodeAnalysis.SyntaxNode.IsMissing?displayProperty=nameWithType> property returns `true`.</span></span>

<span data-ttu-id="0a7f9-202">둘째로 파서는 구문 분석을 계속할 수 있는 토큰을 찾을 때까지 토큰을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-202">Second, the parser may skip tokens until it finds one where it can continue parsing.</span></span> <span data-ttu-id="0a7f9-203">이 경우 건너뛴 토큰은 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SkippedTokensTrivia> 종류와 함께 기타 정보 노드로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a7f9-203">In this case, the skipped tokens are attached as a trivia node with the kind <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.SkippedTokensTrivia>.</span></span>