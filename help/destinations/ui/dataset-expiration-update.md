---
title: 為2024年11月之前建立的資料流延長資料集匯出排程
description: 瞭解如何為2024年11月之前建立的資料集匯出資料流（將於2025年9月1日停止運作）延長匯出排程。
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 6f8b906729ec31cc0c4847ccd0ae0f89f63a1627
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# 為2024年11月之前建立的資料流延長資料集匯出排程

>[!IMPORTANT]
>
>**需要動作**：如果您的組織已在2024年11月之前建立[資料集匯出資料流](export-datasets.md)，這些資料流將於2025年9月1日停止運作。 本指南說明如何針對您想要保留的資料流，將匯出排程延長到此日期以後。

## 概觀 {#overview}

在Experience Platform [的2024年9月](/help/release-notes/2024/september-2024.md#destinations)日版本中，Adobe為2024年9月版本之前建立的所有資料集匯出資料流，引入預設結束日期&#x200B;**2025年5月1日**。

**對於**&#x200B;在2024年11月之前&#x200B;**建立的所有資料集匯出資料流，此日期已更新為2025年9月1日**。

在2024年11月之前建立的資料集匯出資料流將於2025年9月1日&#x200B;**停止匯出資料**，除非您手動延長其到期日。

如果您需要資料流在&#x200B;**2025年9月1日**&#x200B;之後繼續匯出資料，您必須依照本指南中的步驟，為您要匯出資料集的每個目的地擴充其排程。

## 受影響的目的地 {#affected-destinations}

您的組織可能有使用中的資料集匯出資料流，會將資料傳送到下列目的地。 請依照下節中的步驟操作，並觀看逐步解說影片，以瞭解如何識別哪些資料集將設為過期。

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## 教學課程影片 {#video}

請觀看以下影片，逐步示範如何使用即將到來的結束日期識別資料集匯出，並為您想要保留的資料流延長匯出排程。

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## 步驟1：識別受影響的資料流 {#identify-dataflows}

在延長資料集匯出資料流程的匯出排程之前，您必須先識別哪些資料流程會受即將到來的到期日影響。 請依照下列步驟，尋找需要動作的資料流。

1. 前往Experience Platform UI中的&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**。
2. 在含有作用中資料集匯出資料流的目的地上選取&#x200B;**[!UICONTROL 啟用]**。

   >[!TIP]
   >
   >使用目錄左側的&#x200B;**[!UICONTROL 資料型別]**&#x200B;篩選器，依&#x200B;**[!UICONTROL 資料集]**&#x200B;篩選可用的目的地。

3. 選取&#x200B;**[!UICONTROL 資料集]**資料型別以僅顯示具有資料集匯出的資料流。
   ![熒幕擷圖顯示如何依資料型別篩選資料流程。](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. 選取&#x200B;**[!UICONTROL 已建立]**&#x200B;欄標題，並選擇&#x200B;**[!UICONTROL 遞增排序]**以檢視較舊的資料流。
   ![顯示如何遞增排序資料流程的熒幕擷圖。](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. 識別您要保留在2024年11月之前建立的資料流。

## 步驟2：存取匯出資料集工作流程 {#access-workflow}

對於要保留的每個資料流，您需要存取匯出資料集工作流程以修改排程。

1. 在&#x200B;**[!UICONTROL 名稱]**&#x200B;欄中選取資料流名稱。 這會將您帶往&#x200B;**[!UICONTROL 資料流執行]**&#x200B;頁面。
2. 在此頁面中，選取&#x200B;**[!UICONTROL 匯出資料集]**選項。
   ![在資料流執行頁面中顯示匯出資料集選項的熒幕擷圖。](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. 在&#x200B;**[!UICONTROL 選取資料集]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 下一步]**。 您不需要將任何新資料集新增到資料流。
4. 這會將您帶往&#x200B;**[!UICONTROL 排程]**頁面，您也可以在此看到通知資料集匯出到期日的通知。
   ![資料集匯出資料流，其中包含到期通知](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## 步驟3：擴充匯出排程 {#extend-export-schedule}

現在您可以修改匯出排程，將其延長到2025年9月1日之後。

1. 選取&#x200B;**[!UICONTROL 編輯排程]**。
   ![顯示[編輯排程]按鈕之[排程]步驟的熒幕擷圖。](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. 選取新的匯出排程，然後選取&#x200B;**[!UICONTROL 儲存]**。
   ![顯示排程選項的排程步驟熒幕擷圖。](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >請檢視[資料集匯出檔案](export-datasets.md#scheduling)，以取得有關如何設定資料集匯出排程的詳細指引。

## 如果我錯過2025年9月1日的最後期限，會發生什麼事？ {#missed-deadline}

如果您的資料集匯出資料流於2025年9月1日到期，而您尚未延長其排程，則您有&#x200B;**30天的寬限期**，您可聯絡Adobe以重新啟用資料流，而不會遺失任何資料。 這包括9月1日至您聯絡Adobe之日期間未匯出的資料。

>[!IMPORTANT]
>
>雖然Adobe提供此寬限期，我們強烈建議您在截止日期2025年9月1日之前延長排程，以確保資料匯出不會受到干擾，並避免任何服務中斷。
