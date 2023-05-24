---
title: Zendesk連接
description: Zendesk目標允許您導出帳戶資料並在Zendesk中激活它以滿足您的業務需要。
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 55f1eafa68124b044d20f8f909f6238766076a7a
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 1%

---

# [!DNL Zendesk] 連接

[[!DNL Zendesk]](https://www.zendesk.com) 是客戶服務解決方案和銷售工具。

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [[!DNL Zendesk] 聯繫人API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)。 **建立和更新身份** 作為分部內聯繫人 [!DNL Zendesk]。

[!DNL Zendesk] 使用承載令牌作為與通信的驗證機制 [!DNL Zendesk] 聯繫人API。 驗證到您 [!DNL Zendesk] 下面是實例， [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

多渠道B2C平台的客戶服務部門希望確保其客戶獲得無縫的個性化體驗。 部門可以從自己的離線資料構建段，以建立新的用戶配置檔案或更新來自不同交互的現有配置檔案資訊（例如採購、退貨等）。 把這些片段從Adobe Experience Platform [!DNL Zendesk]。 將更新的資訊 [!DNL Zendesk] 確保客戶服務代理立即獲得客戶的最新資訊，從而加快響應和解決速度。

## 先決條件 {#prerequisites}

### Experience Platform先決條件 {#prerequisites-in-experience-platform}

在將資料激活到 [!DNL Zendesk] 目標，您必須 [架構](/help/xdm/schema/composition.md)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。

請參閱Experience Platform文檔，瞭解 [段成員身份詳細資訊架構欄位組](/help/xdm/field-groups/profile/segmentation.md) 如果需要有關段狀態的指導。

### [!DNL Zendesk] 先決條件 {#prerequisites-destination}

為了將資料從平台導出到 [!DNL Zendesk] 你需要的帳戶 [!DNL Zendesk] 帳戶。

#### 收集 [!DNL Zendesk] 憑據 {#gather-credentials}

在驗證到 [!DNL Zendesk] 目標：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `Bearer token` | 您在中生成的訪問令牌 [!DNL Zendesk] 帳戶。 <br> 按照文檔進行 [生成 [!DNL Zendesk] 訪問令牌](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) 如果你沒有。 | `a0b1c2d3e4...v20w21x22y23z` |

## 護欄 {#guardrails}

的 [定價和費率限制](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) 頁面詳細資訊 [!DNL Zendesk] 與帳戶關聯的API限制。 您需要確保您的資料和負載在這些限制範圍內。

## 支援的身份 {#supported-identities}

[!DNL Zendesk] 支援更新下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 範例 | 說明 | 必要 |
|---|---|---|---|
| `email` | `test@test.com` | 聯繫人的電子郵件地址。 | 是 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | <ul><li>您正在導出段的所有成員以及所需的架構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位映射。</li><li> 中的每個段狀態 [!DNL Zendesk] 將根據 **[!UICONTROL 映射ID]** 值 [段調度](#schedule-segment-export-example) 的子菜單。</li></ul> |
| 導出頻率 | **[!UICONTROL 流]** | <ul><li>流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

在 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]** 搜索 [!DNL Zendesk]。 或者，可將其定位在 **[!UICONTROL CRM]** 的子菜單。

### 驗證到目標 {#authenticate}

填寫下面的必填欄位。 請參閱 [收集 [!DNL Zendesk] 憑據](#gather-credentials) 的雙曲餘切值。
* **[!UICONTROL 持有者令牌]**:您在中生成的訪問令牌 [!DNL Zendesk] 帳戶。

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**。
![平台UI螢幕快照，顯示如何進行身份驗證。](../../assets/catalog/crm/zendesk/authenticate-destination.png)

如果提供的詳細資訊有效，UI將顯示 **[!UICONTROL 已連接]** 狀態為綠色複選標籤。 然後，可以繼續下一步。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。
![顯示目標詳細資訊的平台UI螢幕快照。](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
>
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射注意事項和示例 {#mapping-considerations-example}

正確將您的受眾資料從Adobe Experience Platform發送到 [!DNL Zendesk] 目標，您需要完成欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。

在 **[!UICONTROL 目標欄位]** 應按照屬性映射表中所述命名，因為這些屬性將構成請求正文。

在 **[!UICONTROL 源欄位]** 不要遵守任何此類限制。 您可以根據需要對其進行映射，但是，如果資料格式在推入到 [!DNL Zendesk] 會導致錯誤。

正確將XDM欄位映射到 [!DNL Zendesk] 目標欄位，請執行以下步驟：

1. 在 **[!UICONTROL 映射]** 步驟，選擇 **[!UICONTROL 添加新映射]**。 螢幕上將顯示新的映射行。
1. 在 **[!UICONTROL 選擇源欄位]** ，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選擇XDM屬性或 **[!UICONTROL 選擇標識命名空間]** 並選擇標識。
1. 在 **[!UICONTROL 選擇目標欄位]** ，選擇 **[!UICONTROL 選擇標識命名空間]** 選擇目標標識，或選擇 **[!UICONTROL 選擇屬性]** 類別，然後選擇支援的架構屬性之一。
   * 重複這些步驟以添加以下強制映射，您還可以添加要在XDM配置檔案架構和XDM配置檔案架構之間更新的任何其他屬性 [!DNL Zendesk] 實例： |源欄位|目標欄位|強制| |—|—| |`xdm: person.name.lastName`|`xdm: last_name`|是 | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * 下面顯示了使用這些映射的示例：
      ![平台UI螢幕快照示例，包含屬性映射。](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>的 `Attribute: last_name` 和 `Identity: email` 目標映射是此目標的必需映射。 如果缺少這些映射，則忽略任何其他映射，而不將其發送到 [!DNL Zendesk]。

完成為目標連接提供映射後，選擇 **[!UICONTROL 下一個]**。

### 計畫段導出和示例 {#schedule-segment-export-example}

在 [[!UICONTROL 計畫段導出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在激活工作流的步驟中，必須手動將平台段映射到中的自定義欄位屬性 [!DNL Zendesk]。

為此，請選擇每個段，然後輸入相應的自定義欄位屬性 [!DNL Zendesk] 的 **[!UICONTROL 映射ID]** 的子菜單。

下面顯示了一個示例：
![平台UI螢幕快照示例，顯示「計畫」段導出。](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## 驗證資料導出 {#exported-data}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 選擇 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 導航到目標清單。
1. 接下來，選擇目標並切換到 **[!UICONTROL 激活資料]** ，然後選擇段名稱。
   ![平台UI螢幕快照示例，顯示目標激活資料。](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. 監視段摘要並確保配置檔案的計數與段內的計數相對應。
   ![平台UI螢幕抓圖示例顯示「段」。](../../assets/catalog/crm/zendesk/segment.png)

1. 登錄到 [!DNL Zendesk] ，然後導航到 **[!UICONTROL 聯繫人]** 的子菜單。 此清單可配置為顯示使用段建立的附加欄位的列 **[!UICONTROL 映射ID]** 和段狀態。
   ![Zendesk UI螢幕快照顯示「聯繫人」頁面，其中包含使用段名稱建立的附加欄位。](../../assets/catalog/crm/zendesk/contacts.png)

1. 或者，可以深入到單個 **[!UICONTROL 人員]** 並檢查 **[!UICONTROL 其他欄位]** 中顯示段名稱和段狀態。
   ![Zendesk UI螢幕快照顯示「人員」頁，其中附加欄位部分顯示段名稱和段狀態。](../../assets/catalog/crm/zendesk/contact.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

來自 [!DNL Zendesk] 文檔如下：
* [打第一個電話](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [自定義欄位](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### 更改日誌

本節將捕獲對此目標連接器進行的功能和重要文檔更新。

+++ 查看更改日誌

| 發放月 | 更新類型 | 說明 |
|---|---|---|
| 2023 年 4 月 | 文檔更新 | <ul><li>我們更新了 [用例](#use-cases) 部分中提供了一個更清晰的示例，說明客戶何時可以從使用此目標中獲益。</li> <li>我們更新了 [映射](#mapping-considerations-example) 的下界。 的 `Attribute: last_name` 和 `Identity: email` 目標映射是此目標的必需映射。 如果缺少這些映射，則忽略任何其他映射，而不將其發送到 [!DNL Zendesk]。</li> <li>我們更新了 [映射](#mapping-considerations-example) 部分，其中包含強制映射和可選映射的明確示例。</li></ul> |
| 2023 年 3 月 | 首次發行 | 初始目標版本和文檔發佈。 |

{style="table-layout:auto"}

+++