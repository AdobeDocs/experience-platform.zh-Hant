---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料使用原則使用指南
topic: policies
translation-type: tm+mt
source-git-commit: c4554e3fbc0dd527606b81e2767cb5777b6e81e7
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---


# 資料使用原則使用指南

Adobe Experience Platform Data Governance提供使用者介面，可讓您建立和管理資料使用政策。 本檔案概述您可在Experience Platform使用者介面的「原則 __ 」工作區中執行的動作。

>[!IMPORTANT] 預設會停用所有資料使用政策（包括Adobe提供的核心政策）。 要考慮實施單個策略，您必須手動啟用該策略。 如需如何在UI中 [執行此動作](#enable) ，請參閱啟用原則一節。

## 必要條件

本指南需要有效瞭解下列Experience Platform概念：

- [資料控管](../home.md)
- [資料使用原則](./overview.md)

## 檢視資料使用原則 {#view-policies}

在Experience Platform UI中，按一下「 **[!UICONTROL 原則]** 」以開啟 *[!UICONTROL 「原則]* 」工作區。 在「瀏 **[!UICONTROL 覽]** 」索引標籤中，您可以看到可用原則的清單，包括其相關標籤、行銷動作和狀態。

![](../images/policies/browse-policies.png)

按一下列出的策略以查看其說明和類型。 如果選取自訂原則，則會顯示其他控制項以編輯、刪除或啟 [用／停用原則](#enable)。

![](../images/policies/policy-details.png)

## 建立自訂資料使用原則 {#create-policy}

若要建立新的自訂資料使用原則，請按一 **[!UICONTROL 下「原則]** 」工作區中「瀏覽 **[!UICONTROL 」標籤右上角的「建立]** 原則 ** 」。

![](../images/policies/create-policy-button.png)

此時將 *[!UICONTROL 顯示「建立策略]* 」工作流。 首先，提供新策略的名稱和說明。

![](../images/policies/create-policy-description.png)

接著，選擇策略將基於的資料使用標籤。 在選擇多個標籤時，系統會提供您選項來選擇資料應包含所有標籤，還是只包含其中一個標籤，以便套用原則。 完成後，按&#x200B;**[!UICONTROL 「下一步」]**。

![](../images/policies/add-labels.png)

此時會 *[!UICONTROL 顯示「選擇行銷]* 」動作步驟。 從提供的清單中選擇適當的行銷動作，然後按一下「 **[!UICONTROL 下一步]** 」繼續。

>[!NOTE] 選取多個行銷動作時，原則會將其解譯為「OR」規則。 換言之，如果執行任何選 _定的行銷_ ，則套用原則。

![](../images/policies/add-marketing-actions.png)

此時 *[!UICONTROL 會出現]* 「查看」步驟，允許您在建立新策略之前查看其詳細資訊。 在您滿意後，按一下「 **[!UICONTROL 完成]** 」以建立原則。

![](../images/policies/policy-review.png)

「瀏 *[!UICONTROL 覽]* 」標籤會重新出現，現在會列出新建立的「草稿」狀態原則。 若要啟用原則，請參閱下一節。

![](../images/policies/created-policy.png)

## 啟用或停用資料使用原則 {#enable}

預設會停用所有資料使用政策（包括Adobe提供的核心政策）。 若要考慮實施個別原則，您必須透過API或UI手動啟用該原則。

您可以從「策略」工作區的「瀏 *[!UICONTROL 覽]* 」頁籤中啟用或 *[!UICONTROL 禁用策略]* 。 從清單中選取自訂原則，以在右側顯示其詳細資訊。 在「 *[!UICONTROL 狀態]*」下，選擇切換按鈕以啟用或停用原則。

![](../images/policies/enable-policy.png)

## 檢視行銷動作 {#view-marketing-actions}

在「原 **[!UICONTROL 則]** 」工作區中，選取「 **[!UICONTROL 行銷動作]** 」標籤，以檢視Adobe及您自己組織定義的可用行銷動作清單。

![](../images/policies/marketing-actions.png)

## 建立行銷動作 {#create-marketing-action}

若要建立新的自訂行銷動作，請按一 **[!UICONTROL 下「原則」工作區中「行銷動作]** 」標籤右上角的「建立行銷 **[!UICONTROL 動作]**** 」。

![](../images/policies/create-marketing-action.png)

此時會 *[!UICONTROL 出現「建立行銷]* 」對話方塊。 輸入行銷動作的名稱和說明，然後按一下「建 **[!UICONTROL 立]**」。

![](../images/policies/create-marketing-action-details.png)

新建立的動作會顯示在「行銷 *[!UICONTROL 動作」標籤]* 中。 您現在可以在建立新的資料使用 [政策時使用行銷動作](#create-policy)。

![](../images/policies/created-marketing-action.png)

## 編輯或刪除行銷動作 {#edit-delete-marketing-action}

>[!NOTE] 只能編輯您組織定義的自訂行銷動作。 Adobe定義的行銷動作無法變更或刪除。

在「原 **[!UICONTROL 則]** 」工作區中，選取「 **[!UICONTROL 行銷動作]** 」標籤，以檢視Adobe及您自己組織定義的可用行銷動作清單。 從清單中選取自訂行銷動作，然後使用右側區段中提供的欄位來編輯行銷動作的詳細資料。

![](../images/policies/edit-marketing-action.png)

如果任何現有的使用政策未使用行銷動作，您可以按一下刪除行銷動 **[!UICONTROL 作來刪除動作]**。

>[!NOTE] 嘗試刪除現有原則使用的行銷動作時，會顯示錯誤訊息，指出刪除嘗試失敗。

![](../images/policies/delete-marketing-action.png)

## 後續步驟

本檔案概述如何在Experience Platform UI中管理資料使用原則。 如需如何使用DULE Policy API管理原則的步驟，請參閱開發 [人員指南](../api/getting-started.md)。 如需如何實施資料使用原則的詳細資訊，請參閱 [原則實施概觀](../enforcement/overview.md)。

以下視訊示範如何在Experience Platform UI中使用使用原則：

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)