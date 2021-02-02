---
keywords: Experience Platform; home；熱門主題；資料治理；資料使用策略使用手冊
solution: Experience Platform
title: 資料使用原則使用指南
topic: policies
description: Adobe Experience Platform Data Governance提供使用者介面，可讓您建立和管理資料使用政策。 本檔案概述您可在Experience Platform使用者介面的「原則」工作區中執行的動作。
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# 資料使用原則使用指南

Adobe Experience Platform [!DNL Data Governance]提供使用者介面，可讓您建立並管理資料使用政策。 本文檔概述了在[!DNL Experience Platform]用戶介面的&#x200B;**策略**&#x200B;工作區中可以執行的操作。

>[!IMPORTANT]
>
>預設會停用所有資料使用政策（包括Adobe提供的核心政策）。 要考慮實施單個策略，您必須手動啟用該策略。 有關如何在UI中執行此操作的步驟，請參閱[啟用策略](#enable)一節。

## 必要條件

本指南需要對以下[!DNL Experience Platform]概念有充分的瞭解：

- [[!DNL Data Governance]](../home.md)
- [資料使用原則](./overview.md)

## 查看資料使用策略{#view-policies}

在[!DNL Experience Platform] UI中，選擇&#x200B;**[!UICONTROL 策略]**&#x200B;以開啟&#x200B;**[!UICONTROL 策略]**&#x200B;工作區。 在&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤中，您可以看到可用原則的清單，包括其相關標籤、行銷動作和狀態。

![](../images/policies/browse-policies.png)

選擇列出的策略以查看其說明和類型。 如果選擇了自定義策略，則顯示其他控制項以編輯、刪除或[啟用／禁用策略](#enable)。

![](../images/policies/policy-details.png)

## 建立自訂資料使用原則{#create-policy}

要建立新的自定義資料使用策略，請在&#x200B;**[!UICONTROL 策略]**&#x200B;工作區的&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁籤的右上角選擇&#x200B;**[!UICONTROL 建立策略]**。

![](../images/policies/create-policy-button.png)

出現&#x200B;**[!UICONTROL 建立策略]**&#x200B;工作流。 首先，提供新策略的名稱和說明。

![](../images/policies/create-policy-description.png)

接著，選擇策略將基於的資料使用標籤。 在選擇多個標籤時，系統會提供您選項來選擇資料應包含所有標籤，還是只包含其中一個標籤，以便套用原則。 完成後，選擇&#x200B;**[!UICONTROL Next]**。

![](../images/policies/add-labels.png)

此時會顯示「選擇行銷動作&#x200B;]**」步驟。**[!UICONTROL &#x200B;從提供的清單中選擇適當的行銷動作，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

>[!NOTE]
>
>選取多個行銷動作時，原則會將其解譯為「OR」規則。 換言之，如果所選行銷動作的&#x200B;**any**&#x200B;已執行，則套用原則。

![](../images/policies/add-marketing-actions.png)

出現&#x200B;**[!UICONTROL Review]**&#x200B;步驟，允許您在建立新策略之前查看其詳細資訊。 滿足後，選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以建立策略。

![](../images/policies/policy-review.png)

**[!UICONTROL Browse]**&#x200B;標籤會重新出現，現在會列出新建立的「草稿」狀態原則。 若要啟用原則，請參閱下一節。

![](../images/policies/created-policy.png)

## 啟用或禁用資料使用策略{#enable}

預設會停用所有資料使用政策（包括Adobe提供的核心政策）。 若要考慮實施個別原則，您必須透過API或UI手動啟用該原則。

您可以在&#x200B;**[!UICONTROL 策略]**&#x200B;工作區的&#x200B;**[!UICONTROL 瀏覽]**&#x200B;頁籤中啟用或禁用策略。 從清單中選取自訂原則，以在右側顯示其詳細資訊。 在&#x200B;**[!UICONTROL Status]**&#x200B;下，選擇切換按鈕以啟用或禁用策略。

![](../images/policies/enable-policy.png)

## 檢視行銷動作{#view-marketing-actions}

在&#x200B;**[!UICONTROL 原則]**&#x200B;工作區中，選取&#x200B;**[!UICONTROL 行銷動作]**&#x200B;標籤，以檢視由Adobe和您自己的組織定義的可用行銷動作清單。

![](../images/policies/marketing-actions.png)

## 建立行銷動作{#create-marketing-action}

若要建立新的自訂行銷動作，請在&#x200B;**[!UICONTROL 原則]**&#x200B;工作區的&#x200B;**[!UICONTROL 行銷動作]**&#x200B;標籤右上角選取&#x200B;**[!UICONTROL 建立行銷動作]**。

![](../images/policies/create-marketing-action.png)

此時會顯示「建立行銷動作&#x200B;]**」對話方塊。**[!UICONTROL &#x200B;輸入行銷動作的名稱和說明，然後選擇&#x200B;**[!UICONTROL Create]**。

![](../images/policies/create-marketing-action-details.png)

新建立的動作會顯示在&#x200B;**[!UICONTROL 行銷動作]**&#x200B;標籤中。 現在，當[建立新的資料使用政策](#create-policy)時，您可以使用行銷動作。

![](../images/policies/created-marketing-action.png)

## 編輯或刪除行銷動作{#edit-delete-marketing-action}

>[!NOTE]
>
>只能編輯您組織定義的自訂行銷動作。 Adobe定義的行銷動作無法變更或刪除。

在&#x200B;**[!UICONTROL 原則]**&#x200B;工作區中，選取&#x200B;**[!UICONTROL 行銷動作]**&#x200B;標籤，以檢視由Adobe和您自己的組織定義的可用行銷動作清單。 從清單中選取自訂行銷動作，然後使用右側區段中提供的欄位來編輯行銷動作的詳細資料。

![](../images/policies/edit-marketing-action.png)

如果任何現有的使用策略未使用行銷動作，則可以選擇&#x200B;**[!UICONTROL 刪除行銷動作]**&#x200B;將其刪除。

>[!NOTE]
>
>嘗試刪除現有原則使用的行銷動作時，會顯示錯誤訊息，指出刪除嘗試失敗。

![](../images/policies/delete-marketing-action.png)

## 後續步驟

本檔案概述如何在[!DNL Experience Platform] UI中管理資料使用原則。 有關如何使用[!DNL Policy Service API]管理策略的步驟，請參閱[開發人員指南](../api/getting-started.md)。 有關如何強制執行資料使用策略的資訊，請參閱[策略實施概述](../enforcement/overview.md)。

以下視頻演示了如何在[!DNL Experience Platform] UI中使用使用策略：

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)