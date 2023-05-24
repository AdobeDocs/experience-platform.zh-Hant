---
title: （測試版）交易台 — CRM連接
description: 將配置檔案激活到您的交易台帳戶，以便根據CRM資料鎖定和禁止受眾。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---

# (Beta) [!DNL Trade Desk] - CRM連接

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] 平台中的目標當前處於beta中。 文檔和功能可能會更改。
>
>隨著EUID（歐洲統一ID）的發佈，您現在看到兩個 [!DNL The Trade Desk - CRM] 目標 [目標目錄](/help/destinations/catalog/overview.md)。
>* 如果您在歐盟中源資料，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目標。
>* 如果您在APAC或NAMER區域中源資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目標。
>
>Experience Platform中的兩個目的地目前都是Beta。 此文檔頁面由 *[!DNL Trade Desk]* 團隊。 有關任何查詢或更新請求，請與 [!DNL Trade Desk] 代表，文檔和功能可能會更改。

## 總覽 {#overview}

此文檔旨在幫助您將配置檔案激活到 [!DNL Trade Desk] 針對基於CRM資料的受眾目標和禁止的帳戶。

[!DNL The Trade Desk(TTD)] 不會隨時直接處理電子郵件地址的上載檔案，也不會 [!DNL The Trade Desk] 儲存原始（未散列）電子郵件。

>[!TIP]
>
>使用 [!DNL The Trade Desk] CRM目標，用於CRM資料映射，如電子郵件或散列電子郵件地址。 使用 [其他交易台目的地](/help/destinations/catalog/advertising/tradedesk.md) 在Adobe Experience Platform目錄的Cookie和設備ID映射中。

## 先決條件 {#prerequisites}

在將段激活到 [!DNL The Trade Desk]您必須聯繫您 [!DNL The Trade Desk] 客戶經理，以簽署CRM登陸合同。 [!DNL The Trade Desk] 然後將授予權限並共用您的廣告商ID以配置您的目標。

## ID匹配要求 {#id-matching-requirements}

根據您在Adobe Experience Platform接收的ID類型，您必須遵守相應的要求。 請閱讀 [Identity Namespace概述](/help/identity-service/namespaces.md) 的子菜單。

## 支援的身份 {#supported-identities}

[!DNL The Trade Desk] 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 按照ID匹配要求部分中的說明，分別為純文字檔案和散列電子郵件地址使用相應的命名空間。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 電子郵件地址（純文字檔案） | 輸入 `email` 當源標識是電子郵件命名空間或屬性時，作為目標標識。 |
| Email_LC_SHA256 | 需要使用SHA256和小寫對電子郵件地址進行散列。 確保遵循任何 [電子郵件規範化](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) 規則為必填項。 您以後將無法更改此設定。 | 輸入 `hashed_email` 當源標識為Email_LC_SHA256命名空間或屬性時，作為目標標識。 |

{style="table-layout:auto"}

## 電子郵件散列要求 {#hashing-requirements}

您可以先對電子郵件地址進行散列，然後再將其插入Adobe Experience Platform或使用原始電子郵件地址。

要瞭解在Experience Platform中插入電子郵件地址的資訊，請閱讀 [批處理接收概述](/help/ingestion/batch-ingestion/overview.md)。

如果您選擇自己對電子郵件地址進行散列，請確保符合以下要求：

* 刪除前導空格和尾隨空格。
* 將所有ASCII字元轉換為小寫。
* 在 `gmail.com` 電子郵件地址中，從電子郵件地址的用戶名部分刪除以下字元：
   * 期間(. （ASCII代碼46）。 例如，規範化 `jane.doe@gmail.com` 至 `janedoe@gmail.com`。
   * 加號(+（ASCII代碼43）)和所有後續字元。 例如，規範化 `janedoe+home@gmail.com` 至 `janedoe@gmail.com`。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中包含在交易台目標中使用的標識符（電子郵件或散列電子郵件）。 |
| 導出頻率 | **[!UICONTROL 每日批]** | 當基於段評估在Experience Platform中更新配置檔案時，將配置檔案（標識）每天更新一次到目標平台下游。 閱讀有關 [批出口](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

### 驗證到目標 {#authenticate}

[!DNL The Trade Desk] CRM目標是每日的批處理檔案上載，不需要用戶進行身份驗證。

### 填寫目標詳細資訊 {#fill-in-details}

在將受眾資料發送或激活到目標之前，必須設定到您自己的目標平台的連接。 同時 [設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 此目標，必須提供以下資訊：

* **[!UICONTROL 帳戶類型]**:請選擇 **[!UICONTROL 現有帳戶]** 的雙曲餘切值。
* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 廣告商ID]**:你 [!DNL Trade Desk Advertiser ID]，您可以共用 [!DNL Trade Desk] 客戶經理或 [!DNL Advertiser Preferences] 的 [!DNL Trade Desk] UI。

![平台UI螢幕快照，顯示如何填寫目標詳細資訊。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

連接到目標時，設定資料治理策略是完全可選的。 請查看Experience Platform [資料治理概述](/help/data-governance/policies/overview.md) 的子菜單。

## 將段激活到此目標 {#activate}

閱讀 [激活受眾資料以批處理配置檔案導出目標](/help/destinations/ui/activate-batch-profile-destinations.md) 有關激活目標受眾段的說明。

在 **[!UICONTROL 計畫]** 頁中，您可以配置要導出的每個段的調度和檔案名。 配置計畫是必需的，但配置檔案名是可選的。

![平台UI螢幕快照，用於安排段激活。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>激活到的所有段 [!DNL The Trade Desk] CRM目標將自動設定為每日頻率和完整檔案導出。

![平台UI螢幕快照，用於安排段激活。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在 **[!UICONTROL 映射]** 頁中，必須從源列中選擇屬性或標識名稱空間並映射到目標列。

![平台UI螢幕快照以映射段激活。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

下面是激活段到時正確標識映射的示例 [!DNL The Trade Desk] CRM目標。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目標不接受原始和散列電子郵件地址作為同一激活流中的標識。 為原始和散列電子郵件地址建立單獨的激活流。

選擇源欄位：

* 選擇 `Email` 命名空間或屬性作為源標識（如果在資料接收時使用原始電子郵件地址）。
* 選擇 `Email_LC_SHA256` 命名空間或屬性作為源標識（如果您將客戶電子郵件地址與資料接收相關）。

選擇目標欄位：

* 輸入  `email` 在源命名空間或屬性時作為目標標識 `Email`。
* 輸入  `hashed_email` 在源命名空間或屬性時作為目標標識 `Email_LC_SHA256`。

## 驗證資料導出 {#validate}

驗證資料是否正確從Experience Platform導出到 [!DNL The Trade Desk]，請在Adobe1PD資料磁貼下查找 [!DNL The Trade Desk] 資料管理平台(DMP)。 下面是查找中相應ID的步驟 [!DNL Trade Desk] UI:

1. 首先，按一下 **[!UICONTROL 資料]** 頁籤，並查看 **[!UICONTROL 第一方]**。
2. 向下滾動頁面，在 **[!UICONTROL 導入的資料]**&#x200B;的 **[!UICONTROL Adobe1PD磁貼]**。
3. 按一下**[!UICONTROL Adobe1PD]**平鋪，並列出所有激活到 [!DNL Trade Desk] 廣告商的目的地。 您還可以使用搜索功能。
4. 來自Experience Platform的段ID #將作為段名稱顯示在 [!DNL Trade Desk] UI。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。
