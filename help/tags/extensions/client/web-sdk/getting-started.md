---
title: 開始使用網路SDK標籤擴充功能
description: 使用網頁Adobe Experience Platform標籤擴充功能，將事件資料傳送至SDK Edge Network。
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# 開始使用網路SDK標籤擴充功能

使用Adobe Experience Platform的&#x200B;**標籤** （先前稱為Launch），將事件資料從您的網站傳送至Edge Network和下游Adobe解決方案。

在執行這些步驟之前，請確定您可以存取下列[屬性權利](/help/tags/ui/administration/user-permissions.md)：

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

此外，請確定您擁有下列類別的所有[許可權](/help/access-control/home.md#permissions)：

* 資料模式
* 身分識別

## 建立 XDM 結構描述 {#schema}

[Experience Data Model (XDM)](/help/xdm/home.md)是開放原始碼規格，以結構描述形式提供資料的通用結構和定義。 將資料傳送至Edge Network時，強烈建議設定結構描述。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**。
1. 選擇「**[!UICONTROL Create schema]**」。
1. 選取&#x200B;**[!UICONTROL Experience Event]**，然後選取&#x200B;**[!UICONTROL Next]**。
1. 為結構描述指定所需的名稱，然後選取&#x200B;**[!UICONTROL Finish]**。
1. （選擇性）您可以新增更多欄位或[欄位群組](/help/xdm/ui/resources/field-groups.md)，以取得您要收集的任何其他資料。

![結構描述畫布](assets/getting-started/schema-structure.png)

>[!NOTE]
>\
>儲存後，結構描述僅允許&#x200B;*加總*&#x200B;變更。 如需詳細資訊，請參閱[結構描述演變](/help/xdm/schema/composition.md#evolution)。

## 建立資料串流 {#datastream}

[資料串流](/help/datastreams/overview.md)是告訴Edge Network如何處理您傳送之資料的設定。 當您設定資料流以傳送資料給指定產品時，資料流會以特定產品可理解的方式，自動將相關資料傳遞至每個個別產品。

1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**。
1. 選擇「**[!UICONTROL New datastream]**」。
1. 為資料流指定所需的名稱，並在&#x200B;**[!UICONTROL Mapping schema]**&#x200B;下選取最近建立的結構描述。
1. 選擇「**[!UICONTROL Save]**」。

![資料串流清單](assets/getting-started/datastreams.png)

## 建立標籤屬性

建立方案和資料流後，您可以建立和設定標籤屬性。

1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選擇「**[!UICONTROL New property]**」。
1. 為標籤屬性指定所需的名稱和網域，然後選取&#x200B;**[!UICONTROL Save]**。

## 安裝標籤擴充功能

Web SDK標籤擴充功能會安裝在指定的標籤屬性上。

1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**。
1. 選取 **[!UICONTROL Catalog]** 索引標籤。
1. 使用搜尋來尋找&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;副檔名。
1. 選取擴充功能卡片，然後在右側選取「**[!UICONTROL Install]**」。

![安裝SDK](assets/getting-started/install-sdk.png)

## 設定標籤擴充功能

當您安裝Web SDK標籤擴充功能時，會自動移至[設定](configure/config-overview.md)頁面。

1. 在[資料串流區段](configure/datastreams.md)下，為每個環境選取所需的資料串流。

所有其他組態設定都會為您填寫或選擇性。 設定任何需要的組態設定，然後選取&#x200B;**[!UICONTROL Save]**。

## 建立變數資料元素

Adobe建議使用[變數](data-element-types.md#variable)資料元素來儲存您要傳送至Adobe的裝載。 XDM物件也是可用的資料元素，但在適用的使用案例中會較舊且較為受限。

1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 選取&#x200B;**[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]**。
1. 在左側為資料元素指定下列屬性：
   * **[!UICONTROL Name]**：任何需要的名稱
   * **[!UICONTROL Extension]**：[!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**：[!UICONTROL Variable]
1. 在右側設定下列屬性：
   **變數型別**： XDM
   **[!UICONTROL Sandbox]**：您建立結構描述的沙箱
   **[!UICONTROL Schema]**：所需的結構描述
1. 選擇「**[!UICONTROL Save]**」。

## 建立規則

規則會決定您何時想要觸發某專案或設定變數。 建立每當程式庫載入時執行的規則，可讓您輕鬆填入想在每個頁面上包含值的變數。

1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 選取&#x200B;**[!UICONTROL Rules]** > **[!UICONTROL Add rule]**。
1. 為規則指定所需的名稱。
1. 選取`+`旁的&#39;**[!UICONTROL Events]**&#39;圖示。
1. 為事件提供下列設定：
   * **[!UICONTROL Extension]**：[!UICONTROL Core]
   * **[!UICONTROL Event type]**：[!UICONTROL Library loaded (page top)]
1. 選擇「**[!UICONTROL Keep changes]**」。

上述步驟會建立規則的條件部分，這會在程式庫載入後觸發。 下列步驟會建立當符合該條件時要採取的動作。

1. 選取`+`旁的&#39;**[!UICONTROL Actions]**&#39;圖示。
1. 在左側為動作執行下列設定：
   * **[!UICONTROL Extension]**：[!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**：[!UICONTROL Send event]
1. 在右側設定下列欄位：
   * **[!UICONTROL XDM]**： XDM變數資料元素
1. 選擇「**[!UICONTROL Keep changes]**」。

![動作設定](assets/getting-started/action-config.png)

## 發佈

標籤屬性包含將資料傳送至Edge Network所需的所有元件。

1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**。
1. 選擇「**[!UICONTROL Add library]**」。
1. 為程式庫提供所需的名稱。 使用版本控制軟體時，請考量這個名稱與認可名稱類似。
1. 將環境下拉式功能表設定為&#x200B;**[!UICONTROL Development]**。
1. 選擇「**[!UICONTROL Add all changed resources]**」。
1. 選擇「**[!UICONTROL Save & build to Development]**」。

您的變更現在已部署至開發環境。

1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**。
1. 選取開發環境旁的安裝圖示
1. 在網站的測試網頁中安裝內嵌程式碼。

一旦您驗證標籤是否適用於您的開發環境，您就可以使用[!UICONTROL Publishing flow]介面將程式庫發佈到測試環境，然後最終發佈到生產環境。

1. 將擴充功能和規則新增至&#x200B;**資料庫**、建置至&#x200B;**環境**，並在您的網站上安裝內嵌程式碼。
2. 使用&#x200B;**Adobe Experience Platform Debugger**&#x200B;進行驗證。

您現在已具備精簡設定，可擷取事件並傳送至Edge Network。 您現在可以將欄位新增至結構、將產品新增至資料串流，或將資料元素新增至標籤屬性，以進一步建立您的實作。
