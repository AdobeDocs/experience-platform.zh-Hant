---
keywords: Experience Platform；首頁；熱門主題；Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: 在UI中建立Google大查詢來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Google UI建立Adobe Experience Platform Big Query來源連線。
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 建立 [!DNL Google Big Query] UI中的源連接

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供建立 [!DNL Google Big Query] 源連接。

## 快速入門

本教學課程需要妥善了解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL Google BigQuery] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/databases.md).

### 收集所需憑據

若要存取 [!DNL Google BigQuery] 帳戶，您必須提供下列OAuth 2.0驗證值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `project` | 預設的專案ID [!DNL Google BigQuery] 要查詢的專案。 |
| `clientID` | 用來產生重新整理Token的ID值。 |
| `clientSecret` | 用於產生重新整理Token的密碼值。 |
| `refreshToken` | 從中取得的重新整理代號 [!DNL Google] 用於授權存取 [!DNL Google BigQuery]. |

如需這些值的詳細資訊，請參閱 [此 [!DNL Google BigQuery] 檔案](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## 連接您的Google BigQuery帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在 [!UICONTROL 資料庫] 類別，選擇 **[!UICONTROL Google BigQuery]** 然後選取 **[!UICONTROL 新增資料]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

此 **[!UICONTROL 連線至Google Big Query]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Google BigQuery] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的 [!DNL Google BigQuery] 憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![](../../../../images/tutorials/create/google-big-query/new.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL Google BigQuery] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料導入Platform](../../dataflow/databases.md).
