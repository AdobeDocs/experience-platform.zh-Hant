---
keywords: Experience Platform;home；熱門主題；paypal;Paypal
solution: Experience Platform
title: 在UI中建立PayPal來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立PayPal來源連線。
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 在UI中建立[!DNL PayPal]源連接

>[!NOTE]
>
> [!DNL PayPal]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教程提供使用[!DNL Platform]用戶介面建立[!DNL PayPal]源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的[!DNL PayPal]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/payments.md)的教程

### 收集必要的認證

若要存取您的[!DNL PayPal]帳戶[!DNL Platform]，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | [!DNL PayPal]實例的URL。 |
| `clientID` | 與[!DNL PayPal]應用程式相關聯的用戶端ID。 |
| `clientSecret` | 與[!DNL PayPal]應用程式相關聯的用戶端密碼。 |

有關快速入門的詳細資訊，請參閱此[[!DNL PayPal] document](https://developer.paypal.com/docs/api/overview/#get-credentials)

## 連接您的[!DNL PayPal]帳戶

收集完所需憑證後，您可以按照以下步驟將[!DNL PayPal]帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Payments]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL PayPal]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的[!DNL PayPal]連接器。

![目錄](../../../../images/tutorials/create/paypal/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to PayPal]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在顯示的輸入表單上，提供名稱、可選說明和您的[!DNL PayPal]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後允許一些時間建立新連接。

![連接](../../../../images/tutorials/create/paypal/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL PayPal]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/paypal/existing.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL PayPal]帳戶的連線。 您現在可以繼續下一個教程，並[配置資料流以將付款資料導入 [!DNL Platform]](../../dataflow/payments.md)。
