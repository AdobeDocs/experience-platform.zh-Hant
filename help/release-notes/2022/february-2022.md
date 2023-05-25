---
title: Adobe Experience Platform發行說明2022年2月
description: Adobe Experience Platform的2022年2月發行說明。
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
>此版本已從原始日期2月23日改為3月7日。

Adobe Experience Platform 現有功能更新：

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個 [!DNL dashboards] 您可以透過它檢視有關您組織資料的重要深入分析，如每日快照期間所擷取。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 新的標準目的地Widget | 下列標準Widget可讓您視覺化與目的地相關的不同量度。<ul><li>目的地最近啟用的區段。 此Widget會根據所選目的地，以遞減順序顯示最近啟用的前五個區段。</li><li>對象規模趨勢. 此Widget針對已對應至目的地帳戶的區段，描述一段時間內設定檔計數之間的關係。</li><li>按身份識別的未對應區段. 此 Widget 會針對特定目的地和身分識別列出按遞減的身分識別計數排名的前五個未對應區段。</li><li>按身分識別的未對應區段. 此Widget列出前五個對應區段。 區段會根據其各自符合從Widget下拉式選單中選取之目的地ID的來源ID計數，從高到低排序。</li><li>常見對象. 此 Widget 會提供在頁面頂部選擇的目的地帳戶中啟動的前五個區段的清單，以及在 Widget 下拉式清單中選取的目的地。</li></ul> 如需可用標準Widget的詳細資訊，請參閱 [目的地儀表板檔案。](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

如需詳細資訊，請參閱 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概觀](../../dashboards/home.md).

## 資料彙集 {#data-collection}

Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 改善資料流設定的UI工作流程 | 更新在資料收集UI中建立新資料流的工作流程。 將服務新增至資料流時，只有您有權存取的服務會包含在選項清單中。 請參閱指南： [設定資料串流](../../edge/datastreams/overview.md) 以取得詳細資訊。 |
| 資料收集的資料準備 | 如果您使用Adobe Experience Platform Web SDK，您現在可以運用資料準備功能，將您的資料對應至伺服器端的Experience Data Model (XDM)。 請參閱以下小節： [資料收集的資料準備](../../edge/datastreams/data-prep.md) 如需詳細資訊，請參閱資料串流指南。 |
| 第一方裝置ID | 使用Platform Web SDK收集客戶資料時，您現在可以將自己的裝置ID傳送至Adobe Experience Platform Edge Network，針對第三方Cookie有效期限的最新瀏覽器限制提供因應措施。 請參閱指南： [第一方裝置ID](../../edge/identity/first-party-device-ids.md) 以取得詳細資訊。 |

如需Platform資料收集的詳細資訊，請參閱 [資料彙集概觀](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| (Beta)檔案型目的地的Destination SDK支援 | [檔案型目的地的Destination SDK支援](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) 目前為私人測試版，僅供特定數量的合作夥伴和客戶使用。 功能和相關檔案在正式發行前可能會有所變更。<br><br>請聯絡您的Adobe客戶代表，瞭解如何存取該功能。 Adobe內部客戶代表應聯絡Experience Platform目標產品與工程團隊，討論支援的使用案例。 <br><br> 在對檔案型目的地提供Destination SDK支援的測試階段，測試版合作夥伴和客戶可以使用 [Experience PlatformDestination SDK](../../destinations/destination-sdk/overview.md) 若要建置私人目的地以受益於以下功能： <ul><li>透過Amazon S3、SFTP伺服器、Azure Blob、Azure Data Lake儲存空間、資料登陸區域儲存空間，建立檔案式（批次）目的地。</li><li>設定並設定預設檔案匯出排程和頻率選項。</li><li>設定並設定匯出的CSV檔案的格式選項（分隔字元、逸出字元和其他選項）。</li><li>設定和編輯自訂檔案標題的功能。</li><li>能夠接收有關檔案和區段匯出的事件通知。</li><li>可匯出其他檔案型別，例如CSV、TSV、JSON、Parquet。</li></ul>  <br>若要開始使用新功能，請閱讀 [（測試版）使用Destination SDK設定以檔案為基礎的目的地](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> 建立私人或產品化的功能 *串流* 所有Experience Platform客戶和合作夥伴皆可使用「使用Destination SDK」目的地。 閱讀操作指南 [使用Destination SDK設定串流目的地](../../destinations/destination-sdk/guides/configure-destination-instructions.md) 以取得詳細資訊。 |

## [!DNL Identity Service] {#identity}

提供相關的數位體驗需要完全瞭解您的客戶。 當您的客戶資料分散於不同的系統時，這會使情況更困難，導致每個個別客戶似乎有多個「身分」。

Adobe Experience Platform [!DNL Identity Service] 透過跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更好地瞭解客戶及其行為。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 的新許可權 `view-identity-graph` | 您現在可以使用 `view-identity-graph` 控制組織中使用者是否能夠檢視身分圖表資料的許可權。 沒有此許可權的使用者將無法在UI中或存取時存取身分圖表檢視器 [!DNL Identity Service] 傳回身分的API。 請參閱 [存取控制總覽](../../access-control/home.md) 以取得許可權的詳細資訊。 |

如需更多一般資訊，請參閱 [!DNL Identity Service]，請參閱 [Identity Service概觀](../../identity-service/home.md).

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| Beta版來源移至GA | 下列來源已從Beta版升級至GA版： <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).