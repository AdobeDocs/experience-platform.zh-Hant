---
title: 通過UI將SalesforceMarketing Cloud帳戶連接到Experience Platform
description: 瞭解如何通過UI將SalesforceMarketing Cloud帳戶連接到Experience Platform。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 1%

---

# 連接 [!DNL Salesforce Marketing Cloud] 要通過UIExperience Platform的帳戶

>[!IMPORTANT]
>
>當前不支援自定義對象攝取 [!DNL Salesforce Marketing Cloud] 源整合。


本教程提供了如何連接 [!DNL Salesforce Marketing Cloud] 通過UI向Adobe Experience Platform發送帳戶。

## 快速入門

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果你已經 [!DNL Salesforce Marketing Cloud] 帳戶，您可以跳過本文檔的其餘部分，繼續學習本教程。 [使用UI將營銷自動化資料帶到Experience Platform](../../dataflow/marketing-automation.md)。

### 收集所需憑據

為了訪問 [!DNL Salesforce Marketing Cloud] 帳戶，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| Host | 應用程式的主機伺服器。 這通常是您的子域。 **注：** 輸入 `host` 值，只需指定子域，而不是整個URL。 例如，如果主機URL為 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則只需輸入 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 作為主機值。 |
| 客戶端ID | 與您的 [!DNL Salesforce Marketing Cloud] 的子菜單。 |
| 客戶端密碼 | 與您的 [!DNL Salesforce Marketing Cloud] 的子菜單。 |

有關身份驗證的詳細資訊 [!DNL Salesforce Marketing Cloud]，訪問 [[!DNL Salesforce] 驗證文檔](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)。

## 連接 [!DNL Salesforce Marketing Cloud] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 顯示Experience Platform支援的各種源。

可以從類別清單中選擇相應的類別。 也可以使用搜索欄篩選特定源。

在 [!UICONTROL 營銷自動化] 類別，選擇 **[!UICONTROL SalesforceMarketing Cloud]** ，然後選擇 **[!UICONTROL 設定]**。

![已選擇SalesforceMarketing Cloud源的源目錄。](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

的 **[!UICONTROL 連接到SalesforceMarketing Cloud]** 的子菜單。 在此頁上，您可以建立新帳戶或使用現有帳戶。

### 新帳戶

要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]** 並提供帳戶的名稱、可選說明以及與您的帳戶對應的身份驗證憑據 [!DNL Salesforce Marketing Cloud] 帳戶。

完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![新帳戶介面，您可以在該介面中驗證SalesforceMarketing Cloud的新帳戶。](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 現有帳戶

如果已有現有帳戶，請選擇 **[!UICONTROL 現有帳戶]** 然後，從顯示的清單中選擇要使用的帳戶。

![現有帳戶介面，您可以從現有SalesforceMarketing Cloud帳戶清單中進行選擇。](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 後續步驟

按照本教程，您已在 [!DNL Salesforce Marketing Cloud] 帳戶和Experience Platform。 現在，您可以繼續下一個教程， [建立資料流，將營銷自動化資料引入Experience Platform](../../dataflow/marketing-automation.md)。
