---
keywords: Experience Platform；首頁；熱門主題；Google雲端儲存空間；google雲端儲存空間；GCS;gcs
solution: Experience Platform
title: 在UI中建立Google雲端儲存來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Google UI建立Adobe Experience Platform雲端儲存空間來源連線。
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# 建立 [!DNL Google Cloud Storage] UI中的源連接

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供建立 [!DNL Google Cloud Storage] （以下簡稱「GCS」）源連接器 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效的GCS連線，則可略過本檔案的其餘部分，並繼續進行以下的教學課程： [配置資料流](../../dataflow/batch/cloud-storage.md).

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部儲存器擷取的下列檔案格式：

* 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 DSV格式化檔案中欄位標題的值只能由英數字元和下划線組成。 今後將提供對一般DSV檔案的支援。
* JavaScript物件標籤法(JSON):JSON格式化資料檔案必須符合XDM標準。
* 阿帕奇拼花：必須符合XDM規範，才能使用鑲木格式化資料檔案。

### 收集所需憑據

若要在上存取GCS資料 [!DNL Platform]，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 訪問密鑰ID | 61個字元的英數字串，用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。 |
| 秘密訪問密鑰 | 40個字元的base-64編碼字串，用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。 |

如需這些值的詳細資訊，請參閱 [Google雲端儲存HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有關如何生成您自己的訪問密鑰ID和秘密訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md).

## 連接您的 [!DNL Google Cloud Storage] 帳戶

收集到所需憑證後，您可以依照下列步驟將GCS帳戶連結至 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以為其建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL Google雲端儲存空間]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 來建立新的GCS連接器。

![目錄](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此 **[!UICONTROL 連線至Google雲端儲存空間]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、可選說明和您的GCS憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的GCS帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## 後續步驟

依照本教學課程，您已建立與GCS帳戶的連線。 您現在可以繼續下一個教學課程，以及 [配置資料流，將雲儲存中的資料帶入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
