---
keywords: Experience Platform;home；熱門主題；dule;DULE
solution: Experience Platform
title: 資料使用政策概觀
topic-legacy: policies
description: 為了讓資料使用標籤有效支援資料合規性，必須實作資料使用政策。 資料使用原則是描述您允許或限制對Experience Platform內資料執行之行銷動作類型的規則。
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# 資料使用政策概觀

為了讓資料使用標籤有效支援資料合規性，必須實作資料使用政策。 資料使用原則是描述您可對[!DNL Experience Platform]內的資料執行或受限制之行銷動作的類型的規則。

本檔案提供資料使用原則的高階概述，並提供在UI或API中使用原則的進一步檔案連結。

## 行銷動作{#marketing-actions}

資料治理架構中的行銷動作（也稱為行銷使用案例）是[!DNL Experience Platform]資料使用者可採取的動作，您的組織想要限制資料使用。 因此，資料使用原則由下列項目定義：

1. 特定行銷動作
2. 限制動作的資料使用標籤

行銷動作的範例可能是想要將資料集匯出至第三方服務。 如果有原則指出無法匯出特定資料類型(例如個人識別資訊(PII))，且您嘗試匯出包含&quot;I&quot;標籤（身分資料）的資料集，您會收到[!DNL Policy Service]的回應，告知您資料使用原則已遭違反。

>[!NOTE]
>
>行銷動作本身並不限制資料使用。 必須將它們納入已啟用的資料使用策略中，才能針對策略違規評估這些操作。

當組織的服務中發生資料使用情形時，應指出相關的行銷動作，以便識別任何違反原則的行為。 然後，您可以使用[原則服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)來檢查整合中是否有違反原則的情況。

>[!NOTE]
>
>如果您使用[!DNL Real-time Customer Data Platform]，則可在目標上設定行銷使用案例，以自動執行原則。 有關詳細資訊，請參見[即時CDP中的資料治理文檔。](../../rtcdp/privacy/data-governance-overview.md)

有關[可用的Adobe定義行銷動作](#core-actions)的清單，請參閱本檔案附錄。 您也可以使用[!DNL Policy Service] API或[!DNL Experience Platform ]使用者介面來定義您自己的自訂行銷動作。 有關使用行銷動作和政策的詳細資訊，請參閱下一節。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理資料使用策略{#manage}

在套用資料使用標籤後，資料管理員可使用[!DNL Policy Service] API或[!DNL Experience Platform] UI來管理和評估對包含資料使用標籤的資料所執行的行銷動作相關政策。 您可以建立和更新原則、決定原則的狀態，以及使用行銷動作來評估特定動作是否違反資料使用原則。

>[!IMPORTANT]
>
>所有資料使用原則(包括Adobe提供的核心原則)預設會停用。 若要考慮實施個別原則，您必須透過API或UI手動啟用該原則。

如需在API中使用行銷動作和資料使用原則的逐步指示，請參閱[建立和評估資料使用原則的教學課程](create.md)。 有關[!DNL Policy Service] API提供的關鍵操作的詳細資訊，請參閱[策略服務開發人員指南](../api/getting-started.md)。

有關如何在[!DNL Platform] UI中使用行銷動作和原則的資訊，請參閱[資料使用原則使用指南](./user-guide.md)。

## 後續步驟

本檔案介紹了[!DNL Data Governance]框架中的資料使用策略。 您現在可以繼續閱讀本指南中連結的流程檔案，以進一步瞭解如何在API和UI中使用原則。

## 附錄

下節提供資料使用原則的其他資訊。

### Adobe定義的行銷動作{#core-actions}

下表說明由Adobe提供的現成可用的核心行銷動作。

>[!NOTE]
>
>核心行銷動作應視為起點，以協助您識別要建立和檢查違規的使用政策。 定義及其解讀方式取決於貴組織的需求和政策。

| 行銷動作 | 說明 |
| --- | --- |
| Analytics | 將資料用於分析目的的動作，例如測量、分析和報告客戶對您組織網站或應用程式的使用情形。 |
| 與PII結合 | 結合任何個人識別資訊(PII)與匿名資料的動作。 來自廣告網路、廣告伺服器和第三方資料供應商的資料合約通常包含特定合約禁止在直接可識別資料的情況下使用此類資料。 |
| 跨網站定位 | 使用資料進行跨網站廣告定位的動作。 數個網站的資料組合（包括現場資料與非現場資料的組合，或數個非現場來源的資料組合）稱為跨網站資料。 跨網站資料通常會收集並處理，以做出使用者興趣的推論。 |
| 資料科學 | 資料科學工作流程中使用資料的動作。 有些合約明確禁止資料科學的資料使用。 有時，這些措辭的措辭會禁止為人工智慧(AI)、機器學習(ML)或模型使用資料。 |
| 電子郵件定位 | 在電子郵件定位促銷活動中使用資料的動作。 |
| 匯出至第三方 | 一種將資料導出到與客戶沒有直接關係的處理器和實體的操作。 許多資料提供者在合約中都有條款禁止從原始收集位置匯出資料。 例如，社交網路合約通常會限制您從其接收到的資料傳輸。 |
| 現場廣告 | 使用資料進行現場廣告的動作，包括在您組織的網站或應用程式上選擇和發佈廣告，或測量此類廣告的發佈和效果。 |
| Onsite個人化 | 使用資料進行站上內容個人化的動作。 Onsite個人化是用於推論使用者興趣的任何資料，並用於根據這些推論選擇提供哪些內容或廣告。 |
| 單一身分個人化 | 需要將單一身分識別用於個人化目的，而非從多個來源聯繫身分的動作。 |
