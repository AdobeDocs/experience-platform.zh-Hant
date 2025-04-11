---
title: Adobe Experience Platform 發行說明 (2024 年 1 月)
description: Adobe Experience Platform 2024 年 1 月版發行說明。
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: ht
source-wordcount: '1662'
ht-degree: 100%

---

# Adobe Experience Platform 發行說明

**發行日期：2024 年 1 月 30 日**

Adobe Experience Platform 的新功能：

- [使用案例教戰手冊](#use-case-playbooks)

Experience Platform 現有功能的更新：

- [屬性型存取控制](#abac)
- [資料準備](#data-prep)
- [儀表板](#dashboards)
- [目標](#destinations)
- [身分識別服務](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [即時客戶設定檔](#profile)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 使用案例教戰手冊 {#use-case-playbooks}

「[!UICONTROL 使用案例教戰手冊]」功能現在已正式推出，可供所有 Real-Time CDP 及 Adobe Journey Optimizer 的客戶使用。「[!UICONTROL 使用案例教戰手冊]」旨在協助使用者克服開始使用 Real-Time Customer Data Platform 或 Adobe Journey Optimizer 時遇到的挑戰。當您不確定要從哪裡開始或如何為所需的使用案例建立正確資產時，使用案例教戰手冊能夠提供靈感和建立不同的資產供您測試，並在準備好時匯入到生產環境中。

若要開始使用「[!UICONTROL 使用案例教戰手冊]」，請閱讀以下文件頁面：

- 閱讀[概觀頁面](/help/use-case-playbooks/playbooks/overview.md)以了解其目的、可用性資訊，並取得教戰手冊運作方式的端對端示範，包括從發現到建立實例，再到將產生的資產匯入至其他沙箱環境等。
- 取得依產品分類的所有[可用教戰手冊](/help/use-case-playbooks/playbooks/playbooks-list.md)清單 (Real-Time CDP 或 Journey Optimizer)
- 取得有關所有[必要權限](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions)的資訊，以利用教戰手冊及其產生的資產。
- 了解[資料感知功能](/help/use-case-playbooks/playbooks/data-awareness.md)；該功能可讓您將產生的資產複製到其他沙箱環境中
- 如果您在運用使用案例教戰手冊時遇到錯誤或困難，可以取得[疑難排解提示](/help/use-case-playbooks/playbooks/troubleshooting.md)。

## 屬性型存取控制 {#abac}

屬性型存取控制是 Adob&#x200B;&#x200B;e Experience Platform 的一項功能，此平台為注重隱私的品牌提供更大的靈活性來管理使用者存取。可以將結構描述欄位和分段等個別物件指派給使用者角色。此功能可讓您授予或撤銷貴組織中特定 Experience Platform 使用者對個別物件的存取權。

透過屬性型存取控制，您組織的管理員可以在所有 Experience Platform 工作流程及資源中，控制使用者對敏感個人資料 (SPD)、個人身分識別資訊 (PII) 和其他自訂類型資料的存取權。管理員可以將使用者角色定義為只能存取特定欄位及這些欄位對應的資料。

**新文件或更新的文件**

| 文件更新 | 說明 |
| --- | --- |
| 針對屬性型存取控制記錄新的 API 端點 | [存取控制 API 參考文件](https://developer.adobe.com/experience-platform-apis/references/access-control/)現在包含屬性型存取控制 API 角色、政策及產品端點。這些端點可用來獲取特定沙箱中指定資源之使用者的相關角色、政策及產品。 |

{style="table-layout:auto"}

若要了解更多關於屬性型存取控制，請參閱[屬性型存取控制概觀](../../access-control/abac/overview.md)。關於屬性型存取控制工作流程的綜合指南，請閱讀[屬性型存取控制端對端指南](../../access-control/abac/end-to-end-guide.md)。

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 新的對應工具函數 | <ul><li>`object_to_map`：使用 `object_to_map` 函數可建立對應資料類型。此函數支援多種不同的語法。如需詳細資訊，請參閱[階層函數 - 物件](../../data-prep/functions.md#objects)的指南。 </li><li>`to_map`：使用 `to_map` 函數可透過物件來建立具有指定欄位名稱和數值組的對應。如需詳細資訊，請閱讀[階層函數 - 對應](../../data-prep/functions.md#map)的指南。 </li><li>`array_to_map`：使用 `array_to_map` 函數可透過物件陣列來建立具有指定欄位名稱和數值組的對應。如需詳細資訊，請閱讀[階層函數 - 對應](../../data-prep/functions.md#map)的指南。 |

{style="table-layout:auto"}

如需有關資料準備的詳細資訊，請閱讀[資料準備概觀](../../data-prep/home.md)。

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 檢視 SQL | 您現在可以使用「檢視 SQL」切換鈕檢視設定檔、客群、目標和自訂深入解析背後的 SQL，然後透過查詢編輯器隨選執行查詢。存取為 Real-time Customer Data Platform 深入解析提供支援的 SQL，可協助您了解資料模型分析背後的邏輯。這種透明度可讓您的 Adobe Real-time CDP 資料更易於存取和理解，並對決策產生影響。<br>從 40 多個現有深入分析的 SQL 中汲取靈感，然後建立新的查詢，以根據您的業務需求從 Experience Platform 資料中獲得獨特的深入分析。SQL 也可用於 Experience League 文件中的[設定檔](../../dashboards/insights/profiles.md)、[客群](../../dashboards/insights/audiences.md)，以及[目標](../../dashboards/insights/destinations.md)深入解析。這些文件特別介紹了能夠透過標準深入解析來回應的業務使用案例。如需詳細資訊，請閱讀[檢視 SQL 深入解析](../../dashboards/view-sql.md)的指南。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂小工具，請先閱讀[儀表板概觀](../../dashboards/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目標** {#new-destinations}

| 目標 | 說明 |
| ----------- | ----------- |
| [Pubmatic 連線](../../destinations/catalog/advertising/pubmatic.md) | 使用此目標可將客群資料傳送至 [!DNL PubMatic Connect] 平台。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| Amazon S3 目標的新&#x200B;**假定角色**&#x200B;驗證類型 | 如果您不想與 Experience Platform 共用帳戶金鑰和私密金鑰，則在將 Experience Platform 連線到 Amazon S3 貯體時，請使用新的假定角色驗證類型。請到 Amazon S3 文件的[驗證區段](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication)閱讀更多有關新驗證方法的資訊。 |

{style="table-layout:auto"}

如需更多有關目標的一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 身分識別服務 {#identity-service}

Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。

**新文件或更新的文件**

| 文件更新 | 說明 |
| --- | --- |
| 文件重組 | 身分識別服務文件已經過重組，以改善身分識別服務中概念的呈現和清晰度：<ul><li>造訪[身分識別服務概觀頁面](../../identity-service/home.md)可取得擴充的術語指南、詳細說明典型客戶歷程的使用案例範例、身分識別服務如何將身分識別連結在一起的詳細介紹，以及身分識別服務在 Experience Platform 生態系中扮演之角色的摘要。</li><li>閱讀[了解身分識別服務和即時客戶設定檔之間的關係](../../identity-service/identity-and-profile.md)指南，即可詳細了解這兩種服務如何協同運作，以及其目的、流程、輸入和輸出方面的不同之處。</li><li>參閱[身分識別服務連結邏輯指南](../../identity-service/features/identity-linking-logic.md)，即可透過說明和視覺效果來了解身分識別圖在特定場景與時間戳記下會如何運作。</li></ul> |

{style="table-layout:auto"}

若要了解更多有關身分識別服務的資訊，請閱讀[身分識別服務概觀](../../identity-service/home.md)。

## Real-Time Customer Data Platform {#rtcdp}

建置在 Experience Platform、Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 上有助於公司匯集已知和未知的資料，以使用整個客戶歷程中的智慧型決策啟動客戶設定檔。[!DNL Real-Time CDP] 會結合多個企業資料來源以即時建立客戶設定檔。然後，根據這些設定檔建置的區段即可傳送到下游目標，以便在所有管道和裝置上提供一對一的個人化客戶體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [Real-Time CDP 首頁](https://experience.adobe.com)的更新 | <ul><li>**設定檔小工具**：您現在可以使用設定檔小工具導覽至設定檔概觀頁面，並檢視您組織的設定檔量度。</li><li>**設定檔量度卡片**：視您個別的合併原則而定，首頁儀表板中的設定檔量度卡片現在會顯示組織中的設定檔總數。</li><li>**結構描述小工具**：您現在可以使用結構描述小工具導覽至使用者介面中的結構描述建立工作流程。</li></ul> |

{style="table-layout:auto"}

**新文件或更新的文件**

| 文件更新 | 說明 |
| --- | --- |
| 新的 Real-Time CDP 文件首頁 | 造訪[新的 Real-Time CDP 文件首頁](/help/rtcdp/home.md)可了解如何開始使用產品、護欄、使用案例樣本等概覽資訊。 |
| Real-Time CDP 使用案例樣本概觀 | 造訪[新的使用案例樣本概觀頁面](/help/rtcdp/use-case-guides/overview.md)，可取得您組織能夠透過 Real-Time CDP 實現的使用案例樣本集合。 |

{style="table-layout:auto"}

若要深入了解 Real-Time CDP，請閱讀 [Real-Time CDP 概觀](../../rtcdp/overview.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶設定檔，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 改善設定檔檢視器之預設儀表板卡片的本地化 | 預設的設定檔卡片現在會有透過動態方式本地化的名稱。自訂設定檔卡片可以繼續使用可編輯的自訂名稱。 |

{style="table-layout:auto"}

若要深入了解即時客戶設定檔，請閱讀[設定檔概觀](../../profile/home.md)

## 細分服務 {#segmentation}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 外部產生的客群上傳 | 最大欄數已增加至 **25**。 |
| 客戶細分工具預估 | 預估和符合資格的設定檔現在會顯示在客群屬性區段中。如需有關此變更的詳細資訊，請閱讀[客戶細分工具使用者介面指南](../../segmentation/ui/segment-builder.md)。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[細分概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite] 來源 | 使用來源目錄中的 [!DNL Oracle NetSuite] 整合可將資料從您的 [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) 和 [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) 帳戶帶至 Experience Platform。 |
| [!BADGE Beta]{type=Informative} [!DNL Braze Currents] 來源 | 使用來源目錄中的 [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) 整合可將資料從您的 [!DNL Braze] 帳戶帶至 Experience Platform。 |
| 支援 [!DNL Snowflake] 批次來源的金鑰組驗證 | 現在起，您為批次資料建立新的 [!DNL Snowflake] 帳戶時，可以使用金鑰組驗證了。如需詳細資訊，請閱讀[使用 API 建立 [!DNL Snowflake] 帳戶](../../sources/tutorials/api/create/databases/snowflake.md)的指南，或[透過使用者介面建立 [!DNL Snowflake] 帳戶](../../sources/tutorials/ui/create/databases/snowflake.md)的指南。 |

{style="table-layout:auto"}

若要深入了解來源，請閱讀[來源概觀](../../sources/home.md)。
