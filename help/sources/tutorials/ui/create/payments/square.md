---
keywords: Experience Platform；首頁；熱門主題；方塊；方形
title: 在UI中建立方形源連接
description: 瞭解如何使用Adobe Experience PlatformUI建立方形源連接。
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# 建立 [!DNL Square] UI中的源連接

本教程提供建立 [!DNL Square] 使用平台用戶介面的源連接器。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

### 收集所需憑據

為了訪問 [!DNL Square] 帳戶平台，必須提供以下值：

| 憑據 | 說明 |
| --- | --- |
| Host | 的URL [!DNL Square] 實例。 |
| 客戶端ID | 與您的 [!DNL Square] 帳戶。 |
| 客戶端密碼 | 與您的 [!DNL Square] 帳戶。 |
| 訪問令牌 | 訪問令牌用於驗證 [!DNL Square] OAuth 2.0身份驗證的帳戶。 可以從 [!DNL Square]。 |
| 刷新標籤 | 刷新令牌用於在當前訪問令牌過期後生成新訪問令牌。 可從中獲取刷新令牌 [!DNL Square]。 |

有關這些憑據以及如何獲取這些憑據的詳細資訊，請參見 [[!DNL Square] OAuth文檔](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens)。

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Square] 帳戶到平台。

## 連接 [!DNL Square] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 [!UICONTROL 付款] 類別，選擇 **[!UICONTROL 方塊]**，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/square/catalog.png)

的 **[!UICONTROL 連接到正方形]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL Square] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/square/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後為您提供名稱、可選說明和相應的值 [!DNL Square] 憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![新](../../../../images/tutorials/create/square/new.png)

## 後續步驟

按照本教程，您已經驗證並建立了源連接 [!DNL Square] 帳戶和平台。 現在，您可以繼續下一個教程， [建立資料流，將付款資料引入平台](../../dataflow/payments.md)。
