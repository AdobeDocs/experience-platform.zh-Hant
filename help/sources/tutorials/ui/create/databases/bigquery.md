---
title: 使用UI連線 [!DNL Google BigQuery] 至Experience Platform
description: 瞭解如何使用Adobe Experience Platform UI建立Google Big Query來源連線。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# 使用UI連線[!DNL Google BigQuery]至Experience Platform

>[!IMPORTANT]
>
>[!DNL Google BigQuery]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

閱讀本教學課程，瞭解如何使用使用者介面將您的[!DNL Google BigQuery]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Google BigQuery]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

閱讀[[!DNL Google BigQuery] 驗證指南](../../../../connectors/databases/bigquery.md#prerequisites)以瞭解收集所需認證的詳細步驟。

## 瀏覽來源目錄 {#navigate}

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 您可以在&#x200B;*[!UICONTROL 類別]*&#x200B;面板中選取適當的類別。或者，您可以使用搜尋列導覽至您要使用的特定來源。

若要使用[!DNL Google BigQuery]，請選取&#x200B;*[!UICONTROL 資料庫]*&#x200B;下的&#x200B;**[!UICONTROL Google BigQuery]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 新增資料]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取Google BigQuery的來源目錄。](../../../../images/tutorials/create/google-big-query/catalog.png)

## 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取您要連線的[!DNL Google BigQuery]帳戶，然後選取[下一步] ]**以繼續。**[!UICONTROL 

![現有帳戶頁面，其中顯示現有帳戶的清單。](../../../../images/tutorials/create/google-big-query/existing.png)

## 建立新帳戶 {#create}

如果您沒有現有的帳戶，則必須提供與您來源對應的必要驗證認證，以建立新的帳戶。

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱並選擇性地為您的帳戶新增說明。

![來源工作流程中的新帳戶介面。](../../../../images/tutorials/create/google-big-query/new.png)

### 在Azure上連線到Experience Platform {#azure}

您可以使用基本或服務驗證，將您的[!DNL Google BigQuery]帳戶連線至Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 使用基本驗證]

若要使用基本驗證，請選取&#x200B;**[!UICONTROL 基本驗證]**，並提供[專案、使用者端識別碼、使用者端密碼、重新整理權杖及（選擇性）大型結果資料集識別碼](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)的值。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![選取基本驗證的新帳戶介面。](../../../../images/tutorials/create/google-big-query/basic-auth.png)

>[!TAB 使用服務驗證]

若要使用服務驗證，請選取&#x200B;**[!UICONTROL 服務驗證]**，並提供[專案ID、金鑰檔案內容和（選擇性）大型結果資料集ID](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)的值。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![已選取服務驗證的新帳戶介面。](../../../../images/tutorials/create/google-big-query/service-auth.png)

>[!ENDTABS]

### 在Amazon Web Services (AWS)上連線至Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

若要建立新[!DNL Google BigQuery]帳戶並連線至AWS上的Experience Platform，請確定您位於VA6沙箱，然後提供驗證所需的認證。

* **專案識別碼**：與您的[!DNL Google BigQuery]帳戶對應的專案識別碼。
* **金鑰檔內容**：用來驗證服務帳戶的金鑰檔。 您可以從[[!DNL Google Cloud service accounts] 儀表板](https://console.cloud.google.com)擷取此值。 金鑰檔案內容為JSON格式。 向Experience Platform驗證時，您必須在[!DNL Base64]中編碼此專案。
* **資料集識別碼**： [!DNL Google BigQuery]資料集識別碼。 此ID代表資料表所在的位置，必須預先建立此ID才能支援大型結果集。

![用於AWS連線的新帳戶介面。](../../../../images/tutorials/create/google-big-query/aws.png)

## 略過範例資料預覽 {#skip-preview-of-sample-data}

在資料選擇步驟中，您可能會在擷取大型資料表或資料檔案時遭遇逾時。 您可以略過資料預覽以避開逾時，並且仍可檢視您的結構描述，不過沒有範例資料。 若要略過資料預覽，請啟用&#x200B;**[!UICONTROL 略過預覽範例資料]**&#x200B;切換按鈕。

工作流程的其餘部分將維持不變。 唯一的警告是，略過資料預覽可能會阻止在對應步驟期間自動驗證計算和必填欄位，然後您就必須在對應期間手動驗證這些欄位。

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Google BigQuery]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Experience Platform](../../dataflow/databases.md)。
