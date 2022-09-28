---
keywords: Experience Platform；首頁；熱門主題；存取控制；基於屬性的存取控制；
title: 基於屬性的訪問控制端到端指南
description: 本檔案提供Adobe Experience Platform中以屬性為基礎的存取控制的端對端指南
source-git-commit: 0035f4611f2c269bb36f045c3c57e6e7bad7c013
workflow-type: tm+mt
source-wordcount: '2382'
ht-degree: 0%

---

# 基於屬性的訪問控制端到端指南

基於屬性的存取控制是Adobe Experience Platform的一項功能，可讓多品牌和注重隱私的客戶擁有更大的彈性來管理使用者存取。 可以根據對象的屬性和角色使用策略來授予/拒絕對單個對象（如方案欄位和段）的訪問權。 此功能可讓您授予或撤銷組織中特定Platform使用者對個別物件的存取權。

此功能可讓您使用定義組織或資料使用範圍的標籤，對結構欄位、區段等進行分類。 您可以將這些相同的標籤套用至Adobe Journey Optimizer中的歷程、選件和其他物件。 同時，管理員可以定義XDM結構欄位的存取原則，並更妥善地管理哪些使用者或群組（內部、外部或第三方使用者）可以存取這些欄位。


## 快速入門

本教學課程需要妥善了解下列平台元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [Adobe Experience Platform區段服務](../../segmentation/home.md):內的分段引擎 [!DNL Platform] 用於根據客戶行為和屬性，從您的客戶設定檔建立受眾區段。

### 使用案例概觀

您將執行一個基於屬性的訪問控制工作流示例，在該工作流中，您將建立並分配角色、標籤和策略，以配置您的用戶是否可以訪問組織中的特定資源。 本指南使用限制存取敏感資料的範例來示範工作流程。 此使用案例概述如下：

您是醫療保健提供商，希望配置對組織中資源的訪問。

* 您的內部行銷團隊應能存取 **[!UICONTROL PHI/受管制的健康資料]** 資料。
* 您的外部機構應無法訪問 **[!UICONTROL PHI/受管制的健康資料]** 資料。

要執行此操作，您必須設定角色、資源和原則。

您會：

