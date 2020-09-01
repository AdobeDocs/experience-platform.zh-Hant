---
keywords: Experience Platform;home;popular topics;ServiceNow;servicenow
solution: Experience Platform
title: 在UI中建立ServiceNow來源連接器
topic: overview
description: 本教學課程提供使用平台使用者介面建立ServiceNow來源連接器的步驟。
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---


# 在UI中 [!DNL ServiceNow] 建立來源連接器

>[!NOTE]
>
>連接 [!DNL ServiceNow] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使用者介 [!DNL ServiceNow] 面建立來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model] (XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL即時客戶基本資料]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的 [!DNL ServiceNow] 連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/customer-success.md)

### 收集必要的認證

若要存取您的帳 [!DNL ServiceNow] 戶， [!DNL Platform]您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL ServiceNow] server. |
| `username` | 用於連接到伺服器以進行驗 [!DNL ServiceNow] 證的用戶名。 |
| `password` | 連線至伺服器以進行驗 [!DNL ServiceNow] 證的密碼。 |

如需快速入門的詳細資訊，請參閱本 [ [!DNL ServiceNow] 檔案](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

## 連線您的帳 [!DNL ServiceNow] 戶

收集完所需的認證後，您可依照下列步驟將帳戶連結 [!DNL ServiceNow] 至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「客戶 **[!UICONTROL 成功]** 」類別下，選 **[!UICONTROL 擇ServiceNow]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 擇「連接源]** 」(Connect source [!DNL ServiceNow] )以建立新連接器。

![](../../../../images/tutorials/create/servicenow/catalog.png)

此時 **[!UICONTROL 將顯示「連接到ServiceNow]** 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明和您的認 [!DNL ServiceNow] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![](../../../../images/tutorials/create/servicenow/new.png)

### 現有帳戶

若要連線現有帳戶，請選 [!DNL ServiceNow] 取您要連線的帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![](../../../../images/tutorials/create/servicenow/existing.png)

## 後續步驟

遵循本教學課程，您已建立與帳戶的 [!DNL ServiceNow] 連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入 [!DNL Platform]](../../dataflow/customer-success.md)。
