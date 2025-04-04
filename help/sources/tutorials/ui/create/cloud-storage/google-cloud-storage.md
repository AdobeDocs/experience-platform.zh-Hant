---
title: 在UI中建立Google雲端儲存空間Source連線
description: 瞭解如何使用Google UI建立Adobe Experience Platform雲端儲存空間來源連線。
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---

# 在使用者介面中建立[!DNL Google Cloud Storage]來源連線

本教學課程提供使用Adobe Experience Platform UI建立[!DNL Google Cloud Storage]來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Google Cloud Storage]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/batch/cloud-storage.md)的教學課程。

### 支援的檔案格式

[!DNL Experience Platform]支援從外部儲存區擷取的下列檔案格式：

* 分隔符號分隔值(DSV)：任何單一字元值都可以當作DSV格式資料檔案的分隔符號。
* JavaScript物件標籤法(JSON)： JSON格式資料檔案必須符合XDM。
* Apache Parquet： Parquet格式的資料檔案必須符合XDM標準。

### 收集必要的認證

若要在Experience Platform上存取您的[!DNL Google Cloud Storage]資料，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| 存取金鑰 ID | 61個字元的英數字串，用於向Experience Platform驗證您的[!DNL Google Cloud Storage]帳戶。 |
| 祕密存取金鑰 | 用於向Experience Platform驗證您的[!DNL Google Cloud Storage]帳戶的40個字元Base-64編碼字串。 |
| 貯體名稱 | 您的[!DNL Google Cloud Storage]儲存貯體的名稱。 如果您想要提供雲端儲存空間中特定子資料夾的存取權，您必須指定儲存貯體名稱。 |
| 檔案夾路徑 | 您要提供存取權的資料夾路徑。 |

如需這些值的詳細資訊，請參閱[Google雲端儲存空間HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 如需如何產生您自己的存取金鑰ID和秘密存取金鑰的步驟，請參閱[[!DNL Google Cloud Storage] 概觀](../../../../connectors/cloud-storage/google-cloud-storage.md)。

收集必要的認證後，您可以依照下列步驟將[!DNL Google Cloud Storage]帳戶連結至Experience Platform。

## 連線您的[!DNL Google Cloud Storage]帳戶

在Experience Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL 雲端儲存空間]類別下，選取&#x200B;**[!UICONTROL Google雲端儲存空間]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![顯示來源目錄頁面的Experience Platform UI畫面。](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

**[!UICONTROL 連線至Google雲端儲存空間]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL Google Cloud Storage]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![Experience Platform UI畫面顯示Google雲端儲存空間來源的現有帳戶頁面](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL Google Cloud Storage]認證。 在此步驟中，您還可以定義子資料夾的路徑名稱，以指定您的帳戶將可以存取的子資料夾。

完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![Experience Platform UI畫面顯示Google雲端儲存空間來源的新帳戶頁面。](../../../../images/tutorials/create/google-cloud-storage/new.png)


## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Google Cloud Storage]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，將您的雲端儲存空間中的資料匯入Experience Platform](../../dataflow/batch/cloud-storage.md)。
