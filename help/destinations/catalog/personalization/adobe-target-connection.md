---
keywords: 目標個人化；目的地；experience platform target目的地；adobe target目的地；
title: Adobe Target連線
description: Adobe Target是一款應用程式，可在網站、行動應用程式等所有傳入客戶互動中，提供由AI支援的即時個人化和實驗功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: f97b667f8d4dc311683b018bb1c1792aae871648
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Adobe Target連線 {#adobe-target-connection}

## 目標更改日誌 {#changelog}

>[!IMPORTANT]
>
>增強Adobe Target V2目的地連接器測試版推出後，目的地目錄中可能會出現兩個Adobe Target卡。
>Adobe Target V2目的地連接器目前為測試版，僅適用於指定數量的客戶。 除了AdobeV1卡提供的功能外，Target V2連接器還新增 [對應步驟](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 啟用工作流程，此工作流程可讓您將設定檔屬性對應至Adobe Target，啟用以屬性為基礎的同頁和下一頁個人化。

![以並排檢視顯示的兩個Adobe Target目的地卡片影像。](/help/destinations/assets/catalog/personalization/adobe-target-connection/adobe-target-side-by-side-view.png)

## 總覽 {#overview}

Adobe Target是一款應用程式，可在網站、行動應用程式等所有傳入客戶互動中，提供由AI支援的即時個人化和實驗功能。

Adobe Target是Adobe Experience Platform目的地目錄中的個人化連線。

## 先決條件 {#prerequisites}

### 資料流ID {#datastream-id}

將Adobe Target連線設定為 [使用資料流ID](#parameters)，您必須有 [Adobe Experience Platform Web SDK](../../../edge/home.md) 已實作。

在不使用資料流ID的情況下設定Adobe Target連線不需要您實作Web SDK。

>[!IMPORTANT]
>
>建立 [!DNL Adobe Target] 連接，請閱讀有關如何 [為同一頁面和下一頁個人化設定個人化目的地](../../ui/configure-personalization-destinations.md). 本指南會逐步引導您執行相同頁面和下一頁個人化使用案例所需的設定步驟，涵蓋多個Experience Platform元件。 設定Adobe Target連線時，同頁和下一頁個人化需要使用資料流ID。

### Adobe Target的必要條件 {#prerequisites-in-adobe-target}

在Adobe Target中，確認您的使用者：

* 存取 [預設工作區](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* 此 **核准者** [角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

閱讀更多有關授予 [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) 和 [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!DNL Profile request]** | 您正在為單一設定檔要求Adobe Target目的地中對應的所有區段。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 使用案例 {#use-cases}

**個人化首頁橫幅**

一家房屋租賃與銷售公司想要根據Adobe Experience Platform中的客戶區段資格，使用橫幅來個人化其首頁。 公司可以選取哪些對象應該獲得個人化體驗，並將這些對象傳送至Adobe Target，作為其Target選件的鎖定目標條件。

## 連接到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="關於資料流ID"
>abstract="此選項會決定要納入區段的資料收集資料流。 下拉式功能表只會顯示已啟用Target設定的資料流。 若要使用邊緣分段，您必須選取資料流ID。 選取「無」會停用所有使用邊緣分段的使用案例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="進一步了解選取資料流"

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

Adobe Experience Platform會自動連線至您公司的Adobe Target執行個體。 不需要驗證。

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **名稱**:填寫此目的地的首選名稱。
* **說明**:輸入目的地的說明。 例如，您可以提及您使用此目的地的促銷活動。 此欄位為選填欄位。
* **資料流ID**:這會決定要納入區段的資料收集資料流。 下拉式功能表只會顯示已啟用Target和Adobe Experience Platform服務的資料流。 請參閱 [設定資料流](../../../edge/datastreams/configure.md#aep) 以取得如何設定Adobe Experience Platform和Adobe Target資料流的詳細資訊。
   * **[!UICONTROL 無]**:如果您需要設定Adobe Target個人化，但無法實作 [Experience PlatformWeb SDK](../../../edge/home.md). 使用此選項時，從Experience Platform匯出至Target的區段僅支援下次工作階段個人化，且會停用邊緣區段。 如需詳細資訊，請參閱下表。

| 未選擇資料流 | 已選取資料流 |
|---|---|
| <ul><li>[邊緣分割](../../../segmentation/ui/edge-segmentation.md) 不支援。</li><li>[同頁和下一頁個人化](../../ui/configure-personalization-destinations.md) 不支援。</li><li>您只能將區段共用至Adobe Target連線， *預設生產沙箱*.</li><li>若要在不使用資料流ID的情況下設定下次工作階段個人化，請使用 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>邊緣分割可如預期運作。</li><li>[同頁和下一頁個人化](../../ui/configure-personalization-destinations.md) 。</li><li>其他沙箱支援區段共用。</li></ul> |

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至設定檔請求目的地](../../ui/activate-profile-request-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

Adobe Target會從Adobe Experience Platform邊緣網路讀取設定檔資料，因此不會匯出任何資料。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).
