---
title: 棄用UI中的XDM欄位
description: 瞭解如何在Experience Platform中使用結構描述編輯器來棄用Experience Data Model (XDM)欄位。
exl-id: f4c5f58a-5190-47d7-8bfc-b33ed238bf25
source-git-commit: 4fa98df9dcc296ba7cb141cb22df116524a0eb0c
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# 棄用UI中的XDM欄位

Experience Data Model (XDM)可在您業務需求有所變更時，彈性為您管理資料模型，方法是在擷取資料後停用結構描述欄位。 棄用不想要的欄位時，可從UI檢視中移除這些欄位，也可對下游UI隱藏這些欄位。 方便的是，結構編輯器中的核取方塊可讓您顯示已棄用的欄位，並可視需要取消棄用。

由於預設會從UI隱藏已棄用的欄位，因此可簡化結構編輯器中的結構描述，並防止將不需要的欄位新增到下游相依性，例如區段產生器、歷程設計器等。 欄位棄用也可以回溯相容。 其他使用已棄用欄位的系統（例如對象和查詢）將會繼續依預期進行評估。 如果現有對象中使用已棄用的欄位，則會正常處理該欄位，這表示該欄位會如預期在「區段產生器」畫布中顯示，或根據已棄用欄位中可用的任何資料進行評估。 這是無中斷的變更，不會對任何現有資料流程造成負面影響。

>[!NOTE]
>
>將資料內嵌到結構描述中之前，您可以移除不必要的欄位群組。 如需詳細資訊，請參閱有關[如何從結構描述](../ui/resources/schemas.md#remove-fields)移除欄位群組的檔案。

一旦將資料內嵌到結構描述中，您就無法在不進行重大變更的情況下從結構描述中移除欄位。 在此情況下，您可以使用[結構描述編輯器](./create-schema-ui.md)或[結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)，取代結構描述或自訂資源中不需要的欄位。

本文會說明如何使用Experience Platform使用者介面中的結構描述編輯器，為不同的XDM資源棄用欄位。 如需使用API來取代XDM欄位的步驟，請參閱有關[使用結構描述登入API取代XDM欄位的教學課程](./field-deprecation-api.md)。

## 棄用欄位 {#deprecate}

若要棄用自訂欄位，請導覽至您要編輯的結構描述的「結構描述編輯器」。 從畫布的[!UICONTROL Structure]區段中選取您要棄用的欄位，然後從[!UICONTROL 欄位屬性]中選取&#x200B;**[!UICONTROL Deprecate]**。

![已選取欄位且已反白的結構描述編輯器。](../images/tutorials/field-deprecation/deprecate-single-field.png)

系統會顯示一個對話方塊，以確認您的選擇，並通知您該欄位將會從聯合結構描述的UI檢視中移除，並隱藏在下游UI中。 若要完成動作，請選取&#x200B;**[!UICONTROL 確認]**。

![反白顯示Confirm的Deprecate欄位對話方塊。](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

該欄位現在從UI檢視中移除。

>[!NOTE]
>
>一旦棄用，下游UI (例如區段控制面板、Customer Journey Analytics和Adobe Journey Optimizer)就不會再將棄用的欄位顯示為工作流程的一部分。 不過，下游UI可選擇視需要顯示已棄用的欄位，並繼續將已棄用的欄位視為正常欄位。 如需詳細資訊，請參閱其各自的檔案。 使用已棄用欄位的查詢和受眾將繼續如預期般執行。

## 顯示已被取代的欄位 {#show-deprecated}

若要檢視先前已棄用的欄位，請導覽至結構編輯器中的相關結構。 在畫布的[!UICONTROL 構成]區段中，選取&#x200B;**[!UICONTROL 顯示已棄用的欄位]**&#x200B;核取方塊。

已棄用的欄位現在會出現在UI檢視中。 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以確認您的設定。

![結構描述編輯器已選取欄位，顯示已棄用的欄位，並醒目提示儲存。](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## 取消棄用欄位 {#undeprecate-fields}

若要復原已棄用的欄位，請先依照上述說明顯示已棄用的欄位](#show-deprecated)，然後從編輯器的[!UICONTROL 結構]區段中選取已棄用的欄位。 [接著，從[!UICONTROL 欄位屬性]側邊欄選取&#x200B;**[!UICONTROL 取消棄用]**，接著選取&#x200B;**[!UICONTROL 儲存]**。

![結構描述編輯器，包含已棄用的欄位、取消棄用和醒目提示的儲存。](../images/tutorials/field-deprecation/undeprecate-single-field.png)

[!UICONTROL 取消棄用欄位]對話方塊就會顯示。 若要確認您的變更，請選取&#x200B;**[!UICONTROL 確認]**。

![反白顯示[!UICONTROL 取消棄用欄位]的確認對話方塊。](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

欄位現在在UI檢視以及下游UI中顯示為標準欄位。 同樣地，您現在可以選擇棄用欄位。

## 後續步驟

本檔案說明如何使用結構描述編輯器UI來棄用XDM欄位。 如需設定自訂資源欄位的詳細資訊，請參閱[在API中定義XDM欄位的指南](./custom-fields-api.md)。 如需有關管理描述元的詳細資訊，請參閱[描述元端點指南](../api/descriptors.md)。
