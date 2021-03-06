---
title: "방법: MaskedTextBox 컨트롤에 데이터 바인딩"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- MaskedTextBox control [Windows Forms]
- data binding [Windows Forms], MaskedTextBox control [Windows Forms]
- MaskedTextBox control [Windows Forms], binding data
ms.assetid: 34b29f07-e8df-48d4-b08b-53fcca524708
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: cb3fd4038634969d34be4514f4d314cf5d7513e4
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-bind-data-to-the-maskedtextbox-control"></a>방법: MaskedTextBox 컨트롤에 데이터 바인딩
데이터를 바인딩할 수 있습니다는 <xref:System.Windows.Forms.MaskedTextBox> 다른 Windows Forms 컨트롤에 경우와 마찬가지로 제어 합니다. 그러나 데이터베이스의 데이터 형식 마스크 정의 필요한 형식이 일치 하지 않는 데이터의 서식을 다시 지정 해야 합니다. 다음 절차를 사용 하 여 수행 하는 방법을 보여 줍니다는 <xref:System.Windows.Forms.Binding.Format> 및 <xref:System.Windows.Forms.Binding.Parse> 의 이벤트는 <xref:System.Windows.Forms.Binding> 클래스를 별도 전화 번호를 표시 및 편집할 수 있는 단일 필드로 확장 데이터베이스 필드에 전화 합니다.  
  
 다음 절차는 Northwind 샘플 데이터베이스가 설치 된 SQL Server 데이터베이스에 액세스할 수 있어야 합니다.  
  
### <a name="to-bind-data-to-a-maskedtextbox-control"></a>MaskedTextBox 컨트롤에 데이터를 바인딩할  
  
1.  새 Windows Forms 프로젝트를 만듭니다.  
  
2.  두 개 <xref:System.Windows.Forms.TextBox> ; 양식에 컨트롤 이름을 지정 하 여 `FirstName` 및 `LastName`합니다.  
  
3.  끌어서는 <xref:System.Windows.Forms.MaskedTextBox> 컨트롤을 양식에; 이름을 `PhoneMask`합니다.  
  
4.  설정의 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 속성 `PhoneMask` 를 `(000) 000-0000 x9999`합니다.  
  
5.  폼에 다음 네임 스페이스 가져오기를 추가 합니다.  
  
    ```csharp  
    using System.Data.SqlClient;  
    ```  
  
    ```vb  
    Imports System.Data.SqlClient  
    ```  
  
