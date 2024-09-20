---
title: 在使用者介面中建立Google Big Query Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立Google Big Query來源連線。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 55aaaa39659566de81bb161d704b6f8212e29a8b
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 在使用者介面中建立[!DNL Google BigQuery]來源連線

>[!IMPORTANT]
>
>[!DNL Google BigQuery]來源可在來源目錄中提供給已購買Real-time Customer Data Platform Ultimate的使用者。

閱讀本教學課程，瞭解如何使用使用者介面將您的[!DNL Google BigQuery]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Google BigQuery]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

閱讀[[!DNL Google BigQuery] 驗證指南](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)以瞭解收集所需認證的詳細步驟。

## 連線您的Google BigQuery帳戶

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL 資料庫]類別下，選取&#x200B;**[!UICONTROL Google BigQuery]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取Google BigQuery的來源目錄。](../../../../images/tutorials/create/google-big-query/catalog.png)

**[!UICONTROL 連線至Google Big Query]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL Google BigQuery]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![現有帳戶頁面，其中顯示現有帳戶的清單。](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後為您新的[!DNL Google BigQuery]帳戶提供名稱和選擇性說明。

![來源工作流程中的新帳戶介面。](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB 使用基本驗證]

若要使用基本驗證，請選取&#x200B;**[!UICONTROL 基本驗證]**，並提供[專案、使用者端識別碼、使用者端密碼、重新整理權杖及（選擇性）大型結果資料集識別碼](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)的值。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![選取基本驗證的新帳戶介面。](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB 使用服務驗證]

若要使用服務驗證，請選取&#x200B;**[!UICONTROL 服務驗證]**，並提供[專案ID、金鑰檔案內容和（選擇性）大型結果資料集ID](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)的值。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![已選取服務驗證的新帳戶介面。](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Google BigQuery]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Platform](../../dataflow/databases.md)。
