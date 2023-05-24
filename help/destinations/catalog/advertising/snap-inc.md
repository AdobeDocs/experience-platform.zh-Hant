---
title: Snap Inc連接
description: 瞭解如何連接到Snapchat廣告平台，並將您的觀眾群從Experience Platform中導出。
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 988ecbed3084ef162453c9f1124998c6e9ae2e45
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---

# Snap Inc連接

## 總覽 {#overview}

[Snapchat廣告](https://forbusiness.snapchat.com/) 不管規模大小和行業如何，每家企業都能生產。 通過全屏數字廣告，成為Snapchatters日常對話的一部分，這些廣告能夠激勵對您的業務最重要的人採取行動。

>[!IMPORTANT]
>
>此文檔頁面由 *Snap公司* 團隊。 如有任何查詢或更新請求，請直接聯繫他們，地址為： *dev-support@snap.com*

## 使用案例 {#use-cases}

這個目的地使營銷人員能夠將通過Experience Platform建立的用戶段導入Snapchat廣告中，並用它們來瞄準他們的廣告。

## 先決條件 {#prerequisites}

要使用此目的地，您必須擁有Snapchat廣告帳戶。 有關如何建立文檔的資訊，請參閱本文檔：

[Snapchat廣告入門](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## 限制 {#limitations}

* Snap Inc不支援給定受眾群的多個身份。 激活段時，請只映射一個標識。
* Snap Inc不支援更名段。 要更名段，必須停用、更名，然後激活它。
* 無法為受眾群的成員定義保留期。 所有成員都具有生存期保留期，並將處於段中，直到刪除。

## 支援的身份 {#supported-identities}

的 *Snap公司* 目標支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

發送到的所有標識符 *Snap公司* 目標必須以SHA-256格式散列。 要在將純文字檔案標識符發送到目標之前對其進行散列，請檢查 **[!UICONTROL 應用轉換]** 選項。

>[!WARNING]
> 
> Snap Inc目標將不接受未散列的標識符，發送這些標識符可能會導致錯誤。


>[!IMPORTANT]
> 
> Snap Inc目標不支援多個標識。 請只選擇一個標識。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| Email Address | SHA-256散列電子郵件地址 | 將電子郵件地址映射到目標標識欄位 *電子郵件地址*。 |
| 電話號碼 | SHA-256散列電話號碼 | 將電子郵件地址映射到目標標識欄位 *電話號碼*。 |
| GAID | SHA-256散列Google廣告ID | 將Google廣告ID映射到目標標識欄位 *蓋德*。 |
| IDFA | SHA-256散列Apple廣告ID | 將Apple廣告ID映射到目標標識欄位 *伊德法*。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中使用的標識符（名稱、電話號碼或其他） *您的目標* 目標。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 正在連接到Snap Inc {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

### 驗證到目標 {#authenticate}

要驗證到目標，請執行以下步驟：

1. 查找 *Snap公司* 目標，從Adobe Experience Platform目錄中選擇 **設定**。
2. 選擇 **[!UICONTROL 連接到目標]**。 您將被重定向到以下螢幕：
   ![身份驗證螢幕1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. 輸入Snapchat憑據並選擇 **登錄**。
4. 你將看到Adobe Experience Platform能夠訪問的Snapchat資料。 選擇 **繼續** 繼續連接過程。

![身份驗證螢幕2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

選擇「繼續」後，等待您重定向回Adobe Experience Platform。

### 填寫目標詳細資訊 {#destination-details}

![目標詳細資訊](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

要配置目標的詳細資訊，請填寫必填欄位並選擇 **[!UICONTROL 下一個]**。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 帳戶ID]**:與要將段導入的Ad帳戶關聯的Ad帳戶ID。 有關如何查找此項的詳細資訊，請參閱 [Snapchat業務幫助中心上的此文檔](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US)。

>[!IMPORTANT]
> 
>輸入不正確或無效的Snapchat廣告帳戶ID將導致段激活失敗。 請仔細檢查您是否輸入了正確的廣告帳戶ID。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 驗證資料導出 {#exported-data}

將段激活到 *Snap公司* 目標，您將能夠在Snap Ads管理器的 [**觀眾** 節](https://businesshelp.snapchat.com/s/article/audience-sharing)。 要導航到此部分，請執行以下步驟：

1. 登錄 [快照廣告管理器](https://ads.snapchat.com/)
2. 選擇 **觀眾** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。 您將在「受眾庫」中看到在Adobe Experience Platform激活的段：

![受眾](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

請注意，當Adobe段首次激活到Snap Inc時，您最初將視其為空受眾。 這是因為Adobe Experience Platform在評估該段之前不會將成員資料導出到Snap Inc。 有關如何在Experience Platform中評估段的詳細資訊，請參閱 [分段服務概述](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments)。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。