6.  폼을 마우스 오른쪽 단추로 클릭 하 고 선택 **코드 보기**합니다. 아무 곳 이나 폼 클래스에이 코드를 추가 합니다.  
  
    ```csharp  
    Binding currentBinding, phoneBinding;  
    DataSet employeesTable = new DataSet();  
    SqlConnection sc;  
    SqlDataAdapter dataConnect;  
  
    private void Form1_Load(object sender, EventArgs e)  
    {  
        DoMaskBinding();  
    }  
  
    private void DoMaskBinding()  
    {  
        try  
        {  
            sc = new SqlConnection("Data Source=CLIENTUE;Initial Catalog=NORTHWIND;Integrated Security=SSPI");  
            sc.Open();  
        }  
        catch (Exception ex)  
        {  
            MessageBox.Show(ex.Message);  
            return;  
        }  
  
        dataConnect = new SqlDataAdapter("SELECT * FROM Employees", sc);  
        dataConnect.Fill(employeesTable, "Employees");  
  
        // Now bind MaskedTextBox to appropriate field. Note that we must create the Binding objects  
        // before adding them to the control - otherwise, we won't get a Format event on the   
        // initial load.   
        try  
        {  
            currentBinding = new Binding("Text", employeesTable, "Employees.FirstName");  
            firstName.DataBindings.Add(currentBinding);  
  
            currentBinding = new Binding("Text", employeesTable, "Employees.LastName");  
            lastName.DataBindings.Add(currentBinding);  
  
            phoneBinding =new Binding("Text", employeesTable, "Employees.HomePhone");  
            // We must add the event handlers before we bind, or the Format event will not get called  
            // for the first record.  
            phoneBinding.Format += new ConvertEventHandler(phoneBinding_Format);  
            phoneBinding.Parse += new ConvertEventHandler(phoneBinding_Parse);  
            phoneMask.DataBindings.Add(phoneBinding);  
        }  
        catch (Exception ex)  
        {  
            MessageBox.Show(ex.Message);  
            return;  
        }  
    }  
    ```  
  
    ```vb  
    Dim WithEvents CurrentBinding, PhoneBinding As Binding  
    Dim EmployeesTable As New DataSet()  
    Dim sc As SqlConnection  
    Dim DataConnect As SqlDataAdapter  
  
    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load  
        DoMaskedBinding()  
    End Sub  
  
    Private Sub DoMaskedBinding()  
        Try  
            sc = New SqlConnection("Data Source=SERVERNAME;Initial Catalog=NORTHWIND;Integrated Security=SSPI")  
            sc.Open()  
        Catch ex As Exception  
            MessageBox.Show(ex.Message)  
            Exit Sub  
        End Try  
  
        DataConnect = New SqlDataAdapter("SELECT * FROM Employees", sc)  
        DataConnect.Fill(EmployeesTable, "Employees")  
  
        ' Now bind MaskedTextBox to appropriate field. Note that we must create the Binding objects  
        ' before adding them to the control - otherwise, we won't get a Format event on the   
        ' initial load.  
        Try  
            CurrentBinding = New Binding("Text", EmployeesTable, "Employees.FirstName")  
            firstName.DataBindings.Add(CurrentBinding)  
            CurrentBinding = New Binding("Text", EmployeesTable, "Employees.LastName")  
            lastName.DataBindings.Add(CurrentBinding)  
            PhoneBinding = New Binding("Text", EmployeesTable, "Employees.HomePhone")  
            PhoneMask.DataBindings.Add(PhoneBinding)  
        Catch ex As Exception  
            MessageBox.Show(ex.Message)  
            Application.Exit()  
        End Try  
    End Sub  
    ```  
  
7.  에 대 한 이벤트 처리기를 추가 <xref:System.Windows.Forms.Binding.Format> 및 <xref:System.Windows.Forms.Binding.Parse> 조합 및 분리 하는 이벤트는 `PhoneNumber` 및 `Extension` 필드의 경계에서 <xref:System.Data.DataSet>합니다.  
  
    ```csharp  
    private void phoneBinding_Format(Object sender, ConvertEventArgs e)  
    {  
        String ext;  
  
        DataRowView currentRow = (DataRowView)BindingContext[employeesTable, "Employees"].Current;  
        if (currentRow["Extension"] == null)   
        {  
            ext = "";  
        } else   
        {  
            ext = currentRow["Extension"].ToString();  
        }  
  
        e.Value = e.Value.ToString().Trim() + " x" + ext;  
    }  
  
    private void phoneBinding_Parse(Object sender, ConvertEventArgs e)  
    {  
        String phoneNumberAndExt = e.Value.ToString();  
  
        int extIndex = phoneNumberAndExt.IndexOf("x");  
        String ext = phoneNumberAndExt.Substring(extIndex).Trim();  
        String phoneNumber = phoneNumberAndExt.Substring(0, extIndex).Trim();  
  
        //Get the current binding object, and set the new extension manually.   
        DataRowView currentRow = (DataRowView)BindingContext[employeesTable, "Employees"].Current;  
        // Remove the "x" from the extension.  
        currentRow["Extension"] = ext.Substring(1);  
  
        //Return the phone number.  
        e.Value = phoneNumber;  
    }  
    ```  
  
    ```vb  
    Private Sub PhoneBinding_Format(ByVal sender As Object, ByVal e As ConvertEventArgs) Handles PhoneBinding.Format  
        Dim Ext As String  
  
        Dim CurrentRow As DataRowView = CType(Me.BindingContext(EmployeesTable, "Employees").Current, DataRowView)  
        If (CurrentRow("Extension") Is Nothing) Then  
            Ext = ""  
        Else  
            Ext = CurrentRow("Extension").ToString()  
        End If  
  
        e.Value = e.Value.ToString().Trim() & " x" & Ext  
    End Sub  
  
    Private Sub PhoneBinding_Parse(ByVal sender As Object, ByVal e As ConvertEventArgs) Handles PhoneBinding.Parse  
        Dim PhoneNumberAndExt As String = e.Value.ToString()  
  
        Dim ExtIndex As Integer = PhoneNumberAndExt.IndexOf("x")  
        Dim Ext As String = PhoneNumberAndExt.Substring(ExtIndex).Trim()  
        Dim PhoneNumber As String = PhoneNumberAndExt.Substring(0, ExtIndex).Trim()  
  
        ' Get the current binding object, and set the new extension manually.   
        Dim CurrentRow As DataRowView = CType(Me.BindingContext(EmployeesTable, "Employees").Current, DataRowView)  
        ' Remove the "x" from the extension.  
        CurrentRow("Extension") = CObj(Ext.Substring(1))  
  
        ' Return the phone number.  
        e.Value = PhoneNumber  
    End Sub  
    ```  
  
