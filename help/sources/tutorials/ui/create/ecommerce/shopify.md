---
keywords: Experience Platform;home；熱門主題；shopify;Shopify
solution: Experience Platform
title: 在UI中建立Shopify來源連線
topic: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Shopify來源連線。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# 在UI中建立[!DNL Shopify]源連接

>[!NOTE]
>
> [!DNL Shopify]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供使用[!DNL Platform]用戶介面建立[!DNL Shopify]源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有[!DNL Shopify]連接，則可跳過本文檔的其餘部分，並繼續[為電子商務連接器](../../dataflow/ecommerce.md)配置資料流的教程。

### 收集必要的認證

若要存取[!DNL Platform]上的[!DNL Shopify]帳戶，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL Shopify]伺服器的端點。 |
| `accessToken` | 您[!DNL Shopify]使用者帳戶的存取Token。 |

有關快速入門的詳細資訊，請參閱[[!DNL Shopify] document](https://shopify.dev/concepts/about-apis/authentication)。

## 連接您的[!DNL Shopify]帳戶

收集完所需憑證後，您可以按照以下步驟將[!DNL Shopify]帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL eCommerce]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Shopify]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，選擇「添加資料」(**[!UICONTROL Add data]**)以建立新的[!DNL Shopify]連接器。

![目錄](../../../../images/tutorials/create/shopify/catalog.png)

此時將顯示&#x200B;**[!UICONTROL 連接到Shopify]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新憑據，請選擇&#x200B;**[!UICONTROL 新建帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和您的[!DNL Shopify]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/shopify/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL Shopify]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/shopify/existing.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL Shopify]帳戶的連線。 您現在可以繼續下一個教程，並[配置資料流，將電子商務資料導入 [!DNL Platform]](../../dataflow/ecommerce.md)。