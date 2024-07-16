---
keywords: Experience Platform；首頁；熱門主題；dule；DULE
solution: Experience Platform
title: 資料使用原則概觀
description: 資料使用原則是描述允許或限制您在Adobe Experience Platform中對資料執行的行銷動作型別的規則。
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: e5d90b24dad7faa9aa31c3b0670f8efa69cf0334
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 17%

---

# 資料使用原則概觀 {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="限制資料使用方式"
>abstract="資料使用原則類型會評估套用於資料控管標籤的特定行銷動作，以限制行銷活動的資料使用方式。"

為了使資料使用標籤有效地支援資料合規性，必須實施資料使用原則。 資料使用原則是描述允許或限制您在[!DNL Experience Platform]內對資料執行的行銷動作型別的規則。

有兩種可用的原則：

* **[!UICONTROL 資料治理原則]**：根據正在執行的行銷動作和有問題的資料所攜帶的資料使用標籤，限制資料啟用。
* **[!UICONTROL 同意原則]**：根據您客戶的同意或喜好設定，篩選可啟動至[目的地](../../destinations/home.md)的設定檔

>[!NOTE]
>
>資料使用原則不應與[存取控制原則](../../access-control/abac/end-to-end-guide.md#policy)混淆，後者會決定您組織中的某些Platform使用者是否可以存取某些資料欄位，並透過[!UICONTROL 許可權]索引標籤進行設定。

本檔案提供資料使用原則的高層級概觀，並提供在UI或API中使用原則的其他檔案的連結。

## 行銷動作 {#marketing-actions}

資料控管架構內容中的行銷動作（也稱為行銷使用案例）是[!DNL Experience Platform]資料消費者可以採取的動作，貴組織想要針對這些動作限制資料使用。 因此，以下內容會定義資料使用原則：

1. 特定行銷動作
2. 限制執行該動作的條件

行銷動作的範例可能是想要將資料集匯出至第三方服務。 如果有原則規定無法匯出特定型別的資料(例如個人識別資訊(PII))，而您嘗試匯出包含「I」標籤（身分資料）的資料集，您將會收到[!DNL Policy Service]的回應，告知您資料使用原則已遭違反。

>[!NOTE]
>
>行銷動作本身不會限制資料使用。 它們必須包含在啟用的資料使用原則中，才能針對原則違規評估這些動作。

當貴組織的服務中使用資料時，應指出相關的行銷動作，以便識別任何原則違規。 然後，您可以使用[原則服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/)來檢查整合中的原則違規。

>[!NOTE]
>
>您可以在目的地設定行銷使用案例，以自動化原則執行。 請參閱[目的地檔案](../../destinations/home.md)，以取得有關特定目的地組態選項的詳細資訊。

請參閱本檔案的附錄，以取得[可用Adobe定義的行銷動作](#core-actions)的清單。 您也可以使用[!DNL Policy Service] API或[!DNL Experience Platform]使用者介面來定義您自己的自訂行銷動作。 下一節將提供有關使用行銷動作和原則的詳細資訊。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share audiences with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager audiences are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理資料使用原則 {#manage}

一旦套用資料使用標籤，資料管理員就可以使用[!DNL Policy Service] API或[!DNL Experience Platform] UI來管理和評估針對包含資料使用標籤的資料所採取的行銷動作相關原則。 您可以建立和更新原則、判斷原則的狀態，並搭配行銷動作來評估特定動作是否違反資料使用原則。

>[!IMPORTANT]
>
>所有資料使用原則(包括Adobe提供的核心原則)預設為停用。 為了考慮執行個別原則，您必須透過API或UI手動啟用該原則。

如需在API中使用行銷動作和資料使用原則的逐步指示，請參閱有關[建立和評估資料使用原則](create.md)的教學課程。 如需由[!DNL Policy Service] API提供的金鑰作業的詳細資訊，請參閱[原則服務開發人員指南](../api/getting-started.md)。

有關如何在[!DNL Platform] UI中使用行銷動作和原則的資訊，請參閱[資料使用原則使用手冊](./user-guide.md)。

## 後續步驟

本檔案介紹資料控管架構中的資料使用原則。 您現在可以繼續閱讀本指南中連結的流程檔案，以進一步瞭解如何在API和UI中使用原則。

## 附錄

下節提供有關資料使用原則的其他資訊。

### Adobe定義的行銷動作 {#core-actions}

下表說明可透過Adobe立即使用的核心行銷動作。

>[!NOTE]
>
>應將核心行銷動作視為起點，協助您識別要建立的使用原則並檢查違規。 定義和其解譯方式取決於貴組織的需求和原則。

| 行銷動作 | 說明 |
| --- | --- |
| Analytics | 此動作會將資料用於分析目的，例如衡量、分析和報告客戶對您組織的網站或應用程式的使用情況。 |
| 結合直接可識別的資料 | 此動作會將任何個人識別資訊 (PII) 與匿名資料相結合。來自廣告網路、廣告伺服器和第三方資料提供者的資料合約通常包含明確的合約禁令，禁止將此類資料與可直接識別的資料一起使用。 |
| 跨網站目標定位 | 此動作會將資料用於跨網站廣告目標定位。來自多個網站的資料組合（包括站內資料和站外資料的組合，或來自多個站外來源的資料組合）稱為跨網站資料。 通常會收集和處理跨網站資料，以推斷使用者的興趣。 |
| 資料科學 | 此動作會將資料用於資料科學工作流程。有些合約包含明確禁令，禁止將資料用於資料科學。有時，這些措辭為禁止將資料用於人工智慧 (AI)、機器學習 (ML) 或建模。 |
| 資料匯出 | 此動作會將資料匯出至Adobe產品和服務之外的任何位置或目的地。 例如，下載資料到您的本機電腦、從畫面複製資料、排程將資料傳送到Adobe之外的位置、Customer Journey Analytics已排程的專案、下載報表、報告API等等。 |
| 電子郵件目標定位 | 此動作會將資料用於電子郵件目標定位行銷活動。 |
| 匯出到第三方 | 此動作會將資料匯出至與客戶沒有直接關係的處理器和實體。許多資料提供者在合約中都有條款，禁止從最初收集資料的地方匯出資料。例如，社交網路合約通常會限制傳輸您從他們那裡收到的資料。 |
| 現場Advertising | 此動作會將資料用於站內廣告，包括在您組織的網站或應用程式上選擇和投放廣告，或衡量此類廣告的投放和有效性。 |
| 現場Personalization | 此動作會將資料用於站上內容個人化。 站上個人化是用於推斷使用者興趣的任何資料，並用於根據這些推斷選擇提供哪些內容或廣告。 |
| 區段比對 | 此動作會將資料用於「Adobe Experience Platform區段比對」，可讓兩個或更多Platform使用者交換受眾資料。 透過啟用參考此動作的原則，您可以限制用於區段比對的資料。 例如，如果已啟用核心原則「限制資料共用」，則任何具有[C11標籤](../labels/reference.md#c11)的資料都無法用於區段比對。 |
| 單一身分Personalization | 此動作會要求將單一身分用於個人化目的，而非拼接來自多個來源的身分。 |
