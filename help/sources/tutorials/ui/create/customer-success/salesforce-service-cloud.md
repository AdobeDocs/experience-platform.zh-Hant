---
keywords: Experience Platform；首頁；熱門主題；Salesforce服務雲；salesforce服務雲
solution: Experience Platform
title: 在UI中建立Salesforce服務雲源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Salesforce服務雲源連接。
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# 建立 [!DNL Salesforce Service Cloud] UI中的源連接

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供建立 [!DNL Salesforce Service Cloud] （下稱「SSC」）源連接器 [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有有效的SSC連接，則可以跳過本文檔的其餘部分並繼續上的教程 [配置資料流](../../dataflow/customer-success.md)

### 收集所需憑據

為了訪問您的SSC帳戶 [!DNL Platform]，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `username` | 用戶帳戶的用戶名。 |
| `password` | 用戶帳戶的密碼。 |
| `securityToken` | 用戶帳戶的安全令牌。 |

有關入門的詳細資訊，請參閱 [這個 [!DNL Salesforce Service Cloud] 文檔](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

## 連接 [!DNL Salesforce Service Cloud] 帳戶

收集所需憑據後，您可以按照以下步驟將SSC帳戶連結至 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 客戶成功]** 類別，選擇 **[!UICONTROL Salesforce服務雲]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 建立新的SSC連接器。

![目錄](../../../../images/tutorials/create/ssc/catalog.png)

的 **[!UICONTROL 連接到Salesforce服務雲]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單中，提供名稱、可選說明和SSC憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![連接](../../../../images/tutorials/create/ssc/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的SSC帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/ssc/existing.png)

## 後續步驟

按照本教程，您已建立到SSC帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流以將客戶成功資料 [!DNL Platform]](../../dataflow/customer-success.md)。
