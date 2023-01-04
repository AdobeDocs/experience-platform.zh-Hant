---
keywords: Experience Platform；首頁；熱門主題；Azure Blob;Azure Blob;Azure Blob連接器
solution: Experience Platform
title: 在UI中建立Azure Blob來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Platform使用者介面建立Azure Blob來源連接器。
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---

# 建立 [!DNL Azure Blob] UI中的源連接

本教學課程提供建立 [!DNL Azure Blob] (下稱「[!DNL Blob]&quot;)使用Platform使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   - [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   - [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL Blob] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/batch/cloud-storage.md).

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部儲存器擷取的下列檔案格式：

- 分隔字元分隔值(DSV):目前，對DSV格式化資料檔案的支援僅限於逗號分隔值。 DSV格式化檔案中欄位標題的值只能由英數字元和下划線組成。 今後將提供對一般DSV檔案的支援。
- JavaScript物件標籤法(JSON):JSON格式化資料檔案必須符合XDM標準。
- 阿帕奇拼花：必須符合XDM規範，才能使用鑲木格式化資料檔案。

### 收集所需憑據

若要存取 [!DNL Blob] 儲存，您必須為下列憑證提供有效值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 包含驗證所需的授權資訊的字串 [!DNL Blob] Experience Platform。 此 [!DNL Blob] 連線字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 如需連線字串的詳細資訊，請參閱 [!DNL Blob] 文檔 [配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | 共用訪問簽名URI，可用作連接您的 [!DNL Blob] 帳戶。 此 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 如需詳細資訊，請參閱 [!DNL Blob] 文檔 [共用訪問簽名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## 連接您的 [!DNL Blob] 帳戶

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Blob] 帳戶至Platform。

在 [平台UI](https://platform.adobe.com)，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以為其建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選擇 **[!UICONTROL Azure Blob儲存]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/blob/catalog.png)

此 **[!UICONTROL 連接到Azure Blob儲存]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Blob] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/blob/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供新的 [!DNL Blob] 帳戶。

**使用連接字串進行身份驗證**

此 [!DNL Blob] 連接器提供您不同的存取驗證類型。 在 [!UICONTROL 帳戶驗證] 選取 **[!UICONTROL ConnectionString]** 使用基於連接字串的憑據。

![連接字串](../../../../images/tutorials/create/blob/connectionstring.png)

**使用共用訪問簽名URI進行身份驗證**

共用訪問簽名(SAS)URI允許向您的 [!DNL Blob] 帳戶。 您可以使用SAS建立具有不同訪問權限的身份驗證憑據，因為基於SAS的身份驗證允許您設定權限、開始日期和到期日，以及對特定資源的調配。

選擇 **[!UICONTROL SasURIAuthentication]** 然後提供 [!DNL Blob] SAS URI。 選擇 **[!UICONTROL 連接到源]** 繼續。

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL Blob] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料從雲儲存帶入平台](../../dataflow/batch/cloud-storage.md).
