---
title: 在使用者介面中建立Google Big Query Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立Google Big Query來源連線。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# 在使用者介面中建立[!DNL Google Big Query]來源連線

>[!IMPORTANT]
>
>[!DNL Google BigQuery]來源可在來源目錄中提供給已購買Real-time Customer Data Platform Ultimate的使用者。

Adobe Experience Platform中的Source聯結器可讓您依排程擷取外部來源資料。 本教學課程提供使用Platform使用者介面建立[!DNL Google Big Query]來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL Google BigQuery]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

### 收集必要的認證

若要在Platform上存取您的[!DNL Google BigQuery]帳戶，您必須提供下列OAuth 2.0驗證值：

| 認證 | 說明 |
| ---------- | ----------- |
| `project` | 要查詢的預設[!DNL Google BigQuery]專案的專案識別碼。 |
| `clientID` | 用來產生重新整理權杖的ID值。 |
| `clientSecret` | 用來產生重新整理權杖的密碼值。 |
| `refreshToken` | 從[!DNL Google]取得的重新整理權杖用於授權存取[!DNL Google BigQuery]。 |

如需這些值的詳細資訊，請參閱[此 [!DNL Google BigQuery] 檔案](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)。

## 連線您的Google BigQuery帳戶

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL 資料庫]類別下，選取&#x200B;**[!UICONTROL Google BigQuery]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![](../../../../images/tutorials/create/google-big-query/catalog.png)

**[!UICONTROL 連線至Google Big Query]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的[!DNL Google BigQuery]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、選擇性說明和您的[!DNL Google BigQuery]認證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/google-big-query/new.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Google BigQuery]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流以將資料帶入Platform](../../dataflow/databases.md)。
