---
title: 在使用者介面中建立Azure Blob Source連線
description: 瞭解如何使用Experience Platform使用者介面建立Azure Blob來源聯結器。
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL Azure Blob]來源連線

本教學課程提供使用Experience Platform使用者介面建立[!DNL Azure Blob] （以下稱為「[!DNL Blob]」）來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：在Experience Platform中組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Blob]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/batch/cloud-storage.md)的教學課程。

### 支援的檔案格式

Experience Platform支援從外部儲存擷取下列檔案格式：

* 分隔符號分隔值(DSV)：您可以使用任何單一欄分隔符號（例如Tab、逗號、垂直號、分號或雜湊）來收集任何格式的平面檔案。
* JavaScript物件標籤法(JSON)： JSON格式資料檔案必須符合XDM。
* Apache Parquet： Parquet格式的資料檔案必須符合XDM標準。

### 收集必要的認證

若要在Experience Platform上存取您的[!DNL Blob]儲存空間，您必須提供下列認證的有效值：

>[!BEGINTABS]

>[!TAB 連線字串驗證]

| 認證 | 說明 |
| --- | --- |
| 連接字串 | 字串，其中包含驗證[!DNL Blob]給Experience Platform所需的授權資訊。 [!DNL Blob]連線字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 如需有關連線字串的詳細資訊，請參閱[設定連線字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)上的此[!DNL Blob]檔案。 |

>[!TAB SAS URI驗證]

| 認證 | 說明 |
| --- | --- |
| SAS URI | 共用存取簽章URI，可做為連線您的[!DNL Blob]帳戶的替代驗證型別。 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`如需詳細資訊，請參閱[共用存取簽章URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)上的此[!DNL Blob]檔案。 |
| 容器 | 您要指定存取權的容器名稱。 使用[!DNL Blob]來源建立新帳戶時，您可以提供容器名稱，以指定使用者對您所選子資料夾的存取權。 |
| 檔案夾路徑 | 您要提供存取權的資料夾路徑。 |

>[!ENDTABS]

收集必要的認證後，您可以依照下列步驟，將[!DNL Blob]儲存空間連線至Experience Platform

## 連線您的[!DNL Blob]帳戶

在Experience Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL 雲端儲存空間]類別下，選取&#x200B;**[!UICONTROL Azure Blob儲存空間]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![已選取Azure Blob儲存體來源的Experience Platform來源目錄。](../../../../images/tutorials/create/blob/catalog.png)

**[!UICONTROL 連線到Azure Blob儲存體]**&#x200B;頁面就會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL Blob]帳戶，然後選取[下一步] ]**以繼續。**[!UICONTROL 

![現有](../../../../images/tutorials/create/blob/existing.png)

### 新帳戶

>[!TIP]
>
>建立後，您無法變更[!DNL Blob]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後為您新的[!DNL Blob]帳戶提供名稱和選擇性說明。

![Azure Blob儲存來源的新帳戶畫面。](../../../../images/tutorials/create/blob/new.png)

[!DNL Blob]來源同時支援帳戶金鑰驗證和共用存取簽章(SAS)驗證。 帳戶金鑰式驗證需要連線字串來進行驗證，而SAS驗證則使用允許帳戶安全委派授權的URI。

在此步驟中，您還可以透過定義容器名稱和子資料夾的路徑，指定您的帳戶將可以存取的子資料夾。

>[!BEGINTABS]

>[!TAB 連線字串]

若要使用帳戶金鑰進行驗證，請選取&#x200B;**[!UICONTROL 帳戶金鑰驗證]**&#x200B;並提供您的連線字串。 在此步驟中，您還可以指定容器名稱和要存取的子資料夾路徑。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**。

![連線字串](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS URI]

您可以使用SAS建立具有不同存取許可權的驗證認證，因為以SAS為基礎的驗證可讓您設定許可權、開始和到期日期，以及配置給特定資源。

若要使用共用存取簽章進行驗證，請選取&#x200B;**[!UICONTROL 共用存取簽章驗證]**，然後提供您的SAS URI。 在此步驟中，您還可以指定容器名稱和要存取的子資料夾路徑。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**。

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Blob]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，將您的雲端儲存空間中的資料匯入Experience Platform](../../dataflow/batch/cloud-storage.md)。
