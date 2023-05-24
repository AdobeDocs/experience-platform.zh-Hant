---
keywords: Experience Platform；主題；熱門主題；訪問控制；基於屬性的訪問控制；
title: 基於屬性的訪問控制端到端指南
description: 本文檔提供了Adobe Experience Platform基於屬性的訪問控制的端到端指南
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: 004f6183f597132629481e3792b5523317b7fb2f
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 19%

---

# 基於屬性的訪問控制端到端指南

基於屬性的訪問控制是Adobe Experience Platform公司的一項功能，它為多品牌和注重隱私的客戶提供了管理用戶訪問的更大靈活性。 可以使用基於對象屬性和角色的策略來授予/拒絕對單個對象（如架構欄位和段）的訪問。 此功能允許您授予或撤消組織中特定平台用戶對單個對象的訪問權限。

此功能允許您使用定義組織或資料使用範圍的標籤對架構欄位、段等進行分類。 您可以將這些相同的標籤應用於Adobe Journey Optimizer的旅程、優惠和其他對象。 同時，管理員可以定義圍繞體驗資料模型(XDM)架構欄位的訪問策略，並更好地管理哪些用戶或組（內部、外部或第三方用戶）可以訪問這些欄位。

>[!NOTE]
>
>本文檔重點介紹訪問控制策略的使用案例。 如果您試圖設定策略來管理 **使用** 的端到端指南，請參閱 [資料治理](../../data-governance/e2e.md) 的雙曲餘切值。

## 快速入門

本教程需要瞭解以下平台元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [Adobe Experience Platform分段服務](../../segmentation/home.md):分段引擎 [!DNL Platform] 用於根據客戶行為和屬性從客戶配置檔案建立受眾段。

### 用例概述

您將通過一個基於屬性的訪問控制工作流示例，在該工作流中，您將建立和分配角色、標籤和策略，以配置用戶是否可以訪問組織中的特定資源。 本指南使用限制對敏感資料的訪問的示例來演示工作流。 此使用案例概述如下：

您是醫療保健提供商，希望配置對組織中資源的訪問權。

* 您的內部營銷團隊應能夠 **[!UICONTROL PHI/受管制的健康資料]** 資料。
* 您的外部機構應無法訪問 **[!UICONTROL PHI/受管制的健康資料]** 資料。

要執行此操作，必須配置角色、資源和策略。

您將：

