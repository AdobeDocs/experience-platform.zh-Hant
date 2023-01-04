---
keywords: Experience Platform；首頁；熱門主題；方塊；方塊
title: 在UI中建立方形來源連線
description: 了解如何使用Adobe Experience Platform UI建立方形來源連線。
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# 建立 [!DNL Square] UI中的源連接

本教學課程提供建立 [!DNL Square] 來源連接器。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

### 收集所需憑據

若要存取 [!DNL Square] 帳戶平台，您必須提供下列值：

| 憑據 | 說明 |
| --- | --- |
| Host | 的URL [!DNL Square] 例項。 |
| 用戶端ID | 與您的 [!DNL Square] 帳戶。 |
| 用戶端密碼 | 與您的 [!DNL Square] 帳戶。 |
| 存取權杖 | 存取權杖可用來驗證您的 [!DNL Square] 帳戶（驗證OAuth 2.0）。 存取權杖可從 [!DNL Square]. |
| 重新整理Token | 當您目前的存取權杖過期時，會使用重新整理權杖來產生新的存取權杖。 可從取得重新整理代號 [!DNL Square]. |

如需這些憑證以及如何取得的詳細資訊，請參閱 [[!DNL Square] OAuth相關檔案](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Square] 帳戶至Platform。

## 連接您的 [!DNL Square] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL 付款] 類別，選擇 **[!UICONTROL 方]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/square/catalog.png)

此 **[!UICONTROL 連接到Square]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Square] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/square/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明和您的 [!DNL Square] 憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/square/new.png)

## 後續步驟

依照本教學課程，您已驗證並建立來源連線，連線位於 [!DNL Square] 帳戶和平台。 您現在可以繼續下一個教學課程，以及 [建立資料流，將支付資料導入Platform](../../dataflow/payments.md).
