---
title: SalesforceMarketing Cloud客戶項目
description: 瞭解如何使用SalesforceMarketing Cloud客戶項目（以前稱為Pardot）目標導出帳戶資料，並在SalesforceMarketing Cloud客戶項目中根據您的業務需要將其激活。
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: 86feee5981aaa81d4c1f97ff8aaf303b2aacd977
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] 連接

使用 [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(前稱 [!DNL Pardot])* 目標以捕獲、跟蹤、得分和評級線索。 您還可以通過電子郵件滴注式市場活動和具有培養、評分和市場活動細分的銷售線索管理，為目標市場細分和客戶群設計銷售線索渠道的所有階段。

與 [!DNL Salesforce Marketing Cloud Engagement] 更傾向於 **B2C** 營銷， [!DNL Marketing Cloud Account Engagement] 是 **B2B** 使用涉及多個部門和決策者的案例，這些案例需要更長的銷售和決策週期。 此外，您還可以保持與CRM的更接近和整合，以做出適當的銷售和營銷決策。 *注意，Experience Platform還具有 [!DNL Salesforce Marketing Cloud Engagement]你可以查查 [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 和 [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 頁。*

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) 端點，到 **添加或更新您的銷售線索** 在新內激活它們後 [!DNL Marketing Cloud Account Engagement] 段。

[!DNL Marketing Cloud Account Engagement] 使用OAuth 2和授權碼協定對 [!DNL Account Engagement] API。 驗證到您 [!DNL Marketing Cloud Account Engagement] 下面是實例， [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 [!DNL Marketing Cloud Account Engagement] 目的地，這裡是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 將電子郵件發送到營銷活動的聯繫人 {#use-case-send-emails}

一個線上平台的營銷部門希望向策劃的B2B銷售線索的受眾廣播基於電子郵件的營銷活動。 該平台的營銷團隊可以通過Adobe Experience Platform添加新的銷售線索或更新現有的銷售線索資訊，從他們自己的離線資料構建銷售線索段，並將這些線索段發送到 [!DNL Marketing Cloud Account Engagement]，然後可用於發送營銷活動電子郵件。

## 先決條件 {#prerequisites}

有關在Experience Platform和 [!DNL Salesforce] 以及在使用之前需要收集的資訊 [!DNL Marketing Cloud Account Engagement] 目標。

### Experience Platform中的先決條件 {#prerequisites-in-experience-platform}

在將資料激活到 [!DNL Marketing Cloud Account Engagement] 目標，您必須 [架構](/help/xdm/schema/composition.md)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。

### 中的先決條件 [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

請注意以下先決條件，以便將資料從平台導出到 [!DNL Marketing Cloud Account Engagement] 帳戶：

#### 你需要 [!DNL Marketing Cloud Account Engagement] 帳戶 {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] 具有訂閱的帳戶 [Marketing Cloud客戶項目](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 產品必須繼續。

您 [!DNL Salesforce] 帳戶應具有 [!DNL Salesforce] `Account Engagement Administrator role`。 這是 [建立自定義目標欄位](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5)。

最後，您的帳戶還應能夠訪問 [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5)。

伸向 [[!DNL Salesforce] 支援](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 或 [!DNL Salesforce] 帳戶管理員（如果您沒有帳戶或帳戶丟失） [!DNL Marketing Cloud Account Engagement] 訂閱或 [!DNL Account Engagement Administrator role]。

#### 收集 [!DNL Marketing Cloud Account Engagement] 憑據 {#gather-credentials}

在驗證到 [!DNL Marketing Cloud Account Engagement] 目標。

| 憑據 | 說明 |
| --- | --- |
| `Username` | 您 [!DNL Marketing Cloud Account Engagement] 帳戶用戶名。 |
| `Password` | 您 [!DNL Marketing Cloud Account Engagement] 帳戶密碼。 |
| `Account Engagement Business Unit ID` | 要查找帳戶訂約業務單元ID，請使用中的「設定」 [!DNL Salesforce]。 在設定中，輸入 *業務單位設定* 的上界。 您的客戶項目業務單元ID以開頭 `0Uv` 長18個字元。 如果無法訪問業務部門設定資訊，請咨詢 [!DNL Salesforce] 帳戶管理員為您提供 `Account Engagement Business Unit ID`。 如果您需要任何其他指導，請參閱 [[!DNL Salesforce] 驗證](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) 指南。 |

{style="table-layout:auto"}

### 護欄 {#guardrails}

請參閱 [!DNL Marketing Cloud Account Engagement] [速率限制](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) 詳細列出您的計畫所施加的限制，並且也適用於Experience Platform處決。

>[!IMPORTANT]
>
>如果 [!DNL Salesforce] 帳戶管理員對受信任的IP範圍有限制的訪問權限，您需要聯繫他們以獲取 [Experience PlatformIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 已列出。 請參閱 [!DNL Salesforce] [限制對已連接應用的受信任IP範圍的訪問](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文檔。

## 支援的身份 {#supported-identities}

[!DNL Marketing Cloud Account Engagement] 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 潛在客戶電子郵件地址 | 必要 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | <ul><li>您正在導出段的所有成員以及所需的架構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位映射。</li><li> 對於平台中的每個選定段， [!DNL Salesforce Marketing Cloud Account Engagement] 段狀態將從平台更新為其段狀態。</li></ul> |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

在 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]**，搜索 [!DNL Salesforce Marketing Cloud Account Engagement]。 或者，可將其定位在 **[!UICONTROL 電子郵件營銷]** 的子菜單。

### 驗證到目標 {#authenticate}

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**。 將導航到 [!DNL Salesforce] 登錄頁。 輸入 [!DNL Marketing Cloud Account Engagement] 帳戶憑據，選擇 [!DNL Log In]。

![平台UI螢幕快照，顯示如何驗證到Marketing Cloud帳戶項目。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

下一步，選擇 [!UICONTROL 允許] 在後續窗口中授予 **Adobe Experience Platform** 訪問你的應用 [!DNL Salesforce Marketing Cloud Account Engagement] 帳戶。 *您只需執行一次*。

![Salesforce App螢幕截圖確認彈出菜單，用於授予Experience Platform應用對Marketing Cloud帳戶項目的訪問權限。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

如果提供的詳細資訊有效，UI將顯示一條消息： *您已成功連接到SalesforceMarketing Cloud帳戶約定帳戶* 和 **[!UICONTROL 已連接]** 狀態為綠色複選標籤，然後可以繼續執行下一步。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。 請參閱 [收集 [!DNL Marketing Cloud Account Engagement] 憑據](#gather-credentials) 的雙曲餘切值。

![顯示目標詳細資訊的平台UI螢幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 欄位 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 您將來識別此目標的名稱。 |
| **[!UICONTROL 說明]** | 將幫助您在將來確定此目標的說明。 |
| **[!UICONTROL 客戶項目業務單元ID]** | 您 [!DNL Salesforce] `Account Engagement Business Unit ID`。 |

{style="table-layout:auto"}

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
>
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射注意事項和示例 {#mapping-considerations-example}

正確將您的受眾資料從Adobe Experience Platform發送到 [!DNL Marketing Cloud Account Engagement] 目標，您需要完成欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。

正確將XDM欄位映射到 [!DNL Marketing Cloud Account Engagement] 目標欄位，請執行以下步驟。

1. 在 **[!UICONTROL 映射]** 步驟，選擇 **[!UICONTROL 添加新映射]**。 螢幕上將顯示新的映射行。
1. 在 **[!UICONTROL 選擇源欄位]** ，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選擇XDM屬性或 **[!UICONTROL 選擇標識命名空間]** 並選擇標識。
1. 在 **[!UICONTROL 選擇目標欄位]** ，選擇 **[!UICONTROL 選擇標識命名空間]** 選擇標識或 **[!UICONTROL 選擇自定義屬性]** 類別，並從清單中指定 [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) 從可用架構中。

   * 重複這些步驟，在XDM配置檔案架構和 [!DNL Marketing Cloud Account Engagement]: |源欄位 |目標欄位 |強制 | | - | - | - | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * 下面顯示了具有上述映射的示例：
      ![平台UI螢幕快照示例，顯示目標映射。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

完成為目標連接提供映射後，選擇 **[!UICONTROL 下一個]**。

## 驗證資料導出 {#exported-data}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 導航到所選段之一。 選取 **[!DNL Activation data]** 索引標籤。的 **[!UICONTROL 映射ID]** 列顯示在 [!DNL Marketing Cloud Account Engagement Prospects] 的子菜單。
   ![平台UI螢幕快照示例，顯示選定段的映射ID。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. 登錄到 [[!DNL Salesforce]](https://login.salesforce.com/) 的子菜單。 然後導航到 **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** 並檢查是否已添加/更新該段中的潛在客戶。 此外，您還可以 [[!DNL Salesforce Pardot]](https://pi.pardot.com/) 並訪問 **[!DNL Prospects]** 的子菜單。
   ![顯示「潛在客戶」頁的Salesforce UI螢幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 要檢查潛在客戶是否已更新，請選擇一個目標客戶並驗證自定義目標客戶欄位是否已更新為Experience Platform段狀態。
   ![顯示選定目標客戶頁的Salesforce UI螢幕快照，將使用段狀態更新自定義目標客戶欄位。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API文檔](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)。