8.  두 개의 추가 <xref:System.Windows.Forms.Button> 폼에 컨트롤을 합니다. 이름을 지정 하 여 `previousButton` 및 `nextButton`합니다. 추가할 각 단추를 두 번 클릭 한 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기 및 다음 코드 예제와 같이 이벤트 처리기를 입력 합니다.  
  
    ```csharp  
    private void previousButton_Click(object sender, EventArgs e)  
    {  
        BindingContext[employeesTable, "Employees"].Position = BindingContext[employeesTable, "Employees"].Position - 1;  
    }  
  
    private void nextButton_Click(object sender, EventArgs e)  
    {  
        BindingContext[employeesTable, "Employees"].Position = BindingContext[employeesTable, "Employees"].Position + 1;  
    }  
    ```  
  
    ```vb  
    Private Sub PreviousButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles PreviousButton.Click  
        Me.BindingContext(EmployeesTable, "Employees").Position = Me.BindingContext(EmployeesTable, "Employees").Position - 1  
    End Sub  
  
    Private Sub NextButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles NextButton.Click  
        Me.BindingContext(EmployeesTable, "Employees").Position = Me.BindingContext(EmployeesTable, "Employees").Position + 1  
    End Sub  
    ```  
  
9. 샘플을 실행합니다. 데이터를 편집 하 고 사용 하 여는 **이전** 및 **다음** 데이터가 올바르게 유지 되어 있는지 확인 하려면 단추는 <xref:System.Data.DataSet>합니다.  
  
## <a name="example"></a>예  
 다음 코드 예제는 이전 절차를 완료 한 결과를 나열 하는 전체 코드입니다.  
  
 [!code-cpp[MaskedTextBoxData#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/MaskedTextBoxData/cpp/form1.cpp#1)]
 [!code-csharp[MaskedTextBoxData#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/MaskedTextBoxData/CS/form1.cs#1)]
 [!code-vb[MaskedTextBoxData#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/MaskedTextBoxData/VB/form1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
-   만들기는 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 또는 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 프로젝트.  
  
-   추가 <xref:System.Windows.Forms.TextBox> 및 <xref:System.Windows.Forms.MaskedTextBox> 이전 절차에 설명 된 대로을 폼으로 제어 합니다.  
  
-   프로젝트의 기본 폼에 대 한 소스 코드 파일을 엽니다.  
  
-   이전 "코드" 섹션에 나열 된 코드가이 파일의 소스 코드를 바꿉니다.  
  
-   응용 프로그램을 컴파일합니다.  
  
## <a name="see-also"></a>참고 항목  
 [연습: MaskedTextBox 컨트롤 사용](../../../../docs/framework/winforms/controls/walkthrough-working-with-the-maskedtextbox-control.md)
