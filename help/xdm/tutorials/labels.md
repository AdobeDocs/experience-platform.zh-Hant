---
title: 管理架構的資料使用標籤
description: 瞭解如何將資料使用標籤添加到Adobe Experience PlatformUI中的「體驗資料模型」(XDM)架構欄位。
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 3d49b5c503ec0fd92f0639abf366d7652566fac7
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 管理架構的資料使用標籤

>[!IMPORTANT]
>
>基於模式的標籤是 [基於屬性的訪問控制](../../access-control/abac/overview.md)目前，該產品在面向美國醫療保健客戶的有限版本中提供。 這一功能一旦完全發佈，將可供所有Real-time Customer Data Platform客戶使用。

引入Adobe Experience Platform的所有資料都受經驗資料模型(XDM)架構的約束。 此資料可能受您的組織或法律法規定義的使用限制的限制。 為此，平台允許您通過使用 [資料使用標籤](../../data-governance/labels/overview.md)。

應用於架構欄位的標籤表示應用於該特定欄位中包含的資料的使用策略。

雖然標籤可以應用於單個資料集（以及這些資料集中的欄位），但您也可以在架構級別應用標籤。 將標籤直接應用到架構時，這些標籤將傳播到基於該架構的所有現有和將來資料集。

此外，在一個方案中添加的任何欄位標籤都會傳播到使用共用類或欄位組中相同欄位的所有其他方案。 這有助於確保整個資料模型中類似欄位的使用規則保持一致。

本教程介紹了使用平台UI中的架構編輯器向架構添加標籤的步驟。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [[!DNL Experience Data Model (XDM) System]](../home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構編輯器](../ui/overview.md):瞭解如何在平台UI中建立和管理架構和其他資源。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md):提供對平台操作強制實施資料使用限制的基礎架構，使用策略定義可以（或不能）對標籤資料執行哪些市場營銷操作。

## 選擇要將標籤添加到的架構或欄位 {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="編輯治理標籤"
>abstract="將標籤應用到架構欄位，以指示應用於該特定欄位中包含的資料的使用策略。"

要開始添加標籤，必須先 [選擇要編輯的現有架構](../ui/resources/schemas.md#edit) 或 [建立新架構](../ui/resources/schemas.md#create) 在架構編輯器中查看其結構。

要編輯單個欄位的標籤，可以在畫布中選擇該欄位，然後選擇 **[!UICONTROL 管理訪問]** 右欄。

![從「架構編輯器」畫布中選擇一個欄位](../images/tutorials/labels/manage-access.png)

也可以選擇 **[!UICONTROL 標籤]** 頁籤 **[!UICONTROL 編輯治理標籤]** 右欄。

![從 [!UICONTROL 標籤] 頁籤](../images/tutorials/labels/select-field-on-labels-tab.png)

要編輯整個架構的標籤，請選擇鉛筆表徵圖(![](../images/tutorials/labels/pencil-icon.png)) **[!UICONTROL 標籤]** 頁籤。

![從 [!UICONTROL 標籤] 頁籤](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>當您首次嘗試編輯架構或欄位的標籤時，將顯示免責聲明消息，說明標籤使用如何根據組織的策略影響下游操作。 選擇 **[!UICONTROL 繼續]** 來編輯。
>
>![標籤使用免責聲明](../images/tutorials/labels/disclaimer.png)

## 編輯架構或欄位的標籤

此時將顯示一個對話框，允許您編輯選定欄位的標籤。 如果選擇了單個對象類型欄位，右欄將列出應用標籤將傳播到的子欄位。

![顯示的選定欄位](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>如果正在為整個方案編輯欄位，右欄將不列出適用的欄位，而是顯示方案名稱。

使用顯示的清單選擇要添加到方案或欄位的標籤。 選擇標籤後， **[!UICONTROL 已應用標籤]** 部分更新，顯示到目前為止已選擇的標籤。

![顯示的已應用標籤](../images/tutorials/labels/applied-labels.png)

要按類型篩選顯示的標籤，請在左滑軌中選擇所需的類別。 要建立新的自定義標籤，請選擇 **[!UICONTROL 建立標籤]**。

![篩選顯示的標籤或建立新標籤](../images/tutorials/labels/filter-and-create-custom.png)

一旦對所選標籤滿意，請選擇 **[!UICONTROL 保存]** 將其應用於欄位或架構。

![保存選定的標籤](../images/tutorials/labels/save-labels.png)

的 **[!UICONTROL 標籤]** 頁籤，其中顯示架構的已應用標籤。

![已應用欄位標籤](../images/tutorials/labels/field-labels-added.png)

## 後續步驟

本指南介紹了如何管理架構和欄位的資料使用標籤。 有關管理資料使用標籤的資訊，包括如何將其添加到特定資料集而不是架構級別，請參見 [資料使用標籤UI指南](../../data-governance/labels/user-guide.md)。
