---
keywords: Experience Platform;home；熱門主題；OData;odata；通用開放資料協定
solution: Experience Platform
title: 在UI中建立通用OData源連接
topic: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立一般開放資料通訊協定來源連線。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---


# 在UI中建立[!DNL Generic OData]源連接

>[!NOTE]
>
> [!DNL Generic OData]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Generic Open Data Protocol]（以下稱為&quot;[!DNL OData]&quot;）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的[!DNL OData]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/protocols.md)的教程

### 收集必要的認證

要訪問[!DNL Platform]中的[!DNL OData]帳戶，必須提供以下值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `url` | [!DNL OData]服務的根URL。 |

有關入門的詳細資訊，請參閱[this [!DNL OData] document](https://www.odata.org/getting-started/basic-tutorial/)。

## 連接您的[!DNL OData]帳戶

收集完所需憑證後，您可以按照以下步驟將[!DNL OData]帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Protocols]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Generic OData]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，選擇「添加資料」(**[!UICONTROL Add data]**)以建立新的[!DNL OData]連接器。

![目錄](../../../../images/tutorials/create/odata/catalog.png)

此時將顯示&#x200B;**[!UICONTROL 連接到通用OData]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新憑據，請選擇&#x200B;**[!UICONTROL 新建帳戶]**。 在出現的輸入表單上，提供連線名稱、選用說明和您的[!DNL OData]認證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/odata/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL OData]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/odata/existing.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL OData]帳戶的連線。 您現在可以繼續下一個教程，並[配置資料流，將協定資料導入 [!DNL Platform]](../../dataflow/protocols.md)。