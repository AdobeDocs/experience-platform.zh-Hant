---
keywords: Experience Platform；首頁；熱門主題；dule;DULE
solution: Experience Platform
title: 資料使用原則概述
description: 資料使用原則是描述您可在Adobe Experience Platform內對資料執行或限制執行的行銷動作類型的規則。
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# 資料使用原則概觀 {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="限制資料使用"
>abstract="資料使用政策類型會評估套用至資料控管標籤的特定行銷動作，以限制行銷活動的資料使用。"

為了讓資料使用標籤有效支援資料合規性，必須實施資料使用策略。 資料使用原則是描述您可對內的資料執行或限制的行銷動作類型的規則 [!DNL Experience Platform].

可用的策略有兩種類型：

* **[!UICONTROL 資料控管原則]**:根據執行的行銷動作和相關資料所攜帶的資料使用標籤，限制資料啟動。
* **[!UICONTROL 同意政策]**:篩選可啟動至的設定檔 [目的地](../../destinations/home.md) 根據客戶的同意或偏好

>[!NOTE]
>
>資料使用原則不應與 [訪問控制策略](../../access-control/abac/end-to-end-guide.md#policy)，可決定貴組織中的某些Platform使用者能否存取特定資料欄位，並透過 [!UICONTROL 權限] 標籤。

本檔案提供資料使用原則的概觀，並提供在UI或API中使用原則的進一步檔案連結。

## 行銷動作 {#marketing-actions}

在資料控管架構中，行銷動作（又稱為行銷使用案例）是 [!DNL Experience Platform] 資料使用者可採用，而您的組織想要限制資料使用量。 因此，資料使用策略由以下項定義：

1. 特定行銷動作
2. 限制執行該動作的條件

行銷動作的範例可能是想要將資料集匯出至協力廠商服務。 如果有原則指出無法匯出特定類型的資料(例如個人識別資訊(PII))，而您嘗試匯出包含「I」標籤（身分資料）的資料集，您會收到來自 [!DNL Policy Service] 告訴您資料使用原則已遭違反。

>[!NOTE]
>
>行銷動作本身並不會限制資料使用。 必須將它們包含在啟用的資料使用策略中，以便針對違反策略的情況評估這些操作。

當貴組織的服務中發生資料使用情形時，應指出相關的行銷動作，以便識別任何違反政策的行為。 然後，您就可以使用 [策略服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 來檢查整合中是否有違反原則的情況。

>[!NOTE]
>
>您可以在目的地上設定行銷使用案例，以自動執行原則。 請參閱 [目的地檔案](../../destinations/home.md) 以取得特定目的地的設定選項的詳細資訊。

如需 [可用Adobe定義的行銷動作](#core-actions). 您也可以使用 [!DNL Policy Service] API或 [!DNL Experience Platform] 使用者介面。 有關使用行銷動作和政策的詳細資訊，請參閱下一節。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理資料使用策略 {#manage}

在套用資料使用量標籤後，資料管理員可使用 [!DNL Policy Service] API或 [!DNL Experience Platform] 管理及評估針對包含資料使用標籤之資料所採取行銷動作之相關原則的UI。 您可以建立和更新原則、判斷原則的狀態，以及使用行銷動作來評估特定動作是否違反資料使用原則。

>[!IMPORTANT]
>
>預設會停用所有資料使用原則(包括Adobe提供的核心原則)。 為了將個別原則視為執行，您必須透過API或UI手動啟用該原則。

如需在API中使用行銷動作和資料使用原則的逐步指示，請參閱 [建立和評估資料使用策略](create.md). 如需詳細資訊，請參閱 [!DNL Policy Service] API，請參閱 [策略服務開發人員指南](../api/getting-started.md).

有關如何使用 [!DNL Platform] UI，請參閱 [資料使用原則使用指南](./user-guide.md).

## 後續步驟

本檔案介紹資料控管架構中的資料使用政策。 您現在可以繼續閱讀本指南中連結的程式檔案，以進一步了解如何在API和UI中使用原則。

## 附錄

以下章節提供資料使用原則的其他資訊。

### Adobe定義的行銷動作 {#core-actions}

下表說明由Adobe提供的現成核心行銷動作。

>[!NOTE]
>
>核心行銷動作應視為起點，協助您識別要建立和檢查違規的使用原則。 定義及其解讀方式取決於貴組織的需求和原則。

| 行銷動作 | 說明 |
| --- | --- |
| Analytics | 將資料用於分析用途的動作，例如測量、分析和報告客戶對您組織網站或應用程式的使用情形。 |
| 結合可直接識別的資料 | 結合任何個人識別資訊(PII)與匿名資料的動作。 來自廣告網路、廣告伺服器和第三方資料提供者的資料合約通常包含特定合約禁止將這類資料與可直接識別的資料搭配使用。 |
| 跨網站鎖定 | 使用資料進行跨網站廣告鎖定的動作。 來自多個網站的資料組合（包括站上資料和離站資料的組合，或來自多個離站來源的資料組合）稱為跨網站資料。 通常會收集並處理跨網站資料，以便對使用者的興趣做出推論。 |
| 資料科學 | 將資料用於資料科學工作流程的動作。 有些合同明確禁止資料科學使用資料。 有時，這些措辭的措辭禁止將資料用於人工智慧(AI)、機器學習(ML)或建模。 |
| 電子郵件目標定位 | 在電子郵件目標定位促銷活動中使用資料的動作。 |
| 匯出至第三方 | 將資料導出到與客戶沒有直接關係的處理器和實體的操作。 許多資料提供者在合約中都有條款，禁止從最初收集到的資料的地方導出資料。 例如，社交網路合約通常會限制您從這些合約收到的資料傳輸。 |
| 站上廣告 | 將資料用於站上廣告的動作，包括在您組織的網站或應用程式上選擇和投放廣告，或用來評估這類廣告的投放和效果。 |
| 站上個人化 | 使用資料進行站上內容個人化的動作。 Onsite個人化是用於推斷使用者興趣的任何資料，用來根據這些推斷選取提供哪些內容或廣告。 |
| 區段符合 | 使用Adobe Experience Platform區段比對資料的動作，可讓兩位或多位Platform使用者交換區段資料。 啟用可參考此動作的原則，即可限制要用於區段比對的資料。 例如，如果啟用核心原則「限制資料共用」，則任何具有 [C11標籤](../labels/reference.md#c11) 無法用於「區段符合」。 |
| 單一身分個人化 | 此動作需要使用單一身分來進行個人化目的，而非從多個來源連結身分。 |
