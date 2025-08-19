---
title: 在UI中將Azure Blob儲存體連線至Experience Platform
description: 瞭解如何使用UI中的來源工作區將您的Azure Blob儲存體帳戶連結至Experience Platform。
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# 使用UI連線[!DNL Azure Blob Storage]至Experience Platform

閱讀本指南，瞭解如何使用Adobe Experience Platform使用者介面中的來源工作區將您的[!DNL Azure Blob Storage]執行個體連結至Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：在Experience Platform中組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Azure Blob Storage]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/batch/cloud-storage.md)的教學課程。

### 支援的檔案格式

Experience Platform支援從外部儲存擷取下列檔案格式：

* 分隔符號分隔值(DSV)：您可以使用任何單一欄分隔符號（例如Tab、逗號、垂直號、分號或雜湊）來收集任何格式的平面檔案。
* JavaScript物件標籤法(JSON)： JSON格式資料檔案必須符合XDM。
* Apache Parquet： Parquet格式的資料檔案必須符合XDM標準。

### 收集必要的認證

閱讀[[!DNL Azure Blob Storage] 總覽](../../../../connectors/cloud-storage/blob.md#authentication)以取得驗證的相關資訊。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 選擇類別或使用搜尋列來尋找您的來源。

若要連線到[!DNL Azure Blob Storage]，請移至&#x200B;*[!UICONTROL 雲端儲存空間]*&#x200B;類別，選取&#x200B;**[!UICONTROL Azure Blob儲存空間]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>來源顯示&#x200B;**[!UICONTROL 為新連線設定]**，如果帳戶已存在，則顯示&#x200B;**[!UICONTROL 新增資料]**。

![已選取Azure Blob儲存體來源的來源目錄。](../../../../images/tutorials/create/blob/catalog.png)

## 使用現有帳戶

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後選取您要使用的[!DNL Azure Blob Storage]帳戶。

![Azure Blob儲存體的現有來源介面。](../../../../images/tutorials/create/blob/existing.png)

## 建立新帳戶

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱並選擇性地為您的帳戶新增說明。 您可以使用下列驗證型別，將您的[!DNL Azure Blob Storage]帳戶連線至Experience Platform：

* **帳戶金鑰驗證**：使用儲存體帳戶的存取金鑰來驗證並連線至您的[!DNL Azure Blob Storage]帳戶。
* **共用存取簽章(SAS)**：使用SAS URI提供您[!DNL Azure Blob Storage]帳戶中資源的委派、有限時間存取權。
* **以服務主體為基礎的驗證**：使用Azure Active Directory (AAD)服務主體（使用者端ID和密碼）來安全地驗證您的Azure Blob儲存帳戶。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

選取&#x200B;**[!UICONTROL 帳戶金鑰驗證]**&#x200B;並提供您的`connectionString`、`container`和`folderPath`。 接著，選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![新帳戶建立步驟中的帳戶金鑰驗證選項。](../../../../images/tutorials/create/blob/account-key.png)

>[!TAB 共用存取權簽章]

選取&#x200B;**[!UICONTROL 共用存取權簽章]**&#x200B;並提供您的`sasUri`、`container`和`folderPath`。 接著，選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![新帳戶建立步驟中的共用存取簽章驗證選項。](../../../../images/tutorials/create/blob/sas.png)

>[!TAB 以服務主體為基礎的驗證]

選取&#x200B;**[!UICONTROL 以服務主體為基礎的驗證]**，並提供您的`serviceEndpoint`、`servicePrincipalId`、`servicePrincipalKey`、`accountKind`、`tenant`、`container`和`folderPath`。 接著，選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![新帳戶建立步驟中的服務主體驗證選項。](../../../../images/tutorials/create/blob/service-principal.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Azure Blob Storage]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，將您的雲端儲存空間中的資料匯入Experience Platform](../../dataflow/batch/cloud-storage.md)。
