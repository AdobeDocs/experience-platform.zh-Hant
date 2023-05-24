---
keywords: linkedin連接；linkedin連接；linkedin連接；linkedin目標；linkedin
title: Linkedin匹配的受眾連接
description: 根據經過散列的電子郵件激活LinkedIn市場活動的配置檔案，以針對受眾進行目標、個性化和壓制。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences] 連接

## 總覽 {#overview}

激活您的配置檔案 [!DNL LinkedIn] 針對受眾目標、個性化和壓制的營銷活動，基於經過散列的電子郵件和移動ID。

![linkedIn目的地：Adobe Experience PlatformUI](../../assets/catalog/social/linkedin/catalog.png)

## 使用案例

幫助您更好地瞭解如何和何時使用 [!DNL LinkedIn Matched Audiences] destination ，這是Adobe Experience Platform客戶可以使用此功能解決的使用案例。

一家軟體公司組織一個會議，希望與參與者保持聯繫，並根據他們的會議出席情況向他們展示個性化的服務。 公司可以從自己的地址中接收電子郵件地址或移動設備ID [!DNL CRM] 進入Adobe Experience Platform。 然後，他們可以從自己的離線資料構建資料段，並將這些資料段發送到 [!DNL LinkedIn] 社交平台，優化廣告支出。

## 支援的身份 {#supported-identities}

[!DNL LinkedIn Matched Audiences] 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | Apple廣告商ID | 當源標識為IDFA命名空間時，選擇此目標標識。 |
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 文本和散列電子郵件分別使用相應的命名空間。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中使用的標識符（名稱、電話號碼和其他） [!DNL LinkedIn Matched Audiences] 目標。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## linkedIn帳戶先決條件 {#LinkedIn-account-prerequisites}

在使用 [!UICONTROL linkedIn對陣觀眾] 目標，確保 [!DNL LinkedIn Campaign Manager] 帳戶 [!DNL Creative Manager] 權限級別或更高。

瞭解如何編輯 [!DNL LinkedIn Campaign Manager] 用戶權限，請參閱 [添加、編輯和刪除廣告帳戶上的用戶權限](https://www.linkedin.com/help/lms/answer/5753) 在LinkedIn檔案里。

## ID匹配要求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 要求未清除發送個人身份資訊(PII)。 因此，觀眾被激活 [!DNL LinkedIn Matched Audiences] 可以鎖住 *散* 標識符，如電子郵件地址或移動設備ID。

根據您在Adobe Experience Platform接收的ID類型，您必須遵守其相應要求。

## 電子郵件散列要求 {#email-hashing-requirements}

您可以在將電子郵件地址插入Adobe Experience Platform之前對它們進行散列，或在Experience Platform中使用明確的電子郵件地址，並且 [!DNL Platform] 在激活時對它們進行散列。

要瞭解在Experience Platform中插入電子郵件地址的資訊，請參閱 [批處理接收概述](/help/ingestion/batch-ingestion/overview.md) 和 [流式處理概述](/help/ingestion/streaming-ingestion/overview.md)。

如果您選擇自己對電子郵件地址進行散列，請確保符合以下要求：

* 從電子郵件字串中裁切所有前導空格和尾隨空格。 例如： `johndoe@example.com`不 `<space>johndoe@example.com<space>`;
* 散列電子郵件字串時，確保散列小寫字串；
   * 示例： `example@email.com`不 `EXAMPLE@EMAIL.COM`;
* 確保散列字串全部為小寫
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`不 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 別用鹽把繩子撒了。

>[!NOTE]
>
>來自未哈希命名空間的資料自動哈希由 [!DNL Platform] 激活後。
> 屬性源資料不會自動散列。
> 
> 在 [標識映射](../../ui/activate-segment-streaming-destinations.md#mapping) 步驟，當源欄位包含未散列屬性時，檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。
> 
> 的 **[!UICONTROL 應用轉換]** 選項。 選擇命名空間時不顯示它。

![身份映射轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

下面的視頻還演示了配置 [!DNL LinkedIn Matched Audiences] 目標和激活段。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform用戶介面頻繁更新，自此視頻記錄後可能已更改。 有關最新資訊，請參閱 [目標配置教程](../../ui/connect-destination.md)。

### 驗證到目標 {#authenticate}

1. 查找 [!DNL LinkedIn Matched Audiences] 目標目錄中的目標，然後選擇 **[!UICONTROL 設定]**。
2. 選擇 **[!UICONTROL 連接到目標]**。
   ![驗證到LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. 輸入您的LinkedIn憑據並選擇 **登錄**。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="帳戶 ID"
>abstract="您的 LinkedIn 行銷活動管理員帳戶 ID。您可以在您的 LinkedIn 行銷活動管理員帳戶中找到此 ID。"

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 帳戶ID]**:您 [!DNL LinkedIn Campaign Manager Account ID]。 您可以在 [!DNL LinkedIn Campaign Manager] 帳戶。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到流段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

成功激活表示 [!DNL LinkedIn] 自定義訪問群體將以寫程式方式在 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)。 當用戶符合激活的段的條件或取消其資格時，將添加和刪除在受眾中的段成員資格。

>[!TIP]
>
>Adobe Experience Platform與 [!DNL LinkedIn Matched Audiences] 支援歷史受眾回填。 所有歷史段資格均發送至 [!DNL LinkedIn] 將段激活到目標。
