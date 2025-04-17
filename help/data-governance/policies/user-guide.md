---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用原則使用手冊
solution: Experience Platform
title: 在UI中管理資料使用原則
description: Adobe Experience Platform資料控管提供使用者介面，可讓您建立和管理資料使用原則。 本檔案概述您可以在Experience Platform使用者介面的「原則」工作區中執行的動作。
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 16%

---

# 管理 UI 中的資料使用原則 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="在您的設定檔資料中整合並強制執行客戶同意"
>abstract="<h2>說明</h2><p>您可以使用 Experience Platform 將向客戶收集而來的同意資料整合到其各自的輪廓中。然後，您可以設定同意原則來確定在已對特定目的地啟用的區段中，是否可以包含這些資料。</p>"

本文介紹如何在Adobe Experience Platform UI中使用&#x200B;**[!UICONTROL 原則]**&#x200B;工作區來建立及管理資料使用原則。

>[!NOTE]
>
>如需有關如何在UI中管理存取控制原則的資訊，請參閱[屬性型存取控制UI指南](../../access-control/abac/ui/policies.md)。

>[!IMPORTANT]
>
>所有資料使用原則(包括Adobe提供的核心原則)預設為停用。 為了考慮執行個別原則，您必須手動啟用該原則。 請參閱[啟用原則](#enable)的相關小節，以瞭解如何在UI中執行此動作的步驟。

## 先決條件

本指南需要深入瞭解下列[!DNL Experience Platform]概念：

* [資料治理](../home.md)
* [資料使用原則](./overview.md)

## 檢視現有原則 {#view-policies}

在[!DNL Experience Platform] UI中，選取&#x200B;**[!UICONTROL 原則]**&#x200B;以開啟&#x200B;**[!UICONTROL 原則]**&#x200B;工作區。 在&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤中，您可以看到可用原則的清單，包括其關聯的標籤、行銷動作和狀態。

![](../images/policies/browse-policies.png)

如果您有同意原則的存取權，請選取&#x200B;**[!UICONTROL 同意原則]**&#x200B;切換按鈕，以便在[!UICONTROL 瀏覽]索引標籤中檢視這些原則。

![](../images/policies/consent-policy-toggle.png)

選取列出的原則以檢視其說明和型別。 如果選取自訂原則，則會顯示其他控制項以編輯、刪除或[啟用/停用原則](#enable)。

![](../images/policies/policy-details.png)

## 建立自訂原則 {#create-policy}

若要建立新的自訂資料使用原則，請在&#x200B;**[!UICONTROL 原則]**&#x200B;工作區的&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤的右上角選取&#x200B;**[!UICONTROL 建立原則]**。

![](../images/policies/create-policy-button.png)

根據您是否為同意政策Beta版的一部分，會發生下列其中一種情況：

* 如果您不屬於Beta版，則會立即進入工作流程，進行[建立資料治理原則](#create-governance-policy)。
* 如果您是Beta版的一員，對話方塊會提供[建立同意原則](#consent-policy)的額外選項。
  ![](../images/policies/choose-policy-type.png)

### 同時使用資料控管和同意原則 {#combine-policies}

>[!NOTE]
>
>同意原則目前僅適用於已購買Adobe Healthcare Shield或Adobe Privacy &amp; Security Shield的組織。

控管和同意原則可搭配使用，以建立強大的規則來控管對應至目的地的對象。 同意原則本質上具包容性，這表示它們指定可包含在每個行銷體驗中的設定檔。 反之，治理原則會排除使用特定標籤屬性，以免設定為要啟動。

使用此行為，您可以設定包含正確設定檔的原則和同意規則組合，但阻止您包含違反已設定組織規則的資料。 範例情境為，您想要排除敏感性資料不包含在內，但仍可透過社群媒體將目標定位為同意的行銷使用者。 此情境的必要步驟概述於以下資訊圖。

![概述使用治理和同意原則來建立治理對象的健全規則之步驟的資訊圖。](../images/policies/governance-and-consent-policies-infographic.png)

### 建立資料治理原則 {#create-governance-policy}

**[!UICONTROL 建立原則]**&#x200B;工作流程隨即顯示。 首先，提供新原則的名稱和說明。

![](../images/policies/create-policy-description.png)

接著，選取原則將依據的資料使用標籤。 選取多個標籤時，您可以選擇資料應包含所有標籤，還是僅包含其中一個，才能套用原則。 完成時選取&#x200B;**[!UICONTROL 下一步]**。

![](../images/policies/add-labels.png)

**[!UICONTROL 選取行銷動作]**&#x200B;步驟隨即顯示。 從提供的清單中選擇適當的行銷動作，然後選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續。

>[!NOTE]
>
>選取多個行銷動作時，原則會將它們解譯為「OR」規則。 換言之，如果執行&#x200B;**任何**&#x200B;選取的行銷動作，就會套用原則。

![](../images/policies/add-marketing-actions.png)

**[!UICONTROL 檢閱]**&#x200B;步驟出現，可讓您在建立新原則之前檢閱其詳細資訊。 在您滿意後，選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立原則。

![](../images/policies/policy-review.png)

**[!UICONTROL 瀏覽]**&#x200B;索引標籤會重新出現，現在會以「草稿」狀態列出新建立的原則。 若要啟用此原則，請參閱下一節。

![](../images/policies/created-policy.png)

### 建立內容原則 {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="說明"
>abstract="<ul><li>確保您透過 OneTrust 來源連接器或標準 XDM 結構描述，將偏好設定資料擷取到您的聯合結構描述以取得同意。</li><li>在左側導覽中選取<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=zh-Hant">原則</a>，然後選取<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">建立原則</a>。</li><li>在 <b>If</b> 區段下，描述將觸發原則檢查的條件或動作。</li><li>在 <b>Then</b> 區塊下，輸入同意屬性，此同意屬性必須存在才能將設定檔包含在觸發原則的動作中。</li><li>選取<b>儲存</b>以建立原則。若要啟用原則，請選取右側邊欄中的 <b>狀態</b>切換。</li><li>當您將區段啟用到目的地時，Experience Platform 會自動強制執行您的已啟用同意原則，並提供每個原則如何影響對象大小的詳細資訊。</li><li>如需有關此功能的更多說明，請參閱 Experience League 上的<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=zh-Hant#consent-policy">建立同意原則</a>指南。</li></ul>"

>[!IMPORTANT]
>
>同意原則僅適用於已購買&#x200B;**Adobe Healthcare Shield**&#x200B;或&#x200B;**Adobe Privacy &amp; Security Shield**&#x200B;的組織。

如果您選擇建立同意原則，則會顯示一個新畫面，供您設定新原則。

![](../images/policies/consent-policy-dialog.png)

為了使用同意政策，您的設定檔資料中必須有同意屬性。 如需如何在聯合結構描述中包含必要屬性的詳細步驟，請參閱Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md)中的[同意處理指南。

同意原則包含兩個邏輯元件：

* **[!UICONTROL If]**：將觸發原則檢查的條件。 這可能根據所執行的特定行銷動作、特定資料使用標籤的出現或兩者的組合。
* **[!UICONTROL Then]**：必須存在同意屬性，設定檔才能包含在觸發原則的動作中。

#### 設定條件 {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="If 條件"
>abstract="首先定義將觸發原則檢查的條件。條件可以包括正在採取的特定行銷動作、存在的特定資料控管標籤，或兩者的組合。"

在&#x200B;**[!UICONTROL If]**&#x200B;區段下，選取應觸發此原則的行銷動作和/或資料使用標籤。 選取&#x200B;**[!UICONTROL 檢視全部]**&#x200B;和&#x200B;**[!UICONTROL 選取標籤]**&#x200B;以分別檢視可用的行銷動作和標籤的完整清單。

新增至少一個條件後，您可以選取&#x200B;**[!UICONTROL 新增條件]**&#x200B;以繼續視需要新增其他條件，並從下拉式清單中選擇適當的條件型別。

![](../images/policies/add-condition.png)

如果您選取多個條件，您可以使用它們之間顯示的圖示，來切換「與」與「或」之間的條件式關係。

![](../images/policies/and-or-selection.png)

#### 選取同意屬性 {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Then 條件"
>abstract="定義「If」條件後，使用「Then」部分從聯合結構描述中選擇至少一個同意屬性。此屬性必須存在，如此設定檔才能包含在此原則控管的動作中。"

在&#x200B;**[!UICONTROL Then]**&#x200B;區段下，從聯合結構描述中選取至少一個同意屬性。 這是必須存在的屬性，才能將設定檔納入此原則所控管的動作中。 您可以從清單中選擇其中一個提供的選項，或選取[檢視全部]，以直接從聯合結構描述中選擇屬性。****

選取同意屬性時，請選擇您要此原則檢查的屬性值。

![](../images/policies/select-schema-field.png)

選取至少一個同意屬性後，**[!UICONTROL 原則屬性]**&#x200B;面板會更新，以顯示此原則允許的預估設定檔數目，包括設定檔存放區總數的百分比。 當您調整原則設定時，此估計會自動更新。

![](../images/policies/audience-preview.png)

若要新增更多同意屬性至原則，請選取&#x200B;**[!UICONTROL 新增結果]**。

![](../images/policies/add-result.png)

您可以視需要繼續新增及調整條件和同意屬性至原則。 在您滿意組態之後，請先提供原則名稱與選擇性說明，再選取&#x200B;**[!UICONTROL 儲存]**。

![](../images/policies/name-and-save.png)

同意原則現在已建立，其狀態預設為[!UICONTROL 已停用]。 若要立即啟用原則，請選取右側邊欄中的&#x200B;**[!UICONTROL 狀態]**&#x200B;切換按鈕。

![](../images/policies/enable-consent-policy.png)

#### 驗證原則執行

建立並啟用同意原則後，您可以預覽原則在啟用區段至目的地時，對您同意的對象有何影響。 如需詳細資訊，請參閱[同意原則評估](../enforcement/auto-enforcement.md#consent-policy-evaluation)的相關章節。

## 啟用或停用原則 {#enable}

所有資料使用原則(包括Adobe提供的核心原則)預設為停用。 對於要考慮強制執行的個別原則，您必須透過API或UI手動啟用該原則。

您可以從&#x200B;**[!UICONTROL 原則]**&#x200B;工作區的&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤啟用或停用原則。 從清單中選取自訂原則，以在右側顯示其詳細資訊。 在&#x200B;**[!UICONTROL 狀態]**&#x200B;下，選取切換按鈕以啟用或停用原則。

![](../images/policies/enable-policy.png)

## 檢視行銷動作 {#view-marketing-actions}

在&#x200B;**[!UICONTROL 原則]**&#x200B;工作區中，選取&#x200B;**[!UICONTROL 行銷動作]**&#x200B;索引標籤，以檢視Adobe與您自己的組織所定義的可用行銷動作清單。

![](../images/policies/marketing-actions.png)

## 建立行銷動作 {#create-marketing-action}

若要建立新的自訂行銷動作，請在&#x200B;**[!UICONTROL 原則]**&#x200B;工作區中&#x200B;**[!UICONTROL 行銷動作]**&#x200B;索引標籤的右上角選取&#x200B;**[!UICONTROL 建立行銷動作]**。

![](../images/policies/create-marketing-action.png)

**[!UICONTROL 建立行銷動作]**&#x200B;對話方塊就會顯示。 輸入行銷動作的名稱和描述，然後選取&#x200B;**[!UICONTROL 建立]**。

![](../images/policies/create-marketing-action-details.png)

新建立的動作會出現在&#x200B;**[!UICONTROL 行銷動作]**&#x200B;標籤中。 您現在可以在[建立新的資料使用原則](#create-policy)時使用行銷動作。

![](../images/policies/created-marketing-action.png)

## 編輯或刪除行銷動作 {#edit-delete-marketing-action}

>[!NOTE]
>
>只能編輯您組織定義的自訂行銷動作。 Adobe定義的行銷動作無法變更或刪除。

在&#x200B;**[!UICONTROL 原則]**&#x200B;工作區中，選取&#x200B;**[!UICONTROL 行銷動作]**&#x200B;索引標籤，以檢視Adobe與您自己的組織所定義的可用行銷動作清單。 從清單中選取自訂行銷動作，然後使用右側區段中提供的欄位來編輯行銷動作的詳細資訊。

![](../images/policies/edit-marketing-action.png)

如果任何現有使用原則未使用行銷動作，您可以選取&#x200B;**[!UICONTROL 刪除行銷動作]**&#x200B;來刪除它。

>[!NOTE]
>
>嘗試刪除現有原則正在使用的行銷動作會導致出現錯誤訊息，指出刪除嘗試失敗。

![](../images/policies/delete-marketing-action.png)

## 後續步驟

本檔案概述如何在[!DNL Experience Platform] UI中管理資料使用原則。 如需有關如何使用[!DNL Policy Service API]管理原則的步驟，請參閱[開發人員指南](../api/getting-started.md)。 如需如何強制執行資料使用原則的相關資訊，請參閱[原則執行概觀](../enforcement/overview.md)。

下列影片示範如何在[!DNL Experience Platform] UI中使用使用原則：

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
