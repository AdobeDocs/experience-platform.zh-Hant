---
title: Adobe Experience Platform 發行說明 (2024 年 1 月)
description: Adobe Experience Platform 2024 年 1 月版發行說明。
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 39%

---

# Adobe Experience Platform 發行說明

**發行日期： 2024年1月30日**

Adobe Experience Platform中的新功能：

- [使用案例教戰手冊](#use-case-playbooks)

Experience Platform現有功能的更新：

- [屬性型存取控制](#abac)
- [資料準備](#data-prep)
- [儀表板](#dashboards)
- [目的地](#destinations)
- [身分識別服務](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [即時客戶設定檔](#profile)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 使用案例教戰手冊 {#use-case-playbooks}

[!UICONTROL 使用案例教戰手冊]功能現在已普遍提供給所有Real-Time CDP和Adobe Journey Optimizer客戶。 [!UICONTROL 使用案例教戰手冊]的設計目的，是協助使用者在開始使用Real-time Customer Data Platform或Adobe Journey Optimizer時克服挑戰。 當您不確定從何處開始或是如何針對您想要的使用案例建立正確的資產時，使用案例教戰手冊會提供靈感，並建立不同的資產，讓您在準備就緒時測試並匯入生產環境。

若要開始使用[!UICONTROL 使用案例教戰手冊]，請閱讀下列檔案頁面：

- 閱讀[概觀頁面](/help/use-case-playbooks/playbooks/overview.md)以瞭解用途、可用性資訊，並取得教戰手冊如何運作的端對端示範，從探索到建立執行個體，再到將產生的資產匯入其他沙箱環境。
- 取得所有[可用教戰手冊](/help/use-case-playbooks/playbooks/playbooks-list.md)的清單，依產品分組(Real-Time CDP或Journey Optimizer)
- 取得所有[必要許可權](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions)的相關資訊，以使用教戰手冊和教戰手冊產生的資產。
- 瞭解[資料感知功能](/help/use-case-playbooks/playbooks/data-awareness.md)，其可讓您將產生的資產複製到其他沙箱環境
- 如果您在使用使用案例教戰手冊時遇到錯誤或困難，請取得[疑難排解提示](/help/use-case-playbooks/playbooks/troubleshooting.md)。

## 屬性型存取控制 {#abac}

屬性型存取控制是 Adob&#x200B;&#x200B;e Experience Platform 的一項功能，此平台為注重隱私的品牌提供更大的靈活性來管理使用者存取。可以將結構描述欄位和分段等個別對象指派給使用者角色。此功能允許您授予或撤銷組織中特定平台使用者對個別物件的存取權限。

透過屬性型存取控制，組織的管理員可以控制使用者對所有平台工作流程和資源的存取權限，包括其中的敏感個人資料 (SPD)、個人身分資訊 (PII) 和其他自訂類型資料。管理員可以定義只能存取特定欄位以及這些欄位對應資料的使用者角色。

**新檔案或更新的檔案**

| 檔案更新 | 說明 |
| --- | --- |
| 已記錄用於屬性式存取控制的新API端點 | [存取控制API參考檔案](https://developer.adobe.com/experience-platform-apis/references/access-control/)現在包含以屬性為基礎的存取控制API角色、原則及產品端點。 這些端點可用於為使用者擷取指定沙箱中指定資源的相關角色、原則和產品。 |

{style="table-layout:auto"}

若要了解更多關於屬性型存取控制，請參閱[屬性型存取控制概觀](../../access-control/abac/overview.md)。關於屬性型存取控制工作流程的綜合指南，請閱讀[屬性型存取控制端對端指南](../../access-control/abac/end-to-end-guide.md)。

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 新的對應工具函數 | <ul><li>`object_to_map`：使用`object_to_map`函式來建立對應資料型別。 此函式支援數種不同的語法。 如需詳細資訊，請閱讀階層 — 物件](../../data-prep/functions.md#objects)的[函式指南。 </li><li>`to_map`：使用`to_map`函式，使用物件建立具有指定欄位名稱和值配對的對應。 如需詳細資訊，請閱讀階層 — 對應](../../data-prep/functions.md#map)的[函式指南。 </li><li>`array_to_map`：使用`array_to_map`函式，使用物件陣列建立具有指定欄位名稱和值配對的對應。 如需詳細資訊，請閱讀階層 — 對應](../../data-prep/functions.md#map)的[函式指南。 |

{style="table-layout:auto"}

如需「資料準備」的詳細資訊，請閱讀[資料準備總覽](../../data-prep/home.md)。

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 檢視 SQL | 您現在可以使用「檢視SQL」切換來檢視「設定檔」、「對象」、「目的地」和自訂深入分析背後的SQL，然後透過「查詢編輯器」依需求執行查詢。 存取支援Real-time Customer Data Platform深入分析的SQL可幫助您瞭解資料模型分析背後的邏輯。 此透明度可讓您的AdobeReal-time CDP資料更易於存取、理解，並更能對決策產生影響。<br>從SQL中汲取超過40種現有見解的靈感，以建立新的查詢，這些查詢會根據您的業務需求從Platform資料中獲得獨特的見解。 SQL也適用於Experience League檔案中的[設定檔](../../dashboards/insights/profiles.md)、[對象](../../dashboards/insights/audiences.md)和[目的地](../../dashboards/insights/destinations.md)深入分析。 這些檔案會強調可使用標準深入分析來回答的業務使用案例。 如需詳細資訊，請閱讀[檢視分析SQL](../../dashboards/view-sql.md)的指南。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂 Widget，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [公用連線](../../destinations/catalog/advertising/pubmatic.md) | 使用此目的地將對象資料傳送至[!DNL PubMatic Connect]平台。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 適用於Amazon S3目的地的新&#x200B;**承擔角色**&#x200B;驗證型別 | 如果您不想與Experience Platform共用帳戶金鑰和秘密金鑰，請在將Experience Platform連線至您的Amazon S3貯體時，使用新的假定角色驗證型別。 在Amazon S3檔案的[驗證區段](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication)中閱讀更多有關新驗證方法的資訊。 |

{style="table-layout:auto"}

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 身分識別服務 {#identity-service}

Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。

**新檔案或更新的檔案**

| 檔案更新 | 說明 |
| --- | --- |
| 檔案重組 | Identity Service檔案已重新編排，以改善Identity Service中概念的呈現方式及清晰度：<ul><li>請造訪[Identity Service概觀頁面](../../identity-service/home.md)，瞭解擴充的術語指南、詳細描述典型客戶歷程的使用案例範例、Identity Service如何將身分連結在一起的劃分，以及Identity Service在Experience Platform生態系統中所扮演角色的摘要。</li><li>請閱讀[上的指南，瞭解Identity Service和即時客戶個人檔案](../../identity-service/identity-and-profile.md)之間的關係，瞭解這兩種服務如何共同運作及其目的、程式、輸入和輸出之間的差異的詳細摘要。</li><li>請參閱[身分服務連結邏輯指南](../../identity-service/features/identity-linking-logic.md)，以取得身分圖表在指定不同案例和時間戳記下的行為方式說明和視覺效果。</li></ul> |

{style="table-layout:auto"}

若要深入瞭解Identity Service，請閱讀[Identity Service概觀](../../identity-service/home.md)。

## Real-Time Customer Data Platform {#rtcdp}

建置在 Experience Platform、Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 上有助於公司匯集已知和未知的資料，以使用整個客戶歷程中的智慧型決策啟動客戶設定檔。[!DNL Real-Time CDP] 會結合多個企業資料來源以即時建立客戶設定檔。然後，根據這些設定檔建置的區段即可傳送到下游目的地，以便在所有管道和裝置上提供一對一的個人化客戶體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [Real-Time CDP首頁](https://experience.adobe.com)的更新 | <ul><li>**設定檔Widget**：您現在可以使用設定檔Widget瀏覽至設定檔總覽頁面，並檢視您組織的設定檔量度。</li><li>**設定檔量度卡**：首頁儀表板中的設定檔量度卡現在會根據您個別的合併原則，顯示您組織中的設定檔總數。</li><li>**結構描述Widget**：您現在可以使用結構描述Widget導覽至UI中的結構描述建立工作流程。</li></ul> |

{style="table-layout:auto"}

**新檔案或更新的檔案**

| 檔案更新 | 說明 |
| --- | --- |
| 新的Real-Time CDP檔案首頁 | 造訪[新Real-Time CDP檔案首頁](/help/rtcdp/home.md)，以取得如何開始使用產品、護欄、範例使用案例等的簡單資訊。 |
| 範例Real-Time CDP使用案例概覽 | 造訪[新範例使用案例概觀頁面](/help/rtcdp/use-case-guides/overview.md)，瞭解貴組織可透過Real-Time CDP實現的範例使用案例集合。 |

{style="table-layout:auto"}

若要深入瞭解Real-Time CDP，請閱讀[Real-Time CDP概觀](../../rtcdp/overview.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶設定檔，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 改善設定檔檢視器預設控制面板卡片的當地語系化 | 預設設定檔卡片現在會有動態當地語系化的名稱。 自訂設定檔卡片可以繼續擁有可編輯的自訂名稱。 |

{style="table-layout:auto"}

若要深入瞭解即時客戶個人檔案，請閱讀[個人檔案總覽](../../profile/home.md)

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 外部產生的對象上傳 | 欄數上限已增加到&#x200B;**25**。 |
| 區段產生器預估 | 預估和合格的設定檔現在會顯示在對象屬性區段中。 如需此變更的詳細資訊，請參閱[區段產生器UI指南](../../segmentation/ui/segment-builder.md)。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite]來源 | 使用來源目錄中的[!DNL Oracle NetSuite]整合，將您[[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)和[[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md)帳戶的資料帶入Experience Platform。 |
| [!BADGE Beta]{type=Informative} [!DNL Braze Currents]來源 | 使用來源目錄中的[[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md)整合，將您[!DNL Braze]帳戶的資料帶入Experience Platform。 |
| 支援[!DNL Snowflake]批次來源的金鑰組驗證 | 您現在可以在建立批次資料的新[!DNL Snowflake]帳戶時使用金鑰組驗證。 如需詳細資訊，請閱讀[使用API](../../sources/tutorials/api/create/databases/snowflake.md)建立 [!DNL Snowflake] 帳戶的指南，或[使用UI](../../sources/tutorials/ui/create/databases/snowflake.md)建立 [!DNL Snowflake] 帳戶的指南。 |

{style="table-layout:auto"}

若要了解有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
