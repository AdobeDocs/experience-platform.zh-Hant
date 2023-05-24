---
keywords: Experience Platform；首頁；熱門主題；hubspot;hubspot
solution: Experience Platform
title: 在UI中建立HubSpot源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立HubSpot源連接。
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# 建立 [!DNL HubSpot] UI中的源連接

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供建立 [!DNL HubSpot] 源連接器使用 [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果你已經 [!DNL HubSpot] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/marketing-automation.md)。

### 收集所需憑據

為了訪問 [!DNL HubSpot] 帳戶 [!DNL Platform]，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的 [!DNL HubSpot] 的子菜單。 |
| `clientSecret` | 與您的 [!DNL HubSpot] 的子菜單。 |
| `accessToken` | 初始驗證OAuth整合時獲取的訪問令牌。 |
| `refreshToken` | 初始驗證OAuth整合時獲取的刷新令牌。 |

有關入門的詳細資訊，請參閱此 [[!DNL HubSpot] 文檔](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

## 連接 [!DNL HubSpot] 帳戶

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL HubSpot] 帳戶 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 營銷自動化]** 類別，選擇 **[!UICONTROL 集線器競價]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 新建 [!DNL HubSpot] 連接器。

![目錄](../../../../images/tutorials/create/hubspot/catalog.png)

的 **[!UICONTROL 連接到HubSpot]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL HubSpot] 憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![連接](../../../../images/tutorials/create/hubspot/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL HubSpot] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/hubspot/existing.png)

## 後續步驟

按照本教程，您已建立到 [!DNL HubSpot] 帳戶。 現在，您可以繼續下一個教程， [配置資料流，將營銷自動化系統資料 [!DNL Platform]](../../dataflow/marketing-automation.md)。
