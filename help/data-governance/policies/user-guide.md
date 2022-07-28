---
keywords: Experience Platform；首頁；熱門主題；資料管理；資料使用策略使用手冊
solution: Experience Platform
title: 在UI中管理資料使用策略
topic-legacy: policies
description: Adobe Experience Platform資料治理提供了一個用戶介面，允許您建立和管理資料使用策略。 本文檔概述了可在Experience Platform用戶介面的「策略」工作區中執行的操作。
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 0%

---

# 在UI中管理資料使用策略

Adobe Experience Platform資料治理提供了一個用戶介面，允許您建立和管理資料使用策略。 本文檔概述了在 **策略** 工作區 [!DNL Experience Platform] 用戶介面。

>[!IMPORTANT]
>
>預設情況下，所有資料使用策略(包括由Adobe提供的核心策略)都被禁用。 要考慮實施單個策略，必須手動啟用該策略。 請參閱 [啟用策略](#enable) 以獲取有關如何在UI中執行此操作的步驟。

## 先決條件

本指南要求對以下方面有一定的認識 [!DNL Experience Platform] 概念：

* [資料治理](../home.md)
* [資料使用原則](./overview.md)

## 查看現有策略 {#view-policies}

在 [!DNL Experience Platform] UI，選擇 **[!UICONTROL 策略]** 開啟 **[!UICONTROL 策略]** 工作區。 在 **[!UICONTROL 瀏覽]** 頁籤，您可以看到可用策略的清單，包括它們的關聯標籤、市場營銷操作和狀態。

![](../images/policies/browse-policies.png)

如果您有權訪問同意策略，請選擇 **[!UICONTROL 同意策略]** 切換以在 [!UICONTROL 瀏覽] 頁籤。

![](../images/policies/consent-policy-toggle.png)

選擇列出的策略以查看其說明和類型。 如果選擇了自定義策略，則顯示其他控制項以編輯、刪除或 [啟用/禁用策略](#enable)。

![](../images/policies/policy-details.png)

## 建立自定義策略 {#create-policy}

要建立新的自定義資料使用策略，請選擇 **[!UICONTROL 建立策略]** 右上角 **[!UICONTROL 瀏覽]** 的 **[!UICONTROL 策略]** 工作區。

![](../images/policies/create-policy-button.png)

根據您是否是同意策略測試的一部分，將發生以下情況之一：

* 如果您不是測試版的一部分，則會立即將您帶到工作流中， [建立資料治理策略](#create-governance-policy)。
* 如果您是Beta的一部分，則對話框將提供額外選項 [建立同意策略](#consent-policy)。
   ![](../images/policies/choose-policy-type.png)

### 建立資料治理策略 {#create-governance-policy}

的 **[!UICONTROL 建立策略]** 工作流。 首先提供新策略的名稱和說明。

![](../images/policies/create-policy-description.png)

接下來，選擇策略將基於的資料使用標籤。 在選擇多個標籤時，系統會為您提供選項來選擇資料應包含所有標籤還是僅包含其中一個標籤，以便策略應用。 選擇 **[!UICONTROL 下一個]** 的子菜單。

![](../images/policies/add-labels.png)

的 **[!UICONTROL 選擇市場營銷活動]** 的上界。 從提供的清單中選擇相應的市場營銷活動，然後選擇 **[!UICONTROL 下一個]** 繼續。

>[!NOTE]
>
>選擇多個市場營銷活動時，策略會將其解釋為「或」規則。 換句話說，如果 **任何** 執行所選市場活動。

![](../images/policies/add-marketing-actions.png)

的 **[!UICONTROL 審閱]** 的子菜單。 滿足後，選擇 **[!UICONTROL 完成]** 的子菜單。

![](../images/policies/policy-review.png)

的 **[!UICONTROL 瀏覽]** 頁籤，此時將列出新建立的「草稿」狀態策略。 要啟用策略，請參閱下一節。

![](../images/policies/created-policy.png)

### 建立同意策略 {#consent-policy}

>[!IMPORTANT]
>
>目前，只有購買了Healthcare Shield的組織才可使用同意策略。

如果您選擇建立同意策略，將顯示一個新螢幕，允許您配置新策略。

![](../images/policies/consent-policy-dialog.png)

為了使用同意策略，必須在配置檔案資料中包含同意屬性。 請參閱上的指南 [Experience Platform中的同意處理](../../landing/governance-privacy-security/consent/adobe/overview.md) 有關如何在聯合架構中包含所需屬性的詳細步驟。

同意策略由兩個邏輯元件組成：

* **[!UICONTROL 如果]**:將觸發策略檢查的條件。 這可以基於正在執行的特定市場營銷操作、特定資料使用標籤的存在或兩者的組合。
* **[!UICONTROL 然後]**:要將配置檔案包含在觸發策略的操作中，必須存在的同意屬性。

#### 配置條件

在 **[!UICONTROL 如果]** 部分，選擇應觸發此策略的市場營銷操作和/或資料使用標籤。 選擇 **[!UICONTROL 查看全部]** 和 **[!UICONTROL 選擇標籤]** 查看可用市場營銷操作和標籤的完整清單。

添加至少一個條件後，可以選擇 **[!UICONTROL 添加條件]** 要繼續根據需要添加更多條件，請從下拉清單中選擇相應的條件類型。

![](../images/policies/add-condition.png)

如果選擇多個條件，則可以使用它們之間出現的表徵圖來切換「AND」和「OR」之間的條件關係。

![](../images/policies/and-or-selection.png)

#### 選擇同意屬性

在 **[!UICONTROL 然後]** 部分，從聯合架構中至少選擇一個同意屬性。 這是必須存在的屬性，以便配置檔案包含在此策略所管轄的操作中。 可以從清單中選擇一個提供的選項，或選擇 **[!UICONTROL 查看全部]** 從聯合架構中直接選擇屬性。

選擇「同意」屬性時，請為要此策略檢查的屬性選擇值。

![](../images/policies/select-schema-field.png)

在您至少選擇了一個同意屬性後， **[!UICONTROL 策略屬性]** 顯示此策略下允許的配置檔案估計數（包括配置檔案儲存總數的百分比）的面板更新。 此估計值在您調整策略配置時自動更新。

![](../images/policies/audience-preview.png)

要向策略添加進一步的同意屬性，請選擇 **[!UICONTROL 添加結果]**。

![](../images/policies/add-result.png)

您可以根據需要繼續為策略添加和調整條件和同意屬性。 如果對配置滿意，請在選擇 **[!UICONTROL 保存]**。

![](../images/policies/name-and-save.png)

現在已建立同意策略，其狀態設定為 [!UICONTROL 已禁用] 預設值。 要立即啟用策略，請選擇 **[!UICONTROL 狀態]** 在右滑軌中切換。

![](../images/policies/enable-consent-policy.png)

#### 驗證策略實施

建立並啟用同意策略後，您可以預覽在將段激活到目標時它如何影響您同意的受眾。 請參閱 [同意政策評估](../enforcement/auto-enforcement.md#consent-policy-evaluation) 的子菜單。

## 啟用或禁用策略 {#enable}

預設情況下，所有資料使用策略(包括由Adobe提供的核心策略)都被禁用。 要考慮實施的單個策略，必須通過API或UI手動啟用該策略。

可以從 **[!UICONTROL 瀏覽]** 的 **[!UICONTROL 策略]** 工作區。 從清單中選擇自定義策略以在右側顯示其詳細資訊。 下 **[!UICONTROL 狀態]**，選擇切換按鈕以啟用或禁用策略。

![](../images/policies/enable-policy.png)

## 查看市場營銷活動 {#view-marketing-actions}

在 **[!UICONTROL 策略]** 工作區，選擇 **[!UICONTROL 市場營銷操作]** 頁籤，查看由Adobe和您自己的組織定義的可用市場營銷活動的清單。

![](../images/policies/marketing-actions.png)

## 建立市場營銷活動 {#create-marketing-action}

要建立新的自定義市場營銷操作，請選擇 **[!UICONTROL 建立市場營銷活動]** 右上角 **[!UICONTROL 市場營銷操作]** 的 **[!UICONTROL 策略]** 工作區。

![](../images/policies/create-marketing-action.png)

的 **[!UICONTROL 建立市場營銷活動]** 對話框。 輸入市場營銷活動的名稱和說明，然後選擇 **[!UICONTROL 建立]**。

![](../images/policies/create-marketing-action-details.png)

新建立的操作將出現在 **[!UICONTROL 市場營銷操作]** 頁籤。 您現在可以在 [建立新資料使用策略](#create-policy)。

![](../images/policies/created-marketing-action.png)

## 編輯或刪除市場營銷操作 {#edit-delete-marketing-action}

>[!NOTE]
>
>只能編輯由您的組織定義的自定義市場營銷活動。 不能更改或刪除由Adobe定義的市場營銷活動。

在 **[!UICONTROL 策略]** 工作區，選擇 **[!UICONTROL 市場營銷操作]** 頁籤，查看由Adobe和您自己的組織定義的可用市場營銷活動的清單。 從清單中選擇自定義市場營銷操作，然後使用右側部分中提供的欄位編輯市場營銷操作的詳細資訊。

![](../images/policies/edit-marketing-action.png)

如果市場營銷活動未被任何現有使用策略使用，您可以通過選擇 **[!UICONTROL 刪除市場營銷操作]**。

>[!NOTE]
>
>嘗試刪除現有策略正在使用的市場營銷操作將導致出現錯誤消息，表明刪除嘗試失敗。

![](../images/policies/delete-marketing-action.png)

## 後續步驟

本文檔概述了如何管理中的資料使用策略 [!DNL Experience Platform] UI。 有關如何使用 [!DNL Policy Service API]，請參見 [開發者指南](../api/getting-started.md)。 有關如何強制實施資料使用策略的資訊，請參見 [策略實施概述](../enforcement/overview.md)。

以下視頻演示了如何使用中的使用策略 [!DNL Experience Platform] UI:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
