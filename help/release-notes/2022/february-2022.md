---
title: Adobe Experience Platform發行說明2022年2月
description: 2022年2月為Adobe Experience Platform發佈的說明。
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
>本稿從2月23日的原日期改為3月7日。

Adobe Experience Platform 現有功能更新：

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供 [!DNL dashboards] 通過這些資訊，您可以查看有關組織資料的重要見解，如在每日快照中捕獲的。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 新標準目標小部件 | 以下標準小部件允許您可視化與目標相關的不同度量。<ul><li>最近按目標激活的段。 此小部件根據所選目標按降序顯示前五個最近激活的段。</li><li>對象規模趨勢. 此小部件描述已映射到該目標帳戶的段一段時間內配置檔案計數的關係。</li><li>按身份識別的未對應區段. 此 Widget 會針對特定目的地和身分識別列出按遞減的身分識別計數排名的前五個未對應區段。</li><li>按身分識別的未對應區段. 此小部件列出前五個映射的段。 段按與構件下拉菜單中選擇的目標ID匹配的源ID的各個計數從高到低排序。</li><li>常見對象. 此 Widget 會提供在頁面頂部選擇的目的地帳戶中啟動的前五個區段的清單，以及在 Widget 下拉式清單中選取的目的地。</li></ul> 有關可用標準小部件的詳細資訊，請參閱 [目標儀表板文檔。](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets)。 |

有關 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概述](../../dashboards/home.md)。

## 資料收集 {#data-collection}

平台提供一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 用於資料流配置的改進的UI工作流 | 已在資料收集UI中建立新資料流的工作流已更新。 將服務添加到資料流時，選項清單中將只包含您有權訪問的服務。 請參閱上的指南 [配置資料流](../../edge/datastreams/overview.md) 的子菜單。 |
| 資料收集的資料準備 | 如果您使用Adobe Experience PlatformWeb SDK，現在可以利用資料準備功能將資料映射到伺服器端的體驗資料模型(XDM)。 請參閱 [資料收集的資料準備](../../edge/datastreams/data-prep.md) 的子菜單。 |
| 第一方設備ID | 使用平台Web SDK收集客戶資料時，您現在可以將自己的設備ID發送到Adobe Experience Platform邊緣網路，這為最近對第三方Cookie生命週期的瀏覽器限制提供了一種解決方法。 請參閱上的指南 [第一方設備ID](../../edge/identity/first-party-device-ids.md) 的子菜單。 |

有關平台中資料收集的詳細資訊，請參閱 [資料收集概述](../../collection/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新增或更新的功能**

| 功能 | 說明 |
| ----------- | ----------- |
| (Beta)對基於檔案的目標的Destination SDK支援 | [Destination SDK對基於檔案的目標的支援](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) 目前是私有beta版，僅供選定數量的合作夥伴和客戶使用。 在正式發佈之前，功能和相關文檔可能會發生更改。<br><br>請與Adobe客戶代表聯繫，瞭解如何訪問該功能。 Adobe — 內部客戶代表應聯繫Experience Platform目的地產品和工程團隊，討論受支援的使用案例。 <br><br> 在基於檔案的目標的Destination SDK支援的測試階段，測試合作夥伴和客戶可以使用 [Experience PlatformDestination SDK](../../destinations/destination-sdk/overview.md) 要從以下功能中獲益，請構建專用目標： <ul><li>通過AmazonS3、SFTP伺服器、Azure Blob、Azure Data Lake Storage、Data Landing Zone儲存建立基於檔案的（批處理）目標。</li><li>配置和設定預設檔案導出計畫和頻率選項。</li><li>配置和設定選項以格式化導出的CSV檔案（分隔符、轉義字元和其他選項）。</li><li>能夠設定和編輯自定義檔案頭。</li><li>能夠接收有關檔案和段導出的事件通知。</li><li>能夠導出其他檔案類型，如CSV、TSV、JSON和Parmet。</li></ul>  <br>要開始使用新功能，請閱讀 [（測試版）使用Destination SDK配置基於檔案的目標](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)。 <br><br> 建立專用或已生產化的功能 *流* 所有Experience Platform客戶和合作夥伴都可以使用「Destination SDK」來確定目的地。 閱讀有關如何 [使用Destination SDK配置流目標](../../destinations/destination-sdk/guides/configure-destination-instructions.md) 的雙曲餘切值。 |

## [!DNL Identity Service] {#identity}

提供相關數字型驗需要全面瞭解您的客戶。 當您的客戶資料分散在不同的系統中，導致每個客戶都顯示有多個「身份」時，這就變得更加困難了。

Adobe Experience Platform [!DNL Identity Service] 通過跨設備和系統橋接身份，幫助您更好地瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 新權限 `view-identity-graph` | 您現在可以使用 `view-identity-graph` 控制組織中的用戶是否能夠查看身份圖資料的權限。 未具有此權限的用戶將被禁止訪問UI中的標識圖查看器，或在訪問 [!DNL Identity Service] 返回標識的API。 查看 [訪問控制概述](../../access-control/home.md) 的子菜單。 |

有關 [!DNL Identity Service]，請參閱 [Identity Service概述](../../identity-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| Beta源移至GA | 已將以下源從beta升級為GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。