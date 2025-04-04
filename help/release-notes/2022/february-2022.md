---
title: Adobe Experience Platform 發行說明 (2022 年 2 月)
description: Adobe Experience Platform 2022 年 2 月版發行說明。
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 17%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年3月7日**

>[!NOTE]
>
>此版本已從原始日期2月23日變更為3月7日。

Adobe Experience Platform 現有功能的更新：

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個[!DNL dashboards]，您可以透過它們檢視有關您組織資料的重要深入分析，如每日快照期間所擷取。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 新的標準目的地Widget | 下列標準Widget可讓您視覺化與目的地相關的不同量度。<ul><li>目的地最近啟用的區段。 此Widget會根據所選目的地，以遞減順序顯示最近啟用的前五個區段。</li><li>對象人數趨勢。 此Widget針對已對應至目的地帳戶的區段，描述一段時間內設定檔計數之間的關係。</li><li>依身分割槽分的未對應區段。 此Widget會依指定目的地和身分的遞減身分計數，列出前五個未對應的區段。</li><li>依身分割槽分的對應區段。 此Widget列出前五個對應區段。 區段會根據其各自符合從Widget下拉式選單中所選目的地ID的來源ID計數，從高到低排序。</li><li>通用對象。 此Widget提供在頁面上方所選目的地帳戶，以及在下拉式Widget中選取的目的地啟用的前五個區段清單。</li></ul> 如需可用標準Widget的詳細資訊，請參閱[目的地儀表板檔案。](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets)。 |

如需更多有關 [!DNL Dashboards] 的資訊，請參閱[[!DNL Dashboards] 概觀](../../dashboards/home.md)。

## 資料彙集 {#data-collection}

Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料並將資料傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發至Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 改善資料流設定的UI工作流程 | 更新在資料收集UI中建立新資料流的工作流程。 將服務新增至資料流時，只有您有權存取的服務會包含在選項清單中。 如需詳細資訊，請參閱[設定資料流](../../datastreams/overview.md)的指南。 |
| 資料收集的資料準備 | 如果您使用Adobe Experience Platform Web SDK，現在可以運用資料準備功能，將您的資料對應至伺服器端的Experience Data Model (XDM)。 如需詳細資訊，請參閱資料串流指南中資料彙集](../../datastreams/data-prep.md)的[資料準備。 |
| 第一方裝置 ID | 您現在可以在使用Adobe Experience Platform Web Edge Network收集客戶資料時，將自己的裝置ID傳送至Experience Platform SDK，針對第三方Cookie有效期限的最新瀏覽器限制提供因應措施。 如需詳細資訊，請參閱[第一方裝置識別碼](../../web-sdk/identity/first-party-device-ids.md)的指南。 |

如需Experience Platform中資料收集的詳細資訊，請參閱[資料收集概觀](../../collection/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| (Beta) Destination SDK支援檔案型目的地 | [檔案型目的地的Destination SDK支援](../../destinations/destination-sdk/functionality/destination-server/server-specs.md)目前為私人測試版，僅供特定數目的合作夥伴和客戶使用。 功能和相關檔案在正式發行前可能會有所變更。<br><br>請聯絡您的Adobe客戶代表，瞭解如何存取此功能。 Adobe內部客戶代表應聯絡Experience Platform目標產品與工程團隊，討論支援的使用案例。 <br><br>在Destination SDK檔案型目的地支援的測試階段中，測試版合作夥伴和客戶可以使用[Experience Platform Destination SDK](../../destinations/destination-sdk/overview.md)建置私人目的地，以受益於下列功能： <ul><li>透過Amazon S3、SFTP伺服器、Azure Blob、Azure Data Lake儲存空間、資料登陸區域儲存空間，建立檔案式（批次）目的地。</li><li>設定並設定預設的檔案匯出排程和頻率選項。</li><li>設定並設定選項，以格式化匯出的CSV檔案（分隔字元、逸出字元和其他選項）。</li><li>設定和編輯自訂檔案標題的功能。</li><li>能夠接收有關檔案和區段匯出的事件通知。</li><li>可匯出其他檔案型別，例如CSV、TSV、JSON、Parquet。</li></ul>  <br>若要開始使用新功能，請閱讀[(Beta)使用Destination SDK設定檔案型目的地](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)。 <br><br>所有Experience Platform客戶和合作夥伴皆可使用Destination SDK來建立私人或產品化的&#x200B;*串流*&#x200B;目的地。 閱讀如何[使用Destination SDK設定串流目的地](../../destinations/destination-sdk/guides/configure-destination-instructions.md)的指南，以取得詳細資料。 |

## [!DNL Identity Service] {#identity}

提供相關的數位體驗需要完全瞭解您的客戶。 當您的客戶資料分散於不同的系統時，這會使工作變得更困難，導致每個個別客戶似乎擁有多個「身分」。

Adobe Experience Platform [!DNL Identity Service]可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| `view-identity-graph`的新許可權 | 您現在可以使用`view-identity-graph`許可權來控制組織中的使用者是否能夠檢視身分圖表資料。 沒有此許可權的使用者將被禁止在UI中存取身分圖表檢視器，或在存取傳回身分的[!DNL Identity Service] API時進行存取。 如需許可權的詳細資訊，請參閱[存取控制總覽](../../access-control/home.md)。 |

如需[!DNL Identity Service]的一般資訊，請參閱[身分識別服務總覽](../../identity-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| Beta來源移至GA | 下列來源已從Beta版升級至GA版： <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。