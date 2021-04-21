---
keywords: Experience Platform；首頁；熱門主題；Azure Blob;azure blob;Azure blob連接器
solution: Experience Platform
title: 在UI中建立Azure Blob來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用平台使用者介面建立Azure Blob來源連接器。
exl-id: 0e54569b-7305-4065-981e-951623717648
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# 在UI中建立[!DNL Azure Blob]來源連線

本教學課程提供使用平台使用者介面建立[!DNL Azure Blob]（以下稱為「[!DNL Blob]」）的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的[!DNL Blob]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部儲存中提取的以下檔案格式：

- 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 DSV格式檔案中欄位標題的值只能由字母數字字元和下划線組成。 將來將提供對一般DSV檔案的支援。
- JavaScript物件符號(JSON):JSON格式的資料檔案必須符合XDM規範。
- Apache Parce:拼花格式化的資料檔案必須與XDM相容。

### 收集必要的認證

要訪問平台上的[!DNL Blob]儲存，必須為以下憑據提供有效值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 包含驗證[!DNL Blob]到Experience Platform所需的授權資訊的字串。 [!DNL Blob]連接字串模式是：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 有關連接字串的詳細資訊，請參閱[配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)上的[!DNL Blob]文檔。 |
| `sasUri` | 共用訪問簽名URI，可用作連接[!DNL Blob]帳戶的替代驗證類型。 [!DNL Blob] SAS URI模式為：`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`如需詳細資訊，請參閱[共用存取簽名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)上的此[!DNL Blob]檔案。 |

## 連接您的[!DNL Blob]帳戶

收集完所需憑證後，您可依照下列步驟將[!DNL Blob]帳戶連結至平台。

在[平台UI](https://platform.adobe.com)中，從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL Catalog]畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列，找到您要使用的特定來源。

在[!UICONTROL Cloud storage]類別下，選擇&#x200B;**[!UICONTROL Azure Blob Storage]**，然後選擇&#x200B;**[!UICONTROL Add data]**。

![目錄](../../../../images/tutorials/create/blob/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to Azure Blob Storage]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 現有帳戶

要使用現有帳戶，請選擇要建立新資料流的[!DNL Blob]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/blob/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇&#x200B;**[!UICONTROL New account]**，然後為新[!DNL Blob]帳戶提供名稱和選項說明。

**使用連接字串進行驗證**

[!DNL Blob]連接器為您提供不同的訪問驗證類型。 在[!UICONTROL Account authentication]下，選擇&#x200B;**[!UICONTROL ConnectionString]**&#x200B;以使用基於連接字串的憑據。

![連接字串](../../../../images/tutorials/create/blob/connectionstring.png)

**使用共用訪問簽名URI進行驗證**

共用訪問簽名(SAS)URI允許對[!DNL Blob]帳戶進行安全委託授權。 您可以使用SAS來建立具有不同存取度的驗證憑證，因為以SAS為基礎的驗證可讓您設定權限、開始和到期日，以及特定資源的規定。

選擇&#x200B;**[!UICONTROL SasURIAuthentication]**，然後提供[!DNL Blob] SAS URI。 選擇&#x200B;**[!UICONTROL Connect to source]**&#x200B;繼續。

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL Blob]帳戶的連線。 您現在可以繼續下一個教學課程，並[設定資料流，將雲端儲存空間的資料匯入Platform](../../dataflow/batch/cloud-storage.md)。