* [為您的使用者標籤角色](#label-roles):以其行銷組與外部代理合作的醫療保健提供商（ACME業務組）為例。
* [標示資源（結構欄位和區段）](#label-resources):指派 **[!UICONTROL PHI/受管制的健康資料]** 標籤至架構資源和區段。
* [建立將它們連結在一起的策略](#policy):建立原則以將資源上的標籤連結至您角色中的標籤，拒絕存取結構欄位和區段。 對於沒有相符標籤的使用者，這會拒絕其存取所有沙箱中的結構欄位和區段。

## 權限

[!UICONTROL 權限] 是Experience Cloud的區域，管理員可在其中定義用戶角色和策略，以管理產品應用程式內的功能和對象的權限。

通過 [!UICONTROL 權限]，您可以建立和管理角色，並為這些角色指派所需的資源權限。 [!UICONTROL 權限] 也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。

如果您沒有管理員權限，請連絡您的系統管理員以取得存取權。

取得管理員權限後，請前往 [Adobe Experience Cloud](https://experience.adobe.com/) 並使用您的Adobe憑證登入。 登入後， **[!UICONTROL 概述]** 會針對您擁有管理員權限的組織顯示頁面。 此頁面顯示您組織訂閱的產品，以及新增使用者和管理員至組織的其他控制項。 選擇 **[!UICONTROL 權限]** 以開啟您的平台整合工作區。

![顯示在Adobe Experience Cloud中選取之權限產品的影像](../images/flac-ui/flac-select-product.png)

Platform UI的「權限」工作區隨即顯示，在 **[!UICONTROL 角色]** 頁面。

## 將標籤應用於角色 {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="標籤是什麼？"
>abstract="標籤可讓您根據套用至該資料的使用原則，對資料集和欄位進行分類。 Platform提供數個Adobe定義的「核心」資料使用標籤，涵蓋適用於資料控管的各種常見限制。 例如，敏感的「S」標籤(如RHD（受管理的運行狀況資料）)允許您對引用受保護的運行狀況資訊(PHI)的資料進行分類。 您也可以定義符合組織需求的自訂標籤。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="資料使用標籤總覽"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="建立新標籤"
>abstract="您可以建立自訂標籤，以符合組織的需求。 自訂標籤可用來將資料控管和存取控制設定同時套用至您的資料。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="管理自訂標籤"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="什麼是角色？"
>abstract="角色是將與您的Platform例項互動，且是存取控制原則基礎的使用者類型分類的方法。 角色具有一組指定的權限，而您組織的成員可以根據其所需的檢視或寫入存取範圍，指派給一或多個角色。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="管理角色"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="建立新角色"
>abstract="您可以建立新角色，以便對存取您的Platform例項的使用者進行更妥善的分類。 例如，您可以為內部營銷團隊建立角色，並將RHD標籤應用到該角色，從而允許您的內部營銷團隊訪問受保護的健康資訊(PHI)。 或者，您也可以為外部代理建立角色，並不將RHD標籤應用到該角色，從而拒絕該角色對PHI資料的訪問。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="建立新角色"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="角色概觀"
>abstract="角色概述對話方塊會顯示指定角色有權存取的資源和沙箱。"

角色是將與您的Platform例項互動的使用者類型分類的方法，也是存取控制原則的基礎要素。 角色具有一組指定的權限，而您組織的成員可依其需要的存取範圍，指派給一或多個角色。

若要開始，請選取 **[!UICONTROL ACME Business Group]** 從 **[!UICONTROL 角色]** 頁面。

![此影像顯示在「角色」中選擇的ACME業務角色](../images/abac-end-to-end-user-guide/abac-select-role.png)

下一步，選擇 **[!UICONTROL 標籤]** 然後選取 **[!UICONTROL 新增標籤]**.

![在「標籤」頁簽上顯示「添加標籤」的影像](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

組織中所有標籤的清單隨即顯示。 選擇 **[!UICONTROL RHD]** 為添加標籤 **[!UICONTROL PHI/受管制的健康資料]**. 讓藍色勾號在標籤旁出現幾分鐘，然後選取 **[!UICONTROL 儲存]**.

![顯示正在選擇和保存的RHD標籤的影像](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>將組織群組新增至角色時，該群組中的所有使用者都會新增至角色。 對組織群組所做的任何變更（移除或新增的使用者）都會在角色內自動更新。

## 將標籤應用於架構欄位 {#label-resources}

現在您已使用 [!UICONTROL RHD] 標籤，下一步是將相同標籤新增至您要控制該角色的資源。

選擇 **[!UICONTROL 結構]** 從左側導覽列中，然後選取 **[!UICONTROL ACME Healthcare]** 從顯示的結構清單中。

![顯示從「結構」頁簽中選擇的ACME醫療保健結構的影像](../images/abac-end-to-end-user-guide/abac-select-schema.png)

下一步，選擇 **[!UICONTROL 標籤]** 以查看顯示與架構關聯欄位的清單。 從這裡，您可以一次將標籤指派給一或多個欄位。 選取 **[!UICONTROL 血糖]** 和 **[!UICONTROL 胰島素水準]** 欄位，然後選取 **[!UICONTROL 套用存取權和資料控管標籤]**.

![該影像顯示正在選擇的血糖和胰島素水準，並應用正在選擇的訪問和資料控管標籤](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

此 **[!UICONTROL 編輯標籤]** 對話框，可讓您選擇要應用到架構欄位的標籤。 針對此使用案例，選取 **[!UICONTROL PHI/受管制的健康資料]** 標籤，然後選取 **[!UICONTROL 儲存]**.

![顯示正在選擇和保存的RHD標籤的影像](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>將標籤添加到欄位時，該標籤將應用到該欄位的父資源（類或欄位組）。 如果父類或欄位組被其他方案採用，則這些方案將繼承相同的標籤。

## 將標籤套用至區段

完成架構欄位的標籤後，您現在可以開始標籤區段。

選擇 **[!UICONTROL 區段]** 從左側導覽。 隨即顯示組織中可用的區段清單。 在此範例中，以下兩個區段的標籤為包含敏感健康資料：

* 血糖>100
* 胰島素&lt;50

選擇 **[!UICONTROL 血糖>100]** 開始為區段加上標籤。

![顯示從「區段」標籤中選取的「血糖>100」的影像](../images/abac-end-to-end-user-guide/abac-select-segment.png)

區段 **[!UICONTROL 詳細資料]** 畫面。 選擇 **[!UICONTROL 管理存取]**.

![顯示選擇「管理」訪問的影像](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

此 **[!UICONTROL 編輯標籤]** 對話方塊，讓您選擇要套用至區段的標籤。 針對此使用案例，選取 **[!UICONTROL PHI/受管制的健康資料]** 標籤，然後選取 **[!UICONTROL 儲存]**.

![顯示所選RHD標籤和保存的影像](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

使用 **[!UICONTROL 胰島素&lt;50]**.

## 建立訪問控制策略 {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="什麼是政策？"
>abstract="政策是將屬性集合在一起，以制定允許和不允許的行動的聲明。 每個組織都會提供預設原則，您必須啟用此原則，才能定義區段和結構欄位等資源的規則。 不能編輯或刪除預設策略。 但是，可以激活或停用預設策略。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="管理原則"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="建立原則"
>abstract="建立原則以定義使用者可以和無法對您的區段和結構欄位採取的動作。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="建立原則"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="為策略配置允許和不允許的操作"
>abstract="A <b>拒絕訪問</b> 當符合條件時，原則會拒絕使用者存取。 結合 <b>以下為false</b>  — 除非所有用戶都符合匹配標準集，否則他們將被拒絕訪問。 此類型的策略允許您保護敏感資源，並僅允許訪問具有匹配標籤的用戶。 <br>A <b>允許訪問</b> 當符合條件時，原則將允許使用者存取。 結合時 <b>以下為true</b>  — 如果使用者符合相符的條件集，即可取得存取權。 這不會明確拒絕使用者的存取權，但會新增允許存取權。 此類型的策略允許您提供對資源的額外訪問，以及那些可能已經通過角色權限擁有訪問權限的用戶。」</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="編輯策略"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="配置資源的權限"
>abstract="資源是使用者可以或無法存取的資產或物件。 資源可以是區段或結構欄位。 您可以為區段和結構欄位設定寫入、讀取或刪除權限。"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="編輯條件"
>abstract="將條件陳述式套用至您的原則，以設定使用者對特定資源的存取權。 選擇「全部匹配」以要求用戶具有與資源具有相同標籤的角色以允許訪問。 選擇「匹配」以要求用戶具有一個角色，該角色只有一個標籤與資源上的標籤匹配。 標籤可定義為核心或自訂標籤，核心標籤代表Adobe建立和提供的標籤，自訂標籤代表您為組織建立的標籤。"

存取控制原則會利用標籤來定義哪些使用者角色可存取特定平台資源。 策略可以是本地策略，也可以是全局策略，並可以覆蓋其他策略。 在此範例中，對於架構欄位中沒有對應標籤的使用者，在所有沙箱中都會拒絕存取架構欄位和區段。

>[!NOTE]
>
>系統會建立「拒絕原則」來授與敏感資源的存取權，因為角色會授予主體的權限。 本示例中的書面策略 **否認** 如果缺少必要標籤，則可以訪問。

要建立訪問控制策略，請選擇 **[!UICONTROL 權限]** 從左側導覽列中，然後選取 **[!UICONTROL 原則]**. 下一步，選擇 **[!UICONTROL 建立原則]**.

![顯示在「權限」中選擇的「建立」策略的影像](../images/abac-end-to-end-user-guide/abac-create-policy.png)

此 **[!UICONTROL 建立新策略]** 對話框，提示您輸入名稱和可選說明。 選擇 **[!UICONTROL 確認]** 完成時。

![顯示「建立新策略」對話框並選擇「確認」的影像](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

要拒絕對架構欄位的訪問，請使用下拉箭頭並選擇 **[!UICONTROL 拒絕訪問]** 然後選取 **[!UICONTROL 未選擇資源]**. 下一步，選擇 **[!UICONTROL 架構欄位]** 然後選取 **[!UICONTROL 全部]**.

![顯示已選擇拒絕訪問和資源的影像](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

下表顯示了建立策略時可用的條件：

| 條件 | 說明 |
| --- | --- |
| 以下為false | 設定「拒絕存取」時，如果使用者不符合選取的條件，則會限制存取。 |
| 以下為true | 當設定「允許訪問」時，如果用戶滿足所選標準，則允許訪問。 |
| 符合任何 | 使用者的標籤符合套用至資源的任何標籤。 |
| 符合所有 | 使用者的所有標籤都符合套用至資源的所有標籤。 |
| 核心標籤 | 核心標籤是Adobe定義的標籤，可在所有Platform執行個體中使用。 |
| 自訂標籤 | 自訂標籤是貴組織已建立的標籤。 |

選擇 **[!UICONTROL 以下為false]** 然後選取 **[!UICONTROL 未選擇屬性]**. 接下來，選取使用者 **[!UICONTROL 核心標籤]**，然後選取 **[!UICONTROL 符合所有]**. 選取資源 **[!UICONTROL 核心標籤]** 最後選取 **[!UICONTROL 新增資源]**.

![顯示所選條件和新增所選資源的影像](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>資源是主體可以或無法存取的資產或物件。 資源可以是區段或結構。

若要拒絕區段的存取，請使用下拉式箭頭並選取 **[!UICONTROL 拒絕訪問]** 然後選取 **[!UICONTROL 未選擇資源]**. 下一步，選擇 **[!UICONTROL 區段]** 然後選取 **[!UICONTROL 全部]**.

選擇 **[!UICONTROL 以下為false]** 然後選取 **[!UICONTROL 未選擇屬性]**. 接下來，選取使用者 **[!UICONTROL 核心標籤]**，然後選取 **[!UICONTROL 符合所有]**. 選取資源 **[!UICONTROL 核心標籤]** 最後選取 **[!UICONTROL 儲存]**.

![顯示已選條件和已選保存的影像](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

選擇 **[!UICONTROL 啟動]** 要激活策略，將顯示一個對話框，提示您確認激活。 選擇 **[!UICONTROL 確認]** 然後選取 **[!UICONTROL 關閉]**.

![顯示正在激活的策略的影像 ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## 後續步驟

您已完成將標籤套用至角色、結構欄位和區段的作業。 指派給這些角色的外部代理受限於無法在結構、資料集和設定檔檢視中檢視這些標籤及其值。 使用「區段產生器」時，這些欄位也無法用於區段定義中。

有關基於屬性的訪問控制的詳細資訊，請參見 [基於屬性的訪問控制概述](./overview.md).
