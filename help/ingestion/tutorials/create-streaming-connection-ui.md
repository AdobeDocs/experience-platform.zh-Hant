---
keywords: Experience Platform;home；熱門主題；串流連接；建立流連接；ui指南；教學課程；建立流連接；流攝取；攝取；
solution: Experience Platform
title: 使用UI建立串流連線
topic: tutorial
type: Tutorial
description: 本UI指南將協助您使用Adobe Experience Platform建立串流連線。
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# 使用UI建立串流連線

本UI指南將協助您使用Adobe Experience Platform建立串流連線。

## 快速入門

若要開始將資料串流至[!DNL Experience Platform]，您必須先建立串流HTTP連線。 建立串流連線時，您需要提供關鍵詳細資料，例如串流資料來源，以及您是否要從受信任（已驗證）或不受信任（未驗證）來源傳送資料。

註冊串流連線後，您將擁有可用來將資料串流至[!DNL Platform]的唯一URL。

請注意，為了完成本指南，您需要存取Adobe Experience Platform。 如果您沒有[!DNL Platform]的存取權，請在繼續之前與系統管理員聯絡。

## 建立串流連線

登入[!DNL Experience Platform] UI後，按一下&#x200B;**[!UICONTROL Sources]**&#x200B;以開啟&#x200B;**[!UICONTROL Catalog]**&#x200B;標籤。 此頁面將可用的來源類型顯示為個別卡片，每張卡片都包含泡泡，顯示從串流連線到資料集所建立的資料流數。

![](../images/streaming-ingestion/ui/click-sources.png)

在&#x200B;**[!UICONTROL Sources]**&#x200B;頁面上，按一下&#x200B;**[!UICONTROL HTTP API]**，然後按一下&#x200B;**[!UICONTROL Connect sources]**。

![](../images/streaming-ingestion/ui/click-connect-source.png)

出現&#x200B;**[!UICONTROL 連接到HTTP]**&#x200B;螢幕。 在&#x200B;**[!UICONTROL Service details]**&#x200B;下，提供新串流連線的名稱和說明。

在&#x200B;**[!UICONTROL 帳戶驗證]**&#x200B;下，為您的串流連接選擇以下配置屬性：

- **[!UICONTROL 驗證]:** 串流連線是否需要驗證。驗證可確保從受信任的來源收集資料。 如果處理個人識別資訊(PII)，建議開啟此功能。
- **[!UICONTROL XDM架構相容性]:** 此串流連線是否會傳送與XDM架構相容的事件。依預設，此屬性會轉換為&#x200B;**on**。

選擇完配置屬性後，按一下&#x200B;**[!UICONTROL Connect]**。 您的串流HTTP連線現在已建立，現在可在&#x200B;**[!UICONTROL Sources]**&#x200B;工作區的&#x200B;**[!UICONTROL Browse]**&#x200B;標籤下檢視。

![](../images/streaming-ingestion/ui/http-sources-details.png)

在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中，您可以按一下新建立的串流HTTP連線，並檢視該連線的詳細資訊。

![](../images/streaming-ingestion/ui/browse-sources.png)

通過按一下連接名稱的超連結，可以通過配置所連接的資料集來選擇要顯示的資料，方法是按一下&#x200B;**[!UICONTROL 選擇data]**。

![](../images/streaming-ingestion/ui/select-data.png)

您可以[建立新資料集](#create-a-new-dataset)或[使用現有資料集](#use-an-existing-dataset)。

### 建立新資料集

若要建立新資料集，請提供資料集的名稱、說明以及目標模式。

![](../images/streaming-ingestion/ui/create-new-dataset.png)

插入所有詳細資訊並按一下&#x200B;**[!UICONTROL Next]**&#x200B;後，您可以先查看提供的詳細資訊，然後按一下&#x200B;**[!UICONTROL Finish]**&#x200B;將資料集連接到流HTTP連接。

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### 使用現有資料集

若要使用現有資料集，請選取&#x200B;**[!UICONTROL Output資料集名稱]**。

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

按一下&#x200B;**[!UICONTROL Next]**&#x200B;後，您可先檢視詳細資訊，再按一下&#x200B;**[!UICONTROL Finish]**&#x200B;將選取的資料集連線至您的串流HTTP連線。

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## 後續步驟

在本教學課程中，您已建立串流HTTP連線，讓您使用串流端點來存取各種[!DNL Data Ingestion] API。 有關在API中建立流連接的說明，請閱讀[建立流連接教程](../tutorials/create-streaming-connection.md)。
