---
title: 取代UI中的XDM欄位
description: 了解如何使用Experience Platform中的結構編輯器來取代Experience Data Model(XDM)欄位。
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 取代UI中的XDM欄位

Experience Data Model(XDM)可在資料內嵌後淘汰結構欄位，讓您可因應業務需求變更，靈活管理資料模型。 不想要的欄位可以遭到取代，以從UI檢視中移除，也可從下游UI中隱藏。 方便地，結構編輯器中的核取方塊可讓您顯示已棄用的欄位，如有需要，您也可以將其取代。

由於預設會從UI中隱藏已棄用的欄位，因此這會簡化結構編輯器中的結構，並防止不想要的欄位新增至下游相依性，例如區段產生器、歷程設計器等。 欄位取代也可向後相容。 使用已棄用欄位的其他系統（例如區段和查詢）會繼續如預期般評估這些欄位。 如果現有區段中使用已棄用欄位，則會正常處理，這表示該欄位會如預期顯示在區段產生器畫布中，或根據已棄用欄位中任何可用資料評估。 這是不會對任何現有資料流造成負面影響的不間斷變更。

>[!NOTE]
>
>在將資料內嵌至結構之前，您可以移除不必要的欄位群組。 請參閱 [如何從架構中移除欄位群組](../ui/resources/schemas.md#remove-fields) 以取得更多資訊。

將資料擷取至您的架構後，您就無法再移除架構中的欄位，而不進行中斷的變更。 在此情況下，您可以使用 [結構編輯器](./create-schema-ui.md) 或 [結構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

本檔案說明如何使用Experience Platform使用者介面中的結構編輯器，取代不同XDM資源的欄位。 如需使用API取代XDM欄位的步驟，請參閱以下的教學課程： [使用Schema Registry API取代XDM欄位](./field-deprecation-api.md).

## 取代欄位 {#deprecate}

若要取代自訂欄位，請導覽至您要編輯之結構的結構編輯器。 從「 [!UICONTROL 結構] 畫布的區段，後面 **[!UICONTROL 淘汰]** 從 [!UICONTROL 欄位屬性].

![已選取欄位的結構編輯器，並反白顯示「已淘汰」。](../images/tutorials/field-deprecation/deprecate-single-field.png)

畫面會顯示對話方塊，確認您的選擇，並通知您該欄位將從聯合架構的UI檢視中移除，並從下游UI中隱藏。 若要完成動作，請選取 **[!UICONTROL 確認]**.

![反白顯示「確認」欄位對話框。](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

欄位現在會從UI檢視中移除。

>[!NOTE]
>
>下游UI(例如「劃分」控制面板、Customer Journey Analytics和Adobe Journey Optimizer)一旦淘汰後，即不再將已棄用的欄位顯示為其工作流程的一部分。 不過，下游UI有選項可視需要顯示已棄用的欄位，並繼續將已棄用的欄位視為正常欄位。 如需詳細資訊，請參閱其各自的檔案。 使用已棄用欄位的查詢和區段會繼續如預期般執行。

## 顯示已棄用的欄位 {#show-deprecated}

若要檢視先前已棄用的欄位，請導覽至「結構編輯器」中的相關結構。 選取 **[!UICONTROL 顯示已棄用的欄位]** 核取方塊 [!UICONTROL 組合物] 區段。

已棄用的欄位現在會顯示在UI檢視中。 選擇 **[!UICONTROL 儲存]** 確認設定。

![已選取欄位的結構編輯器、顯示已棄用的欄位並反白顯示儲存。](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## 不足的欄位 {#undeprecate-fields}

若要還原已棄用的欄位，請先 [顯示已棄用的欄位](#show-deprecated) 如上所述，然後從編輯器的 [!UICONTROL 結構] 區段。 下一步，選擇 **[!UICONTROL Undeprecate]** 從 [!UICONTROL 欄位屬性] 側欄後跟 **[!UICONTROL 儲存]**.

![架構編輯器中，已過時欄位、未取代和已反白顯示儲存。](../images/tutorials/field-deprecation/undeprecate-single-field.png)

此 [!UICONTROL 不足欄位] 對話框。 若要確認變更，請選取 **[!UICONTROL 確認]**.

![此 [!UICONTROL 不足欄位] 對話框，突出顯示確認。](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

欄位現在會在UI檢視和下游UI中顯示為標準。 同樣地，您現在可以選擇淘汰欄位。

## 後續步驟

本檔案說明如何使用結構編輯器UI來取代XDM欄位。 如需為自訂資源設定欄位的詳細資訊，請參閱 [在API中定義XDM欄位](./custom-fields-api.md). 有關管理描述符的詳細資訊，請參見 [descriptors endpoint worke](../api/descriptors.md).
