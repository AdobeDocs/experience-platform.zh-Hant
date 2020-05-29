---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料使用原則使用指南
topic: policies
translation-type: tm+mt
source-git-commit: af7fa6048fa60392a98975fe6fc36e8302355a05
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 2%

---


# 資料使用原則使用指南

Adobe Experience Platform Data Governance提供使用者介面，可讓您建立和管理資料使用政策。 本檔案概述您可在Experience Platform UI的「原則」工作區 _中_ ，執行的動作。

## 必要條件

本指南需要有效瞭解下列Experience Platform概念：

- [資料控管](../home.md)
- [資料使用原則](./overview.md)

## 檢視資料使用原則

在Experience Platform UI中，按一下「 **[!UICONTROL 原則]** 」以開啟 *[!UICONTROL 「原則]* 」工作區。 在「瀏 **[!UICONTROL 覽]** 」索引標籤中，您可以看到可用原則的清單，包括其相關標籤、行銷動作和狀態。

![](../images/policies/browse-policies.png)

按一下列出的策略以查看其說明和類型。 如果選取自訂原則，則會顯示其他控制項以編輯、刪除或啟 [用／停用原則](#enable)。

![](../images/policies/policy-details.png)

## 建立自訂資料使用原則

若要建立新的自訂資料使用原則，請按一 **[!UICONTROL 下]** 「原則」工作區右上角的「建立 *原則* 」。

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

您可以在「原則」工作區的「瀏覽」標籤上啟用或停 *[!UICONTROL 用自訂資料]**[!UICONTROL 使用原則]* 。 從清單中選取自訂原則，以在右側顯示其詳細資訊。 在「 *[!UICONTROL 狀態]*」下，選擇切換按鈕以啟用或停用原則。

![](../images/policies/enable-policy.png)

## 後續步驟

本檔案概述如何在Experience Platform UI中管理資料使用原則。 如需如何使用DULE Policy API管理原則的步驟，請參閱開發 [人員指南](../api/getting-started.md)。 如需如何實施資料使用原則的詳細資訊，請參閱 [原則實施概觀](../enforcement/overview.md)。

以下視訊示範如何在Experience Platform UI中使用使用原則：

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)