---
keywords: Experience Platform；首頁；熱門主題；Salesforce市場營銷雲；Salesforce市場營銷雲
solution: Experience Platform
title: 在UI中建立SalesforceMarketing Cloud源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立SalesforceMarketing Cloud源連接。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 531d5619e0643b6195abaa53d1708e0368d45871
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 建立 [!DNL Salesforce Marketing Cloud] UI中的源連接

>[!NOTE]
>
> 的 [!DNL Salesforce Marketing Cloud] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供建立 [!DNL Salesforce Marketing Cloud] 使用平台用戶介面的源連接器。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果你已經 [!DNL Salesforce Marketing Cloud] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/marketing-automation.md)。

### 收集所需憑據

為了訪問 [!DNL Salesforce Marketing Cloud] 帳戶，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 應用程式的主機伺服器。 這通常是您的子域。 **注：** 輸入 `host` 值，只需指定子域，而不是整個URL。 例如，如果主機URL為 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則只需輸入 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 作為主機值。 |
| `clientId` | 與您的 [!DNL Salesforce Marketing Cloud] 的子菜單。 |
| `clientSecret` | 與您的 [!DNL Salesforce Marketing Cloud] 的子菜單。 |

有關入門的詳細資訊，請參閱此 [[!DNL Salesforce Marketing Cloud] 文檔](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)。

## 連接 [!DNL Salesforce Marketing Cloud] 帳戶

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Salesforce Marketing Cloud] 帳戶到平台。

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 還可以使用搜索欄縮小顯示的連接器。

在 [!UICONTROL 營銷自動化] 類別，選擇 **[!UICONTROL SalesforceMarketing Cloud]** ，然後選擇 **[!UICONTROL 設定]**。

![目錄](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

的 **[!UICONTROL 連接到SalesforceMarketing Cloud]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL Salesforce Marketing Cloud] 憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![新](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL Salesforce Marketing Cloud] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 後續步驟

按照本教程，您已建立到 [!DNL Salesforce Marketing Cloud] 帳戶。 現在，您可以繼續下一個教程， [配置資料流，將營銷自動化系統資料引入平台](../../dataflow/marketing-automation.md)。
