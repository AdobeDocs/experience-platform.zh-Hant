---
keywords: Experience Platform；首頁；熱門主題；Google大查詢；google大查詢；GBQ;gbq
solution: Experience Platform
title: 在UI中建立Google大查詢源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用GoogleUI建立Adobe Experience Platform大查詢源連接。
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 015a4fa06fc2157bb8374228380bb31826add37e
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 建立 [!DNL Google Big Query] UI中的源連接

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供建立 [!DNL Google Big Query] 源連接。

## 快速入門

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL Google BigQuery] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/databases.md)。

### 收集所需憑據

為了訪問 [!DNL Google BigQuery] 帳戶，必須提供以下OAuth 2.0驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `project` | 預設項目ID [!DNL Google BigQuery] 要查詢的項目。 |
| `clientID` | 用於生成刷新令牌的ID值。 |
| `clientSecret` | 用於生成刷新令牌的密鑰值。 |
| `refreshToken` | 從獲取的刷新令牌 [!DNL Google] 用於授權訪問 [!DNL Google BigQuery]。 |

有關這些值的詳細資訊，請參閱 [這個 [!DNL Google BigQuery] 文檔](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)。

## 連接您的GoogleBigQuery帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL 資料庫] 類別，選擇 **[!UICONTROL Google大查詢]** ，然後選擇 **[!UICONTROL 添加資料]**。

![](../../../../images/tutorials/create/google-big-query/catalog.png)

的 **[!UICONTROL 連接到Google大查詢]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL Google BigQuery] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL Google BigQuery] 憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![](../../../../images/tutorials/create/google-big-query/new.png)

## 後續步驟

按照本教程，您已建立到 [!DNL Google BigQuery] 帳戶。 現在，您可以繼續下一個教程， [配置資料流以將資料引入平台](../../dataflow/databases.md)。
