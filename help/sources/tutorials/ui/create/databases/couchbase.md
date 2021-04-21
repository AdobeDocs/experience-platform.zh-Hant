---
keywords: Experience Platform；首頁；熱門主題；Couchbase;couchbase
solution: Experience Platform
title: 在UI中建立Couchbase來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Couchbase來源連線。
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 在UI中建立[!DNL Couchbase]源連接

>[!NOTE]
>
> [!DNL Couchbase]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

[!DNL Adobe Experience Platform]中的源連接器提供按計畫接收外部源資料的能力。 本教程提供使用[!DNL Platform]用戶介面建立[!DNL Couchbase]源連接器的步驟。

## 快速入門

本教學課程需要對[!DNL Platform]的下列元件有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的[!DNL Couchbase]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/databases.md)的教程。

### 收集必要的認證

要驗證[!DNL Couchbase]源連接器，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到[!DNL Couchbase]實例的連接字串。 [!DNL Couchbase]的連接字串模式是`Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`。 有關獲取連接字串的詳細資訊，請參閱[[!DNL Couchbase] connection](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)上的文檔。 |

## 連接您的[!DNL Couchbase]帳戶

收集完所需憑證後，您可以按照以下步驟將[!DNL Couchbase]帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Couchbase]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的[!DNL Couchbase]連接器。

![目錄](../../../../images/tutorials/create/couchbase/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to Couchbase]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在顯示的輸入表單上，提供名稱、可選說明和您的[!DNL Couchbase]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect to source]** ，然後允許一些時間建立新連接。

![連接](../../../../images/tutorials/create/couchbase/new.png)

### 現有帳戶

若要連接現有帳戶，請選擇您要連接的[!DNL Couchbase]帳戶，然後選擇右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/couchbase/existing.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL Couchbase]帳戶的連線。 現在，您可以繼續下一個教程，並[配置資料流以將資料導入 [!DNL Platform]](../../dataflow/databases.md)。
