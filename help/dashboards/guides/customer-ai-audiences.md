---
title: Audiences控制面板Customer AI Widget
description: 瞭解Customer AI如何提供關於您組織即時客戶個人檔案對象流失或傾向的重要深入分析。
hide: true
hidefromtoc: true
source-git-commit: e14067606e4c4868c926433129d835c7b0a7a18f
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 2%

---

# Audiences儀表板客戶AI Widget {#customer-ai-audiences-widgets}

Customer AI 可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。 Customer AI的運作方式是分析現有的消費者體驗事件資料，以預測流失或轉換傾向分數。 這些高精確度的客戶傾向模型可讓您進行更精確的分段和目標定位。 此 [分數的分佈](#customer-ai-distribution-of-scores) 和 [評分摘要](#customer-ai-scoring-summary) 深入分析會示範您對象中的劃分。 它們會強調哪些設定檔為高/低/中傾向，以及它們在您的設定檔計數中的分配方式。

<!-- 
THe links when required
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL 分數的Customer AI分佈] {#customer-ai-distribution-of-scores}

此 [!UICONTROL 分數的Customer AI分佈] Widget會依傾向分數分類設定檔總數。 設定檔計數的分佈取決於AI模型和所選的合併原則，然後以5%的增量進行視覺化，表示其傾向。 設定檔傾向性是以分別以綠色、黃色和紅色標示為高、中和低的色彩。 設定檔的計數會沿Y軸提供，而傾向分數則會沿X軸提供。

決定傾向分數的AI模型可從Widget標題下方的下拉式選擇器中選取。 下拉式清單包含所有已設定的Customer AI模型清單。 從可用模型清單中為您的分析選取適當的AI模型。 如果沒有可用的Customer AI模型，Widget中的訊息會指示您設定至少一個Customer AI模型，並提供指向Customer AI模型設定頁面的超連結。 如需相關指示，請參閱檔案 [如何設定Customer AI執行個體](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>選取概述標籤正下方的下拉式清單，以變更決定分析中包含哪些設定檔的合併原則。 請參閱以下小節： [合併原則](#merge-policies) 以取得簡要說明，或 [合併原則概觀](../../profile/merge-policies/overview.md) 以取得更多詳細資料。

若要導覽至所選Customer AI模型的詳細深入分析頁面，請選取 **[!UICONTROL 檢視模型詳細資料]**.

![Experience Platform受眾控制面板，具有 [!UICONTROL 分數的Customer AI分佈] Widget和 [!UICONTROL 檢視模型詳細資料] 反白顯示。](../images/segments/customer-ai-distribution-of-scores.png)

詳細模型深入分析頁面隨即顯示。

![Customer AI的深入分析頁面。](../images/profiles/customer-ai-insights-page.png)

有關Customer AI的更多資訊可在以下網址找到： [探索見解UI指南](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL Customer AI評分摘要] {#customer-ai-scoring-summary}

此Widget顯示已評分的個人檔案總數，並將其分類為分別包含高、中及低傾向的綠色、黃色及紅色貯體。 環形圖用於說明高、中和低傾向性之間總設定檔的成比例，分別表示為綠色、黃色和紅色。 設定檔符合75歲以上的高傾向、25到74歲之間的中傾向，以及24歲以下的低傾向。 圖例會指出色彩代碼和傾向性臨界值。 當游標暫留在環圈圖的個別區段上時，高、中和低傾向性的設定檔計數會顯示在對話方塊中。

>[!NOTE]
>
>如果視覺效果是轉換傾向分數，則高分會以綠色顯示，低分會以紅色顯示。 如果您預測的是流失傾向，則系統會加以逆轉，高分會以紅色顯示，低分則會以綠色顯示。 無論您選擇哪種傾向型別，中段貯體都會保持黃色。

Widget標題下方的下拉式選單提供所有已設定的Customer AI模型清單。 從可用模型清單中為您的分析選取適當的AI模型。 如果沒有可用的Customer AI模型，Widget中的訊息會指示您設定至少一個Customer AI模型，並提供指向Customer AI模型設定頁面的超連結。 請參閱以下檔案： [如何設定Customer AI執行個體](../../intelligent-services/customer-ai/user-guide/configure.md) 以取得詳細指示。

>[!NOTE]
>
>計算的設定檔總數取決於所選的合併原則。 若要變更所使用的合併原則，請選取概述標籤正下方的下拉式清單。 請參閱以下小節： [合併原則](#merge-policies) 以取得簡要說明，或 [合併原則概觀](../../profile/merge-policies/overview.md) 以取得更多詳細資料。

![Customer AI評分摘要Widget醒目提示的Experience Platform Audiences儀表板。](../images/segments/customer-ai-scoring-summary.png)

選取 **[!UICONTROL 檢視模型詳細資料]** 導覽至所選Customer AI模型的詳細深入分析頁面。 有關Customer AI的更多資訊可在以下網址找到： [探索見解UI指南](../../intelligent-services/customer-ai/user-guide/discover-insights.md).
