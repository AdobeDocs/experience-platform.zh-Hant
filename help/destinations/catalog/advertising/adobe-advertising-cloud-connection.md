---
title: Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP是Adobe Real-time Customer Data Platform的一個整合目的地，使您能夠與經認證的廣告商和用戶共用經過認證的第一方片段，以便激活活動。
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---

# Adobe Advertising Cloud DSP

## 總覽 {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)目標允許您與經認證的廣告商和用戶共用經過身份驗證的第一方段，以便與他們一起激活活DSP動。 要瞭解有關與的Real-Time CDP整合的詳細信DSP息，請參閱 [關於從受眾源激活經過驗證的段](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html)。

>[!IMPORTANT]
>
>此頁面由團隊創DSP建。 如有任何查詢或更新請求，請直接聯繫Advertising Cloud支援人員，地址為： `adcloud_support@adobe.com`。

## 使用案例 {#use-cases}

為了幫助您更好地瞭解您應如何以及何時使用Advertising Cloud DSP目標，以下是Adobe Experience Platform客戶可通過使用此目標解決的示例使用案例。

### 品牌廣告使用案例

一家線上零售商希望通過展示活動來重新瞄準其高價值客戶，而不用使用Cookie來進行瞄準。 該零售商與其Adobe Real-time Customer Data Platform(Real-Time CDP)帳戶共用一個分類，其中包括其高價值客戶的散列電子郵件IDDSP。 然DSP後將經過散列的電子郵件ID轉換為經過驗證 [!DNL RampIDs] 與LiveRamp合DSP作。 結果 [!DNL RampIDs] 可用於顯示市場活動以針對受眾。

### 代理使用案例

一家擁有賬戶的媒DSP體公司正代表其客戶開展一項重新定位活動。 該品牌希望在去年以新的促銷優惠來重新瞄準所有客人。 該品牌在中承載所有來賓資訊 [!DNL Real-Time CDP]。 該品牌可以共用一個網段，該網段包含其來賓的散列電子郵件ID [!DNL Real-Time CDP] 通過媒體宣傳活動DSP將客人重新定向到媒體賬戶。

## 先決條件 {#prerequisites}

* 帳DSP戶級和市場活動級設定，以啟用段共用 [!DNL LiveRamp RampID]將客戶資料轉換為 [!DNL RampIDs] 建立目標段。 您的DSP帳戶團隊將執行此配置。 [!DNL RampID] 可通過與之間的DSP夥伴關係 [!DNL LiveRamp]而你不需要自己的 [!DNL LiveRamp] 成員身份。
* Experience Cloud帳戶的Experience Platform組織ID。 你可以在你的 [!DNL Real-Time CDP] 用戶配置檔案頁面。
* A [[!DNL Real-Time CDP] 源DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) 接收市場活動激活的段。 您的DSP帳戶團隊將使用您的Experience Cloud組織ID建立源。
* 帳戶或廣DSP告商的源密鑰 [[!DNL Real-Time CDP] 源建立於DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html)。 您的DSP帳戶團隊將與您共用此密鑰。 您將在Experience Platform中使用它建立到Advertising Cloud DSP目標的目標連接，如 [下文](#authenticate)。
* 由電子郵件或散列電子郵件組成的客戶資料。

## 支援的身份 {#supported-identities}

Adobe Advertising Cloud DSP目的地支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | Experience Platform支援純文字檔案和SHA256散列電子郵件地址。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項，使Experience Platform在激活時自動對資料進行散列。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中包含在Advertising Cloud DSP目標中使用的標識符（電子郵件或散列電子郵件）。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 當基於段評估在Experience Platform中更新簡檔時，連接器將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions) Experience Platform。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到目標，請按照說明 [建立目標連接](/help/destinations/ui/connect-destination.md) 使用Experience Platform用戶介面。 在目標配置工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要連接到目標，請在 [!UICONTROL 連接類型] ，然後選擇 **[!UICONTROL 連接到目標]**:

* **[!UICONTROL 帳戶或廣告商密鑰]**:此 [!UICONTROL 源密鑰] 在 [[!DNL Real-Time CDP] 源在用戶介面DSP中建立](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html)。 您的DSP帳戶團隊將在建立源後與您共用此密鑰。

![連接類型欄位](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。

![目標詳細資訊欄位](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 驗證資料導出 {#exported-data}

要驗證資料段是否與Advertising Cloud共用，請檢查以下內容：

* 您的資料流 [!DNL Real-Time CDP] 目標成功。

* 在DSP中，當您從中建立或編輯受眾時 [!UICONTROL 觀眾] > [!UICONTROL 所有受眾] 或從 [!UICONTROL 受眾目標] 的子菜單。 段應在 [!UICONTROL Adobe段] 頁籤 [!UICONTROL Real-Time CDP] 的子菜單。

![Real-Time CDP段DSP在受眾設定](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。
