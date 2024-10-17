---
title: 建立動態資料流設定
description: 瞭解如何根據規則建立動態資料串流設定，以將您的資料路由至各種Experience Cloud服務。
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
source-git-commit: 86416dc11f92a774cda5d95365d3981a637a5595
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---


# 建立動態資料流設定

>[!AVAILABILITY]
>
>* 定義動態資料流設定的選專案前在Beta中，可供有限數量的客戶使用。 若要獲得此功能的存取權，請聯絡您的Adobe代表。 文件和功能可能會有所變更。

根據預設，Experience PlatformEdge Network會將到達資料串流的所有事件傳送至您為資料串流啟用的所有Experience Cloud[服務](configure.md#add-services)。 根據您的使用案例，這可能並不總是適合您的理想工作流程。

動態資料流設定可透過使用者可設定的規則集來解決此問題，這些規則集是針對為資料流啟用的每個服務定義的，會指定應該接收每種資料型別的Experience Cloud解決方案。

## 先決條件 {#prerequisites}

若要為資料串流建立動態設定，您必須符合兩個條件：

* 您必須已建立至少&#x200B;*個*&#x200B;資料流才能使用。 如需詳細資訊，請參閱有關如何[建立資料流](configure.md)的檔案。
* 您必須將&#x200B;*至少*&#x200B;個Experience Cloud服務新增至資料流。 如需詳細資訊，請參閱有關如何[新增服務](configure.md#add-services)到資料流的檔案。

建立資料串流並新增Experience Cloud服務之後，您可以[建立動態組態](#create-dynamic-configuration)。

## 建立動態資料流設定 {#create-dynamic-configuration}

在您[建立資料流](configure.md)並[新增服務](configure.md#add-services)之後，請依照下列步驟將動態設定新增至服務。

1. 移至&#x200B;**[!UICONTROL 資料收集]** > **[!UICONTROL 資料串流]**&#x200B;頁面，並選取您建立的資料串流。

   ![顯示資料串流清單的資料串流使用者介面影像。](assets/configure-dynamic-datastream/select-datastream.png)

1. 在您要定義動態組態的服務上選取&#x200B;**[!UICONTROL 編輯]**&#x200B;選項。

   ![資料串流使用者介面的影像，顯示新增至資料串流的服務。](assets/configure-dynamic-datastream/select-service.png)

1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;頁面中，選取&#x200B;**[!UICONTROL 儲存並編輯動態設定]**。

   ![顯示資料流設定頁面之資料流使用者介面的影像。](assets/configure-dynamic-datastream/save-and-edit.png)

1. 選取&#x200B;**[!UICONTROL 新增動態組態]**。

   ![資料串流使用者介面的影像，顯示未新增規則的動態設定。](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. 從&#x200B;**[!UICONTROL 資源]**&#x200B;面板，將您想要用來建置規則的專案拖放到視窗右側。 您可以合併多個資源以建置複雜規則。

   使用每個資源的選項，例如&#x200B;**[!UICONTROL 等於]**、**[!UICONTROL 不等於]**、**[!UICONTROL 存在]**&#x200B;等等，以微調規則。

   ![顯示動態設定規則之資料串流使用者介面的影像。](assets/configure-dynamic-datastream/drag-resources.png)

1. 在&#x200B;**[!UICONTROL 組態]**&#x200B;區段中，根據您是否要傳送資料給每個服務，切換您要為每個規則啟用或停用的服務。 如果您關閉切換功能，規則會停用，且&#x200B;*所有資料*&#x200B;都會傳送至上游服務。

   ![顯示動態設定規則之資料串流使用者介面的影像。](assets/configure-dynamic-datastream/enable-service.png)

1. 設定完規則後，選取[儲存]。****

## 規則優先順序的考量事項 {#considerations}

您可以為每個動態資料流設定定義多個規則。 但是，如果您的資料符合多個規則的條件，則只會考慮清單中的第一個相符規則，而所有其他相符規則則會被忽略。

若要達到所需的資料路由行為，請留意規則的排列順序。

若要設定規則順序，您可以依照所需的順序拖放規則視窗。

![顯示如何透過拖放變更規則順序的GIF。](assets/configure-dynamic-datastream/move-rules.gif)