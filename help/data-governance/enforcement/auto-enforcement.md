---
keywords: Experience Platform；首頁；熱門主題；策略實施；自動實施；基於API的實施；資料治理
solution: Experience Platform
title: 自動策略強制
topic-legacy: guide
description: 本文檔介紹在將段激活到Experience Platform中的目標時如何自動強制實施資料使用策略。
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: ca35b1780db00ad98c2a364d45f28772c27a4bc3
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 0%

---

# 自動策略強制

一旦標籤了資料並定義了使用策略，您就可以強制資料使用與策略的一致性。 在將受眾段激活到目標時，Adobe Experience Platform會在發生任何違規時自動實施使用策略。

## 先決條件

本指南要求對參與自動強制實施的平台服務進行工作理解。 在繼續閱讀本指南之前，請參閱以下文檔以瞭解更多資訊：

* [Adobe Experience Platform資料治理](../home.md):平台通過使用標籤和策略來實施資料使用合規性的框架。
* [即時客戶概要資訊](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [Adobe Experience Platform分段服務](../../segmentation/home.md):分段引擎 [!DNL Platform] 用於根據客戶行為和屬性從客戶配置檔案建立受眾段。
* [目標](../../destinations/home.md):目標是預構建的與常用應用程式的整合，允許從平台無縫激活資料，用於跨渠道營銷活動、電子郵件活動、目標廣告等。

## 強制流 {#flow}

下圖說明了如何將策略實施整合到段激活的資料流中：

![](../images/enforcement/enforcement-flow.png)

當首次激活段時， [!DNL Policy Service] 根據以下因素檢查適用的策略：

* 應用於要激活的段內的欄位和資料集的資料使用標籤。
* 目標的市場營銷目的。
<!-- * (Beta) The profiles that have consented to be included in the segment activation, based on your configured consent policies. -->

>[!NOTE]
>
>如果資料使用標籤僅應用於資料集（而不是整個資料集）中的某些欄位，則只有在以下條件下才會在激活時強制執行這些欄位級別標籤：
>
>* 欄位用於段定義。
>* 這些欄位被配置為目標目標的投影屬性。


## 資料沿襲 {#lineage}

資料沿襲在平台中如何實施策略方面起著關鍵作用。 一般來說，資料沿襲是指一組資料的源，以及資料隨時間的變化（或移動的位置）。

在資料治理的上下文中，沿襲使資料使用標籤能夠從資料集傳播到使用其資料的下游服務，如即時客戶配置檔案和目標。 這允許在資料通過平台過程中的幾個關鍵點對策略進行評估和實施，並為資料使用者提供關於發生策略違規原因的上下文。

在Experience Platform中，策略執行涉及以下血統：

1. 資料被引入平台並儲存在 **資料集**。
1. 通過根據資料集合資料片段來識別和構建客戶配置檔案 **合併策略**。
1. 將簡檔組分為 **段** 基於公共屬性。
1. 段被激活到下游 **目的地**。

上述時間表中的每個階段都表示一個實體，該實體可能會導致違反的策略，如下表所述：

| 資料沿襲階段 | 策略執行中的角色 |
| --- | --- |
| 資料集 | 資料集包含資料使用標籤（應用於資料集或欄位級別），這些標籤定義了整個資料集或特定欄位可用於哪些使用案例。 如果將包含某些標籤的資料集或欄位用於策略限制的目的，則將發生策略違規。 |
| 合併策略 | 合併策略是平台用於確定合併多個資料集的片段時資料優先順序的規則。 如果將合併策略配置為將帶有限制標籤的資料集激活到目標，則將發生策略違規。 查看 [合併策略概述](../../profile/merge-policies/overview.md) 的子菜單。 |
| 區段 | 段規則定義應從客戶配置檔案中包括哪些屬性。 根據段定義包括哪些欄位，段將繼承這些欄位的所有已應用用法標籤。 如果您根據目標目標的市場營銷使用案例激活其繼承標籤受其適用策略限制的段，則將發生策略違規。 |
| 目的地 | 在設定目標時，可以定義市場營銷活動（有時稱為市場營銷使用案例）。 此使用情形與策略中定義的市場營銷活動相關。 換句話說，您為目標定義的市場營銷使用案例決定了哪些資料使用策略和同意策略適用於該目標。 如果激活的段的使用標籤受目標目標的適用策略的限制，則將發生策略違規。 |
<!-- | Dataset | Datasets contain data usage labels (applied at the dataset or field level) that define which use cases the entire dataset or specific fields can be used for. Policy violations will occur if a dataset or field containing certain labels is used for a purpose that a policy restricts.<br><br>Any consent attributes collected from your customers are also stored in datasets. If you have access to [consent policies](../policies/user-guide.md#consent-policy) (currently in beta), any profiles that do not meet the consent attribute requirements of your policies will be excluded from segments that are activated to a destination. | -->
<!-- | Segment | Segment rules define which attributes should be included from customer profiles. Depending on which fields a segment definition includes, the segment will inherit any applied usage labels for those fields. Policy violations will occur if you activate a segment whose inherited labels are restricted by the target destination's applicable policies, based on its marketing use case. | -->

>[!IMPORTANT]
>
>某些資料使用策略可以指定兩個或多個具有AND關係的標籤。 例如，策略可以在標籤時限制市場營銷操作 `C1` 和 `C2` 都存在，但不限制同一操作（如果只存在其中一個標籤）。
>
>在自動強制方面，資料治理框架不將激活單獨的資料段作為資料的組合用於目標。 所以，這個例子 `C1 AND C2` 策略 **不** 如果這些標籤包含在單獨的段中，則強制執行。 相反，僅當激活時兩個標籤都位於同一段時，才強制執行此策略。

當發生策略違規時，UI中顯示的結果消息將提供有用的工具，用於探查違規的貢獻資料沿襲，以幫助解決問題。 下一節提供了更多詳細資訊。

## 策略違規消息 {#enforcement}

<!-- (TO INCLUDE FOR PHASE 2)
The sections below outline the different policy enforcement messages that appear in the Platform UI:

* [Data usage policy violation](#data-usage-violation)
* [Consent policy evaluation](#consent-policy-evaluation)

### Data usage policy violation {#data-usage-violation} -->

如果嘗試激活段(或 [對已激活的段進行編輯](#policy-enforcement-for-activated-segments))操作被阻止，並出現一個跨距，指示已違反一個或多個策略。 一旦觸發違規， **[!UICONTROL 保存]** 按鈕將被禁用，直到相應元件更新為符合資料使用策略。

在跨距的左列中選擇策略違規以顯示該違規的詳細資訊。

![](../images/enforcement/violation-policy-select.png)

違規消息提供了違反的策略的摘要，包括策略配置為檢查的條件、觸發違規的特定操作以及問題的可能解決方案清單。

![](../images/enforcement/violation-summary.png)

違規概要下方顯示資料沿襲圖，使您能夠直觀地顯示哪些資料集、合併策略、段和目標與策略違規有關。 您當前正在更改的實體在圖形中加亮顯示，指示流中的哪個點導致違規發生。 可以在圖形中選擇實體名稱，以開啟有關實體的詳細資訊頁面。

![](../images/enforcement/data-lineage.png)

您還可以使用 **[!UICONTROL 篩選]** 表徵圖。![](../images/enforcement/filter.png))按類別篩選顯示的實體。 至少必須選擇兩個類別才能顯示資料。

![](../images/enforcement/lineage-filter.png)

選擇 **[!UICONTROL 清單視圖]** 將資料沿襲顯示為清單。 要切換回可視圖形，請選擇 **[!UICONTROL 路徑視圖]**。

![](../images/enforcement/list-view.png)

<!-- (TO INCLUDE FOR PHASE 2)
### Consent policy evaluation (Beta) {#consent-policy-evaluation}

>[!IMPORTANT]
>
>Consent policies are currently in beta and your organization may not have access to them yet.

If you have [created consent policies](../policies/user-guide.md#consent-policy) and are activating a segment to a destination, you can see how your consent policies will affect the percentage of profiles that will be included in the activation.

Once you reach at the **[!UICONTROL Review]** step in the [activation workflow](../../destinations/ui/activation-overview.md), select **[!UICONTROL View applied policies]**.

A policy check dialog appears, showing you a preview of how your consent policies affect the addressable audience of the activated segment.
 -->

## 已激活段的策略實施 {#policy-enforcement-for-activated-segments}

策略實施仍適用於激活段後的段，從而限制對段或其目標的任何更改，從而導致策略違規。 因為 [資料沿襲](#lineage) 在策略實施中，下列任何操作都可能觸發違規：

* 正在更新資料使用標籤
* 更改段的資料集
* 更改段謂語
* 更改目標配置

如果上述任何操作觸發違規，則會阻止保存該操作並顯示策略違規消息，從而確保激活的段在被修改時繼續遵守資料使用策略。

## 後續步驟

本文檔介紹了自動策略實施在Experience Platform中的工作方式。 有關如何以寫程式方式將策略實施與使用API調用的應用程式整合的步驟，請參見上的指南 [基於API的強制](./api-enforcement.md)。
