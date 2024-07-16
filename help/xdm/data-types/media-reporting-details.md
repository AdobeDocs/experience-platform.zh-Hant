---
title: 媒體報表詳細資料資料型別
description: 瞭解Media Reporting Details Experience Data Model (XDM)資料型別。
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# [!UICONTROL 媒體報告詳細資料]資料型別

>[!NOTE]
>
>媒體收集欄位會擷取資料，並將其傳送至其他Adobe服務以供進一步處理。 Adobe服務會使用媒體報表欄位來分析使用者傳送的「媒體收集」欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。

[!UICONTROL 媒體報告詳細資料]是標準的體驗資料模型(XDM)資料型別，可擷取有關媒體播放事件的重要詳細資料。 使用[!UICONTROL 媒體報告詳細資料]資料型別來擷取詳細資料，例如內容內的播放點位置、唯一的工作階段識別碼，以及與工作階段相關的各種巢狀屬性等等。 此資料型別提供播放體驗的全面概觀，可讓您在播放工作階段期間追蹤和分析媒體消耗模式和相關事件。

>[!NOTE]
>
>以下提及的欄位不會直接用來建立請求。 相反地，傳送至Adobe Experience Platform或Adobe Analytics的欄位集合會從您的請求資料中組合，然後由伺服器基礎架構匯入或處理量度。 雖然Platform會收集您各種型別的使用者事件，但傳回給您的報告會著重於特定事件，例如`media.sessionStart`、`media.adStart`和`media.sessionComplete`。 這表示雖然您在收集期間傳輸12種型別的事件，但您的報表只會顯示以下所列五個事件的劃分。

+++選取此選項可顯示[!UICONTROL 媒體報告詳細資料]資料型別的圖表。
![ [!UICONTROL 媒體報告詳細資料]資料型別的圖表。](../images/data-types/media-reporting-details.png)
+++

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Advertising詳細資料] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Advertising詳細資料是指體驗事件期間與廣告活動相關的特定資訊。 這包括廣告中繼資料、目標定位詳情和效能量度。 |
| [!UICONTROL Advertising Pod詳細資料] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Advertising Pod詳細資料包含體驗事件中廣告Pod的相關資訊。 它提供廣告順序、內容和參與量度的深入分析。 |
| [!UICONTROL 章節詳細資料] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | 章節詳細資料會擷取和內容的章節或分段部分相關的資料。 它提供有關章節標籤、時間軸和相關聯的中繼資料的資訊。 |
| [!UICONTROL 狀態清單] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | States屬性是一個陣列，可擷取整個體驗事件的各種狀態。 此屬性提供有關播放、使用者動作或內容變更的循序資料。 |
| [!UICONTROL Qoe資料詳細資料] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | QoE （體驗品質）資料詳細資料會擷取效能相關量度和使用者體驗資料。 它提供品質、回應速度和使用者互動的深入分析。 |
| [!UICONTROL 工作階段詳細資料] | `sessionDetails` | [[!UICONTROL 工作階段詳細資料]](./session-details-reporting.md) | 「工作階段詳細資料」包括與體驗事件相關的全面資訊，提供與播放工作階段相關的使用者互動、持續時間和內容資料的深入分析。 |
| [!UICONTROL 自訂中繼資料] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | 自訂中繼資料包含使用者定義的或與體驗事件相關聯的其他中繼資料。 此中繼資料可讓個人化或特定資料包含在事件內容中。 |
| [!UICONTROL 播放點] | `playhead` | 整數 | 播放點代表媒體內容中的目前播放位置。 若為即時內容，則代表當天的目前秒數(0 &lt;=播放點&lt; 86400)。 對於錄製的內容，這會反映內容持續時間的目前秒數（0 &lt;=播放點&lt;內容長度）。 |

{style="table-layout:auto"}