* [為用戶標籤角色](#label-roles):請使用其市場營銷組與外部代理機構合作的醫療保健提供商（ACME業務組）的示例。
* [標籤資源（架構欄位和段）](#label-resources):分配 **[!UICONTROL PHI/受管制的健康資料]** 標籤到架構資源和段。
* 
   * [激活將它們連結在一起的策略： ](#policy):啟用預設策略，通過將資源上的標籤連接到角色中的標籤來防止訪問架構欄位和段。 然後，具有匹配標籤的用戶將有權訪問所有沙箱中的架構欄位和段。

## 權限

[!UICONTROL 權限] 是Experience Cloud區域，管理員可以在該區域定義用戶角色和策略，以管理產品應用程式中功能和對象的權限。

通過 [!UICONTROL 權限]，您可以建立和管理角色，並為這些角色分配所需的資源權限。 [!UICONTROL 權限也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。]

如果您沒有管理員權限，請與系統管理員聯繫以獲得訪問權限。

一旦您具有管理員權限，請轉到 [Adobe Experience Cloud](https://experience.adobe.com/) 並使用您的Adobe憑據登錄。 登錄後， **[!UICONTROL 概述]** 頁面。 此頁顯示您的組織訂閱的產品以及向組織添加用戶和管理員的其他控制項。 選擇 **[!UICONTROL 權限]** 開啟用於平台整合的工作區。

![顯示在Adobe Experience Cloud中選擇的「權限」產品的影像](../images/flac-ui/flac-select-product.png)

將顯示「平台UI的權限」工作區，在 **[!UICONTROL 角色]** 的子菜單。

## 將標籤應用於角色 {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="什麼是標籤？"
>abstract="標籤可讓您根據適用於該資料的使用原則對資料集和欄位進行分類。平台提供了幾個 Adobe 定義的「核心」資料使用標籤，涵蓋了適用於資料控管的各種常見限制。例如，敏感資料「S」標籤 (例如 RHD (受監管的健康資料))，可讓您將受保護的健康資訊 (PHI) 加以分類。您也可以定義適合您組織需求的自訂標籤。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="資料使用標籤總覽"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="建立新標籤"
>abstract="您可以建立適合您組織需求的自訂標籤。自訂標籤可用於資料控管和存取控制設定套用到您的資料。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="管理自訂標籤"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="什麼是角色？"
>abstract="角色用於分類與 Platform 執行個體互動的使用者類型，也是存取控制原則的組成要素。一個角色具有一組給定的權限，您的組織成員可以指派到一個或多個角色，依據他們需要的視圖範圍或寫入權限而定。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="管理角色"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="建立新角色"
>abstract="您可以建立一個新角色以更好地分類存取您 Platform 執行個體的使用者。例如，您可以為內部行銷團隊建立角色並將 RHD 標籤套用到該角色，從而允許您的內部行銷團隊存取受保護的健康資訊 (PHI)。或者，您也可以為外部機構建立一個角色，且不將 RHD 標籤套用到該角色來拒絕該角色存取 PHI 資料。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="建立新角色"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="角色概觀"
>abstract="角色概觀對話框顯示給定角色可存取的資源和沙箱。"

角色是對與平台實例交互的用戶類型進行分類的方法，是訪問控制策略的構建基塊。 某個角色具有給定的一組權限，您組織的成員可以分配給一個或多個角色，具體取決於他們需要的訪問範圍。

要開始，請選擇 **[!UICONTROL ACME業務組]** 從 **[!UICONTROL 角色]** 的子菜單。

![顯示在角色中選擇的ACME業務角色的影像](../images/abac-end-to-end-user-guide/abac-select-role.png)

下一步，選擇 **[!UICONTROL 標籤]** ，然後選擇 **[!UICONTROL 添加標籤]**。

![顯示在「標籤」頁籤上選擇的「添加標籤」的影像](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

此時將顯示組織中所有標籤的清單。 選擇 **[!UICONTROL RHD]** 添加標籤 **[!UICONTROL PHI/受管制的健康資料]**。 允許在標籤旁邊出現藍色複選標籤，然後選擇 **[!UICONTROL 保存]**。

![顯示正在選擇和保存的RHD標籤的影像](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>將組織組添加到角色時，該組中的所有用戶都將添加到該角色。 對組織組（刪除或添加的用戶）的任何更改將在角色中自動更新。

## 將標籤應用於架構欄位 {#label-resources}

現在，您已使用 [!UICONTROL RHD] 標籤，下一步是將該標籤添加到要控制該角色的資源中。

選擇 **[!UICONTROL 架構]** 從左側導航中，然後選擇 **[!UICONTROL ACME醫療保健]** 框中。

![顯示從「方案」頁籤中選擇的ACME醫療保健方案的影像](../images/abac-end-to-end-user-guide/abac-select-schema.png)

下一步，選擇 **[!UICONTROL 標籤]** 查看顯示與方案關聯的欄位的清單。 在此處，您可以一次將標籤分配給一個或多個欄位。 選擇 **[!UICONTROL 血糖]** 和 **[!UICONTROL 胰島素水準]** 欄位，然後選擇 **[!UICONTROL 應用訪問和資料治理標籤]**。

![顯示正在選擇的血糖和胰島素水準並應用正在選擇的訪問和資料治理標籤的影像](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

的 **[!UICONTROL 編輯標籤]** 對話框，允許您選擇要應用於架構欄位的標籤。 對於此用例，選擇 **[!UICONTROL PHI/受管制的健康資料]** 標籤，然後選擇 **[!UICONTROL 保存]**。

![顯示正在選擇和保存的RHD標籤的影像](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>在將標籤添加到欄位時，該標籤將應用於該欄位的父資源（類或欄位組）。 如果父類或欄位組被其他方案使用，則這些方案將繼承相同的標籤。

## 將標籤應用於段

在完成對架構欄位的標籤後，現在可以開始標籤段。

選擇 **[!UICONTROL 段]** 的上界。 將顯示組織中可用段的清單。 在本示例中，將標籤以下兩個段，因為它們包含敏感健康資料：

* 血糖>100
* 胰島素&lt;50

選擇 **[!UICONTROL 血糖>100]** 開始標籤段。

![顯示從「段」頁籤中選擇的血糖>100的影像](../images/abac-end-to-end-user-guide/abac-select-segment.png)

分部 **[!UICONTROL 詳細資訊]** 的上界。 選擇 **[!UICONTROL 管理訪問]**。

![顯示「管理」訪問選擇的影像](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

的 **[!UICONTROL 編輯標籤]** 對話框，允許您選擇要應用於段的標籤。 對於此用例，選擇 **[!UICONTROL PHI/受管制的健康資料]** 標籤，然後選擇 **[!UICONTROL 保存]**。

![顯示所選RHD標籤和保存的影像](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

重複上述步驟 **[!UICONTROL 胰島素&lt;50]**。

## 激活訪問控制策略 {#policy}

預設訪問控制策略將利用標籤來定義哪些用戶角色有權訪問特定平台資源。 在本示例中，對於不在架構欄位中具有相應標籤的角色的用戶，將在所有沙箱中拒絕訪問架構欄位和段。

要激活訪問控制策略，請選擇 [!UICONTROL 權限] 從左側導航中，然後選擇 **[!UICONTROL 策略]**。

![顯示的策略清單](../images/abac-end-to-end-user-guide/abac-policies-page.png)

接下來，選擇省略號(`...`)旁邊，下拉清單將顯示編輯、激活、刪除或複製角色的控制項。 選擇 **[!UICONTROL 激活]** 的下界。

![要激活策略的下拉清單](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

此時將顯示激活策略對話框，提示您確認激活。 選擇 **[!UICONTROL 確認]**。

![激活策略對話框](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

接收策略激活的確認，並返回到 [!UICONTROL 策略] 的子菜單。

![激活策略確認](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.

To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## 後續步驟

您已完成將標籤應用到角色、架構欄位和段。 分配給這些角色的外部代理在架構、資料集和配置檔案視圖中禁止查看這些標籤及其值。 使用「段生成器」時，這些欄位也限制在段定義中使用。

有關基於屬性的訪問控制的詳細資訊，請參閱 [基於屬性的訪問控制概述](./overview.md)。
