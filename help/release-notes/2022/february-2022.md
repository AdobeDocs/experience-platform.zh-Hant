---
title: Adobe Experience Platform發行說明2022年2月
description: 2022年2月Adobe Experience Platform發行說明。
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: e2342a8a7d03074ac26fbd129a2e7fd520ccb0c3
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 9%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 3 月 7 日**

>[!NOTE]
>
>原發行日期從2月23日改為3月7日。

Adobe Experience Platform 現有功能更新：

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個 [!DNL dashboards] 您可以透過此檢視在每日快照期間擷取的組織資料重要深入分析。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 新標準目標小工具 | 下列標準Widget可讓您視覺化與目的地相關的不同量度。<ul><li>依目的地最近啟用的區段。 此介面工具集會根據所選目的地以遞減順序顯示前五個最近啟動的區段。</li><li>對象規模趨勢. 此介面工具集描述已對應至該目標帳戶之區段在一段時間內的設定檔計數關係。</li><li>按身份識別的未對應區段. 此 Widget 會針對特定目的地和身分識別列出按遞減的身分識別計數排名的前五個未對應區段。</li><li>按身分識別的未對應區段. 此介面工具集列出前5個對應區段。 區段會根據符合從介面工具集的下拉式選單中選取之目標ID的個別來源ID數量，從高到低排序。</li><li>常見對象. 此 Widget 會提供在頁面頂部選擇的目的地帳戶中啟動的前五個區段的清單，以及在 Widget 下拉式清單中選取的目的地。</li></ul> 有關可用標準小部件的詳細資訊，請參閱 [目的地控制面板檔案。](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

如需 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## 資料收集 {#data-collection}

Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分送至Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 改善資料流設定的UI工作流程 | 更新在資料收集UI中建立新資料流的工作流程。 將服務新增至資料流時，選項清單中只會包含您有權存取的服務。 請參閱 [設定資料流](../../edge/datastreams/overview.md) 以取得更多資訊。 |
| 資料收集的資料準備 | 如果您使用Adobe Experience Platform Web SDK，現在可以運用資料準備功能，將資料對應至伺服器端的Experience Data Model(XDM)。 請參閱 [資料收集的資料準備](../../edge/datastreams/data-prep.md) ，以了解詳細資訊。 |
| 第一方裝置ID | 使用Platform Web SDK收集客戶資料時，您現在可以將自己的裝置ID傳送至Adobe Experience Platform Edge Network，以因應最新瀏覽器對第三方Cookie存留期的限制。 請參閱 [第一方裝置ID](../../edge/identity/first-party-device-ids.md) 以取得更多資訊。 |

如需Platform中資料收集的詳細資訊，請參閱 [資料匯集概述](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| （測試版）檔案型目的地的Destination SDK支援 | [Destination SDK支援檔案式目的地](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) 目前為私人測試版，僅適用於特定數量的合作夥伴和客戶。 在正式發行前，功能和相關檔案可能會有所變更。<br><br>請連絡您的Adobe客戶代表，了解如何存取功能。 Adobe內部客戶代表應洽詢Experience Platform目的地產品和工程團隊，以討論支援的使用案例。 <br><br> 在針對檔案式目的地的Destination SDK支援測試階段，測試版合作夥伴和客戶可使用 [Experience PlatformDestination SDK](../../destinations/destination-sdk/overview.md) 若要建置私人目的地，以便受益於下列功能： <ul><li>透過Amazon S3、SFTP伺服器、Azure Blob、Azure資料湖儲存、資料登陸區儲存，建立檔案型（批次）目的地。</li><li>設定和設定預設的檔案匯出排程和頻率選項。</li><li>設定和設定選項，以設定匯出CSV檔案的格式（分隔字元、逸出字元和其他選項）。</li><li>可設定及編輯自訂檔案標題。</li><li>能接收檔案和區段匯出的事件通知。</li><li>可匯出其他檔案類型，例如CSV、TSV、JSON、Parquet。</li></ul>  <br>若要開始使用新功能，請閱讀 [（測試版）使用Destination SDK來設定檔案式目的地](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> 建立專用或產品化的功能 *串流* 所有Experience Platform客戶和合作夥伴皆已可使用透過Destination SDK進行目的地。 閱讀指南，了解如何 [使用Destination SDK來設定串流目的地](../../destinations/destination-sdk/guides/configure-destination-instructions.md) 以取得詳細資訊。 |

## [!DNL Identity Service] {#identity}

要提供相關的數位體驗，必須全面了解客戶。 當您的客戶資料分散於不同的系統，導致每個個別客戶看起來都有多個「身分」時，就會更加困難。

Adobe Experience Platform [!DNL Identity Service] 可跨裝置和系統橋接身分，協助您即時提供具影響力的個人數位體驗，進而協助您更清楚掌握客戶及其行為。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 的新權限 `view-identity-graph` | 您現在可以使用 `view-identity-graph` 可控制組織中的使用者是否能檢視身分圖表資料的權限。 沒有此權限的使用者將被禁止存取UI中的身分圖表檢視器，或存取 [!DNL Identity Service] 傳回身分的API。 請參閱 [存取控制概觀](../../access-control/home.md) 以取得權限的詳細資訊。 |

有關 [!DNL Identity Service]，請參閱 [Identity服務概述](../../identity-service/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 測試版來源轉至GA | 下列來源已從測試版提升為正式發行： <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).