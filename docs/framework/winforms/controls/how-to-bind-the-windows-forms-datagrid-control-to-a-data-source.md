---
title: 将数据网格控制绑定到数据源
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- datasets [Windows Forms], binding to DataGrid control
- data binding [Windows Forms], DataGrid control
- DataGrid control [Windows Forms], data binding
- bound controls [Windows Forms], DataGrid control
- Windows Forms controls, data binding
- bound controls [Windows Forms]
- data-bound controls [Windows Forms], DataGrid
ms.assetid: 128cdb07-dfd3-4d60-9d6a-902847667c36
ms.openlocfilehash: 42514c6a0ab9cf912a32b13675a069976632ece5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182244"
---
# <a name="how-to-bind-the-windows-forms-datagrid-control-to-a-data-source"></a>如何：将 Windows 窗体 DataGrid 控件绑定到数据源
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。 有关详细信息，请参阅 [Windows 窗体 DataGridView 控件与 DataGrid 控件之间的区别](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 Windows 窗体<xref:System.Windows.Forms.DataGrid>控件专为显示数据源中的信息而设计。 通过调用<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>方法在运行时绑定控件。 尽管可以显示来自各种数据源的数据，但最典型的来源是数据集和数据视图。  
  
### <a name="to-data-bind-the-datagrid-control-programmatically"></a>以编程方式绑定 DataGrid 控件  
  
1. 编写代码以填充数据集。  
  
     如果数据源是基于数据集表的数据集或数据视图，请向窗体添加代码以填充数据集。  
  
     您使用的确切代码取决于数据集获取数据的位置。 如果数据集直接从数据库填充，则通常调用数据适配器`Fill`的方法，如以下示例所示，该方法填充名为 的`DsCategories1`数据集：  
  
    ```vb  
    sqlDataAdapter1.Fill(DsCategories1)  
    ```  
  
    ```csharp  
    sqlDataAdapter1.Fill(DsCategories1);  
    ```  
  
    ```cpp  
    sqlDataAdapter1->Fill(dsCategories1);  
    ```  
  
     如果数据集是从 XML Web 服务填充的，则通常在代码中创建服务的实例，然后调用其方法之一来返回数据集。 然后，将 XML Web 服务中的数据集合并到本地数据集中。 下面的示例演示如何创建名为`CategoriesService`的 XML Web 服务的实例， 调用其`GetCategories`方法，并将生成的数据集合并到称为`DsCategories1`：  
  
    ```vb  
    Dim ws As New MyProject.localhost.CategoriesService()  
    ws.Credentials = System.Net.CredentialCache.DefaultCredentials  
    DsCategories1.Merge(ws.GetCategories())  
    ```  
  
    ```csharp  
    MyProject.localhost.CategoriesService ws = new MyProject.localhost.CategoriesService();  
    ws.Credentials = System.Net.CredentialCache.DefaultCredentials;  
    DsCategories1.Merge(ws.GetCategories());  
    ```  
  
    ```cpp  
    MyProject::localhost::CategoriesService^ ws =
       new MyProject::localhost::CategoriesService();  
    ws->Credentials = System::Net::CredentialCache::DefaultCredentials;  
    dsCategories1->Merge(ws->GetCategories());  
    ```  
  
2. 调用控件<xref:System.Windows.Forms.DataGrid><xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>的方法，传递数据源和数据成员。 如果不需要显式传递数据成员，则传递一个空字符串。  
  
    > [!NOTE]
    > 如果首次绑定网格，则可以设置控件和<xref:System.Windows.Forms.DataGrid.DataSource%2A><xref:System.Windows.Forms.DataGrid.DataMember%2A>属性。 但是，在设置这些属性后，无法重置这些属性。 因此，建议您始终使用 方法<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>。  
  
     下面的示例演示如何在称为`DsCustomers1`： 的数据集中以编程方式绑定到客户表：  
  
    ```vb  
    DataGrid1.SetDataBinding(DsCustomers1, "Customers")  
    ```  
  
    ```csharp  
    DataGrid1.SetDataBinding(DsCustomers1, "Customers");  
    ```  
  
    ```cpp  
    dataGrid1->SetDataBinding(dsCustomers1, "Customers");  
    ```  
  
     如果"客户"表是数据集中的唯一表，则可以以这种方式绑定网格：  
  
    ```vb  
    DataGrid1.SetDataBinding(DsCustomers1, "")  
    ```  
  
    ```csharp  
    DataGrid1.SetDataBinding(DsCustomers1, "");  
    ```  
  
    ```cpp  
    dataGrid1->SetDataBinding(dsCustomers1, "");  
    ```  
  
3. （可选）将适当的表样式和列样式添加到网格中。 如果没有表样式，您将看到该表，但格式最小且所有列可见。  
  
## <a name="see-also"></a>另请参阅

- [DataGrid 控件概述](datagrid-control-overview-windows-forms.md)
- [如何：向 Windows 窗体 DataGrid 控件添加表和列](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)
- [DataGrid 控件](datagrid-control-windows-forms.md)
- [Windows 窗体数据绑定](../windows-forms-data-binding.md)
