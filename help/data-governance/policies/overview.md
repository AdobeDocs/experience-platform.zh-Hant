---
keywords: Experience Platform；首頁；熱門主題；模組；DULE
solution: Experience Platform
title: 資料使用策略概述
description: 資料使用策略是描述允許或限制您對Adobe Experience Platform內的資料執行的市場營銷操作類型的規則。
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 2%

---

# 資料使用策略概述 {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="限制資料使用方式"
>abstract="資料使用原則類型會評估套用於資料控管標籤的特定行銷動作，以限制行銷活動的資料使用方式。"

為了使資料使用標籤有效地支援資料合規性，必須實施資料使用策略。 資料使用策略是描述允許或限制您對內部資料執行的市場營銷操作類型的規則 [!DNL Experience Platform]。

可用策略有兩種類型：

* **[!UICONTROL 資料治理策略]**:根據正在執行的營銷活動和由有關資料攜帶的資料使用標籤限制資料激活。
* **[!UICONTROL 同意政策]**:篩選可激活的配置檔案 [目的地](../../destinations/home.md) 根據客戶的同意或偏好

>[!NOTE]
>
>不要將資料使用策略與 [訪問控制策略](../../access-control/abac/end-to-end-guide.md#policy)，確定組織中的某些平台用戶是否可以訪問某些資料欄位，並通過 [!UICONTROL 權限] 頁籤。

本文檔提供資料使用策略的高級概述，並提供指向在UI或API中使用策略的進一步文檔的連結。

## 市場營銷操作 {#marketing-actions}

在資料治理框架中的市場營銷操作（也稱為市場營銷使用案例）是 [!DNL Experience Platform] 資料使用者可以採用，您的組織希望限制其資料使用。 因此，資料使用策略由以下定義：

1. 特定市場營銷操作
2. 限制執行該操作的條件

市場營銷操作的一個示例可能是希望將資料集導出到第三方服務。 如果有策略表明無法導出特定類型的資料(如個人身份資訊(PII))，並且您嘗試導出包含「I」標籤（身份資料）的資料集，您將收到來自 [!DNL Policy Service] 告訴您資料使用策略已被違反。

>[!NOTE]
>
>市場營銷活動本身不限制資料使用。 必須將它們包含在已啟用的資料使用策略中，以便評估策略違規的這些操作。

當組織服務中發生資料使用情況時，應指明相關的市場營銷活動，以便確定任何違反策略的行為。 然後，您可以使用 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 檢查整合中是否存在策略違規。

>[!NOTE]
>
>您可以在目標上設定市場營銷使用案例以自動執行策略。 查看 [目標文檔](../../destinations/home.md) 的子菜單。

請參閱本文檔的附錄，瞭解 [可用Adobe定義的市場營銷操作](#core-actions)。 您還可以使用 [!DNL Policy Service] API或 [!DNL Experience Platform] 用戶介面。 下一節提供了有關使用市場營銷活動和策略的更多資訊。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理資料使用策略 {#manage}

一旦應用了資料使用標籤，資料管理員就可以使用 [!DNL Policy Service] API或 [!DNL Experience Platform] UI，用於管理和評估與對包含資料使用標籤的資料執行的市場營銷操作相關的策略。 您可以建立和更新策略，確定策略的狀態，並使用市場營銷活動來評估特定活動是否違反了資料使用策略。

>[!IMPORTANT]
>
>預設情況下，所有資料使用策略(包括由Adobe提供的核心策略)都被禁用。 要考慮實施單個策略，必須通過API或UI手動啟用該策略。

有關在API中使用市場營銷操作和資料使用策略的逐步說明，請參見上的教程 [建立和評估資料使用策略](create.md)。 有關詳細資訊，請參閱 [!DNL Policy Service] API，請參見 [策略服務開發人員指南](../api/getting-started.md)。

有關如何使用中的市場營銷操作和策略的資訊 [!DNL Platform] UI，請參見 [資料使用策略使用手冊](./user-guide.md)。

## 後續步驟

本文檔介紹了資料治理框架中的資料使用策略。 現在，您可以繼續閱讀本指南中連結到的流程文檔，以瞭解如何在API和UI中使用策略。

## 附錄

以下部分提供了有關資料使用策略的其他資訊。

### Adobe定義的市場營銷活動 {#core-actions}

下表介紹了通過Adobe提供的現成核心營銷活動。

>[!NOTE]
>
>應將核心營銷活動視為幫助您確定要建立和檢查違規的使用策略的起點。 定義及其解釋方式取決於您組織的需要和策略。

| 營銷活動 | 說明 |
| --- | --- |
| Analytics | 將資料用於分析目的的操作，如測量、分析和報告客戶對您組織的站點或應用的使用情況。 |
| 與直接可識別的資料組合 | 將任何個人身份資訊(PII)與匿名資料相結合的操作。 從廣告網路、廣告伺服器和第三方資料提供商獲取的資料合同通常包括禁止使用直接可識別資料的此類資料的具體合同。 |
| 跨站點目標 | 使用資料進行跨站點廣告目標的操作。 來自多個站點的資料的組合，包括現場資料和非現場資料的組合或來自多個非現場源的資料的組合，稱為跨站點資料。 通常收集和處理跨站點資料以推斷用戶的興趣。 |
| 資料科學 | 將資料用於資料科學工作流的操作。 一些合同明確禁止資料科學的資料使用。 有時，這些措辭是禁止使用人工智慧(AI)、機器學習(ML)或建模的資料。 |
| 電子郵件目標 | 在電子郵件目標市場活動中使用資料的操作。 |
| 導出到第三方 | 將資料導出到與客戶沒有直接關係的處理器和實體的操作。 許多資料提供者在合同中有禁止從最初收集的地方導出資料的條款。 例如，社交網路合同通常會限制您從這些合同接收到的資料的傳輸。 |
| 現場廣告 | 使用資料進行現場廣告的操作，包括在您組織的網站或應用上選擇和交付廣告，或衡量此類廣告的交付和效果。 |
| 現場個性化 | 使用資料實現現場內容個性化的操作。 現場個性化是用於推斷用戶興趣的任何資料，並用於根據這些推斷選擇提供哪些內容或廣告。 |
| 段匹配 | 使用Adobe Experience Platform段匹配資料的操作，允許兩個或更多平台用戶交換段資料。 通過啟用引用此操作的策略，您可以限制用於段匹配的資料。 例如，如果啟用了核心策略「限制資料共用」，則具有 [C11標籤](../labels/reference.md#c11) 不能用於段匹配。 |
| 單個身份個性化 | 要求將單個標識用於個性化目的而不是從多個源拼接標識的操作。 |
