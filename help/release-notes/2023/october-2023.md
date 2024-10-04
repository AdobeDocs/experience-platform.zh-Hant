---
title: Adobe Experience Platform發行說明2023年10月
description: Adobe Experience Platform 2023 年 10 月版本注意事項。
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: d6e306294d0a119108e2de7ba03ebed4f633fba1
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 39%

---

# Adobe Experience Platform 發行說明

**發行日期： 2023年10月25日**

Experience Platform 現有功能的更新：

- [儀表板](#dashboards)
- [資料彙集](#data-collection)
- [目標](#destinations)
- [沙箱](#sandboxes)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 目的地使用量度 | 新的計量量度已新增到授權使用儀表板。 **[!UICONTROL Audience Activation大小]**&#x200B;和&#x200B;**[!UICONTROL 資料匯出大小]**&#x200B;量度提供便利的方法，可追蹤您從Platform匯出多少與授權使用權益相關的資料。 請參閱[可用量度](../../dashboards/guides/license-usage.md#available-metrics)檔案，瞭解這些量度和其他授權使用量度的說明。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂 Widget，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 擴充功能 | [!DNL Meta]轉換API增強功能 | [中繼轉換API](/help/tags/extensions/server/meta/overview.md)擴充功能有三個增強功能： <ul><li>與[[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe)整合：可讓您共用pixelID並存取Conversions API與Adobe整合的代號，建立順暢的登入體驗。</li><li>與[[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq)整合：可讓您傳送廣告給更有可能完成所需動作的使用者，並將動作連結回傳送的廣告。</li><li>與[[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha)整合：可讓您在CIP欄位中傳遞LiveRamp的RampID，而不需直接與合作夥伴或Meta共用PII。 </li></ul> |
| 擴充功能 | [!DNL LinkedIn]轉換API | [[!DNL LinkedIn] Conversions API](../../tags/extensions/server/linkedin/overview.md)擴充功能可將Experience Platform事件資料轉送至LinkedIn，讓您評估LinkedIn行銷活動的效益。 |
| Secret | [!DNL LinkedIn] OAuth 2密碼 | [[!DNL LinkedIn] OAuth 2密碼](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2)可讓您在事件轉送中將伺服器與伺服器的互動傳送至[!DNL LinkedIn]。 |
| 事件轉送 | 更新標籤和事件轉送 | 若要在Platform中保留[標籤](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)和[事件轉送](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)效能，僅會保留最新的開發和階段組建（成功和不成功）。 將移除所有不再使用的組建。 此外，已實施節流和速率限制，以確保少數大量的API使用不會降低其他人的API效能。 |
| 擴充功能 | 元素、規則和擴充功能 | [元素、規則和擴充功能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html)現在會在程式庫輸出中排序，以確保相同程式庫的多個組建和部署之間更一致。 |

如需有關資料收集的詳細資訊，請詳閱[資料收集概觀](../../tags/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目標或更新的目標** {#new-updated-destinations}

| 目標 | 全新或更新 | 說明 |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | 新增 | 使用Moengage目的地，即時連線您的Adobe資料（使用者屬性、區段和事件）並將其對應至MoEngage。 然後，客戶可以對這些資料採取行動，提供個人化、鎖定目標的體驗。 |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | 新增 | 在Adobe Experience Platform中彙總多個營運資料來源，作為Qualtrics Experience ID中的輸入專案，以更好地瞭解您的客戶，並實現目標式外聯，在瞭解意圖、情緒和體驗驅動因素方面縮小差距。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| (Beta)計算欄位支援雜湊函式 | 除了[匯出陣列](../../destinations/ui/export-arrays-calculated-fields.md)的特定函式或從陣列中匯出元素之外，您現在還可以使用額外的[雜湊函式](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions)在匯出的檔案中雜湊屬性。 支援的雜湊函式為： `sha`、`sha256`、`sha512`、`hash`、`md5`、`crc32`。 |
| （有限GA）在特定目的地啟用帳戶對象 | Real-Time CDP B2B客戶現在可以在某些目的地啟用[帳戶對象](../../segmentation/ui/account-audiences.md)。 如需有關此功能的詳細資訊，請參閱[啟用帳戶對象教學課程](/help/destinations/ui/activate-account-audiences.md)。 |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

如需更多有關目標的一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform 是為了在全球規模上使數位體驗應用程式更加豐富而打造。公司經常要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱工具 | 沙箱工具功能可讓您提高沙箱之間的設定準確性，以及順暢地匯出和匯入沙箱之間的沙箱設定。 您可以使用沙箱工具功能來選取不同的物件，並將它們匯出到套件中。 如需詳細資訊，請參閱[沙箱工具使用者介面指南](../../sandboxes/ui/sandbox-tooling.md)。 |

如需沙箱的詳細資訊，請參閱[沙箱概觀](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的客群。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立客群。這些客群會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 帳戶對象（有限GA） | 在Real-time Customer Data Platform B2B edition中，您現在可以使用帳戶細分，讓行銷細分體驗（從以人物為基礎的對象到以帳戶為基礎的對象）更趨簡單明瞭。 如需有關此功能的詳細資訊，請閱讀[帳戶客群概觀](../../segmentation/ui/account-audiences.md)。 |

若要深入瞭解分段服務，請閱讀[分段服務概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 更新資料登陸區域的驗證 | 您現在可以在檢視認證時檢視資料登陸區域的指定到期日。 您必須在到期日之前重新整理權杖，才能繼續在應用程式中使用。 如果您未在規定的到期日之前手動重新整理權杖，則下次您擷取認證時，會自動重新整理並提供新的權杖。 如需詳細資訊，請使用資料登陸區域](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)閱讀有關[的檔案。 |

{style="table-layout:auto"}

若要深入瞭解來源，請閱讀[來源概觀](../../sources/home.md)。
