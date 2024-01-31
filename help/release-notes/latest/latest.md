---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2024 年 1 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6ee30e00bceb392b775d15ca2cad95b746698dc4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Platform 發行說明

**發行日期： 2024年1月30日**

Adobe Experience Platform中的新功能：

- [使用案例教戰手冊](#use-case-playbooks)

Experience Platform現有功能的更新：

- [儀表板](#dashboards)
- [資料準備](#data-prep)
- [目的地](#destinations)
- [Real-Time Customer Data Platform](#rtcdp)
- [即時客戶設定檔](#profile)
- [來源](#sources)

## 使用案例教戰手冊 {#use-case-playbooks}

此 [!UICONTROL 使用案例教戰手冊] 功能現已正式開放所有Real-Time CDP和Adobe Journey Optimizer客戶使用。 [!UICONTROL 使用案例教戰手冊] 專門設計來協助使用者在開始使用Real-time Customer Data Platform或Adobe Journey Optimizer時克服挑戰。 當您不確定從何處開始或是如何針對您想要的使用案例建立正確的資產時，使用案例教戰手冊會提供靈感，並建立不同的資產，讓您在準備就緒時測試並匯入生產環境。

開始使用 [!UICONTROL 使用案例教戰手冊]，請閱讀下列檔案頁面：

- 閱讀 [概觀頁面](/help/use-case-playbooks/playbooks/overview.md) 瞭解其用途、可用性資訊，並取得教戰手冊如何運作的端對端示範，從探索到建立執行個體，再到將產生的資產匯入其他沙箱環境。
- 取得所有專案的清單 [可用的教戰手冊](/help/use-case-playbooks/playbooks/playbooks-list.md)，依產品分組(Real-Time CDP或Journey Optimizer)
- 取得所有 [必要許可權](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 使用教戰手冊和教戰手冊產生的資產。
- 瞭解 [資料感知功能](/help/use-case-playbooks/playbooks/data-awareness.md) 可讓您將產生的資產複製到其他沙箱環境
- Get [疑難排解提示](/help/use-case-playbooks/playbooks/troubleshooting.md) 如果您在使用使用案例教戰手冊時遇到錯誤或困難。

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 新的對應工具函數 | <ul><li>`object_to_map`：使用 `object_to_map` 函式以建立對應資料型別。 此函式支援數種不同的語法。 如需詳細資訊，請閱讀以下指南： [階層的函式 — 物件](../../data-prep/functions.md#objects). </li><li>`to_map`：使用 `to_map` 函式以使用物件來建立具有指定欄位名稱和值配對的對應。 如需詳細資訊，請閱讀以下指南： [階層的函式 — 對應](../../data-prep/functions.md#objects). </li><li>`array_to_map`：使用 `array_to_map` 函式，以使用物件陣列來建立具有指定欄位名稱和值組的對應。 如需詳細資訊，請閱讀以下指南： [階層的函式 — 對應](../../data-prep/functions.md#objects). |

{style="table-layout:auto"}

如需「資料準備」的詳細資訊，請閱讀 [資料準備總覽](../../data-prep/home.md).

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 檢視SQL | 您現在可以檢視設定檔、對象、目的地和自訂深入分析背後的SQL，然後透過查詢編輯器依需求執行查詢。 從SQL中汲取超過40種現有的見解靈感，以建立新的查詢，這些查詢會根據您的業務需求從Platform資料中獲得獨特的見解。 如需詳細資訊，請閱讀以下指南： [檢視分析SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂 Widget，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [公用連線](../../destinations/catalog/advertising/pubmatic.md) | 使用此目的地可將受眾資料傳送至 [!DNL PubMatic Connect] 平台。 |

{style="table-layout:auto"}

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## Real-Time Customer Data Platform {#rtcdp}

建置在 Experience Platform、Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 上有助於公司匯集已知和未知的資料，以使用整個客戶歷程中的智慧型決策啟動客戶設定檔。[!DNL Real-Time CDP] 會結合多個企業資料來源以即時建立客戶設定檔。然後，根據這些設定檔建置的區段即可傳送到下游目的地，以便在所有管道和裝置上提供一對一的個人化客戶體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 的更新 [Real-Time CDP首頁](https://experience.adobe.com) | <ul><li>**設定檔Widget**：您現在可以使用設定檔介面工具集導覽至設定檔總覽頁面，並檢視您組織的設定檔量度。</li><li>**設定檔量度卡片**：首頁儀表板中的設定檔量度卡現在會顯示貴組織中的設定檔總數，視您個別的合併原則而定。</li><li>**結構描述Widget**：您現在可以使用結構描述Widget導覽至UI中的結構描述建立工作流程。</li></ul> |

若要進一步瞭解Real-Time CDP，請閱讀 [Real-Time CDP概觀](../../rtcdp/overview.md).

## 即時客戶設定檔 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶設定檔，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 改善設定檔檢視器預設控制面板卡片的當地語系化 | 預設設定檔卡片現在會有動態當地語系化的名稱。 自訂設定檔卡片可以繼續擁有可編輯的自訂名稱。 |

{style="table-layout:auto"}

若要深入瞭解即時客戶個人檔案，請閱讀 [設定檔概述](../../profile/home.md)

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL Oracle NetSuite] 來源 | 使用 [!DNL Oracle NetSuite] 來源目錄中的整合，可從 [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) 和 [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) 要Experience Platform的帳戶。 |
| [!BADGE Beta]{type=Informative}[!DNL Braze Currents] 來源 | 使用 [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) 整合來源目錄，從您的取得資料 [!DNL Braze] 要Experience Platform的帳戶。 |
| 支援的金鑰組驗證 [!DNL Snowflake] 批次來源 | 您現在可以在建立新時使用金鑰組驗證 [!DNL Snowflake] 批次資料的帳戶。 如需詳細資訊，請閱讀以下指南： [建立 [!DNL Snowflake] 使用API的帳戶](../../sources/tutorials/api/create/databases/snowflake.md) 或指南 [建立 [!DNL Snowflake] 使用UI的帳戶](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

若要了解有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。