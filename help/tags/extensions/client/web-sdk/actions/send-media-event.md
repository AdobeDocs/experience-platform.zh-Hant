---
title: 傳送媒體事件
description: 將媒體資料傳送至Adobe Experience Platform Edge Network。
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# 傳送媒體事件

**[!UICONTROL Send media event]**&#x200B;動作會將媒體事件傳送至資料流，然後應用程式和服務(例如Adobe Experience Platform或Adobe Analytics)即可使用這些資料流。 當您在屬性上追蹤串流媒體內容時，此動作很有用。

![Experience Platform UI影像顯示傳送媒體事件畫面。](../assets/send-media-event.png)

可用的選項取決於您選取的&#x200B;**[!UICONTROL Media event type]**。 所有媒體事件型別都需要&#x200B;**[!UICONTROL Player ID]**，也就是內容播放器名稱。

有些事件型別提供設定其他欄位的功能。 如果此處未列出媒體事件型別，則唯一可用的欄位為[!UICONTROL Player ID]。 下列媒體事件型別包含其他欄位：

## [!UICONTROL Ad break start]

可讓您設定Advertising Pod詳細資料。

* **[!UICONTROL Ad break name]**：廣告插播的易記名稱。
* **[!UICONTROL Ad break offset (seconds)]**：內容內的廣告插播位移（以秒為單位）。
* **[!UICONTROL Ad break index]**：內容內廣告插播的索引，從1開始。

## [!UICONTROL Ad start]

可讓您設定廣告詳細資訊。

* **[!UICONTROL Ad name]**：廣告的易記名稱。
* **[!UICONTROL Ad ID]**：廣告的識別碼。 支援任何英數字元。
* **[!UICONTROL Ad length (seconds)]**：視訊廣告的長度（以秒為單位）。
* **[!UICONTROL Advertiser]**：廣告中精選產品的公司或品牌。
* **[!UICONTROL Campaign ID]**：廣告行銷活動的識別碼。
* **[!UICONTROL Creative ID]**：廣告創意的識別碼。
* **[!UICONTROL Creative URL]**：廣告創意的URL。
* **[!UICONTROL Placement ID]**：廣告版位ID。
* **[!UICONTROL Site ID]**：廣告網站的識別碼。
* **[!UICONTROL Pod position]**：上層廣告插播內的廣告索引，從0開始。

此事件型別也支援在媒體事件裝載中提供自訂中繼資料的功能。

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**： [體驗品質](/help/xdm/data-types/qoe-data-details-collection.md)物件，指定位元速率、掉格、每秒影格數和開始時間。

## [!UICONTROL Chapter start]

可讓您設定章節詳細資訊。

* **[!UICONTROL Chapter name]**：章節或區段的名稱。
* **[!UICONTROL Chapter length]**：章節長度（以秒為單位）。
* **[!UICONTROL Chapter index]**：內容內的章節位置。
* **[!UICONTROL Chapter offset]**：章節從內容開始的位移（以秒為單位）。

此事件型別也支援在媒體事件裝載中提供自訂中繼資料的功能。

## [!UICONTROL Error]

可讓您設定錯誤詳細資料。

* **[!UICONTROL Error name]**：錯誤名稱。
* **[!UICONTROL Source]**：錯誤的來源。

## [!UICONTROL Session start]

可讓您設定媒體工作階段詳細資訊。

* **[!UICONTROL Handle media session automatically]**：允許Web SDK自動傳送必要Ping的核取方塊。 如果您要自行手動傳送Ping，可以取消核取此方塊。
* **[!UICONTROL Playhead]**：播放點（以秒為單位）。
* **[!UICONTROL Content type]**：內容型別。 支援任何字串值；Adobe也提供下列預設集：
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**：被使用內容的最長持續時間（秒）。 如果是持續時間不明的即時媒體，預設值為`86400`。
* **[!UICONTROL Content ID]**：內容的內容識別碼。
* **[!UICONTROL Ad load type]**：載入的廣告型別。 支援下列兩個值：
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**：歌曲所屬的專輯。
* **[!UICONTROL Artist]**：歌曲的演出者。
* **[!UICONTROL Asset ID]**：媒體資產內容的唯一識別碼。 這些ID通常衍生自中繼資料授權單位，例如EIDR、TMS/Gracenote或Rovi。 這些識別碼也可能來自其他專屬或內部系統。
* **[!UICONTROL Author]**：有聲書的作者姓名。
* **[!UICONTROL Authorized]**：判斷使用者是否透過Adobe驗證登入的旗標。
* **[!UICONTROL Day part]**：內容播出或播放的當天時間。 支援任何字串值。
* **[!UICONTROL Episode]**：集數。
* **[!UICONTROL Feed type]**：摘要型別。
* **[!UICONTROL First air date]**：內容在電視上的首播日期。 支援任何字串值；不過Adobe建議使用格式`YYYY-MM-DD`。
* **[!UICONTROL First digital date]**：內容在任何數位頻道或平台上的首播日期。 支援任何字串值；不過Adobe建議使用格式`YYYY-MM-DD`。
* **[!UICONTROL Content name]**：內容的易記名稱。
* **[!UICONTROL Genre]**：內容製作者定義的內容型別或群組。 此欄位支援多個值，並以逗號分隔。
* **[!UICONTROL Label]**：唱片公司的名稱。
* **[!UICONTROL Rating]**：依美國電視分級制度(TV Parental Guidelines)的定義進行分級。
* **[!UICONTROL MVPD]**： Adobe驗證所提供的MVPD。
* **[!UICONTROL Network]**：網路或頻道名稱。
* **[!UICONTROL Originator]**：內容的建立者。
* **[!UICONTROL Publisher]**：音訊內容發行者。
* **[!UICONTROL Season]**：如果節目為一系列的一部分，則為節目的季數。
* **[!UICONTROL Show]**：如果節目是數列的一部分，則為數列名稱。
* **[!UICONTROL Show type]**：節目型別。 支援任何字串值；Adobe也提供下列預設集：
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**：資料流型別。
* **[!UICONTROL Stream format]**：資料流的格式，例如HD或SD。
* **[!UICONTROL Station]**：廣播電台的名稱或ID。

此事件型別也支援在媒體事件裝載中提供自訂中繼資料的功能。 它也允許資料流設定覆寫，好讓您控制哪些應用程式和服務會接收此資料。 當您在個別命令和標籤延伸組態設定中設定資料流組態覆寫時，個別命令優先。 如需詳細資訊，請參閱[資料流組態覆寫](../configure/configuration-overrides.md)。

## [!UICONTROL States update]

可讓您設定狀態更新詳細資訊。 您可以開始或結束下列狀態：

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

下列欄位可供使用：

* **[!UICONTROL States started]**：下拉式功能表，可讓您指出狀態已開始。 選取&#x200B;**[!UICONTROL Add another state that started]**&#x200B;按鈕可讓您在同一動作中啟動多個狀態。
* **[!UICONTROL States ended]**：下拉式功能表，可讓您指出狀態已結束。 選取&#x200B;**[!UICONTROL Add another state that ended]**&#x200B;按鈕可讓您在同一動作中結束多個狀態。
