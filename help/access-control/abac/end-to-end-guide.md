---
keywords: Experience Platform；首頁；熱門主題；存取控制；基於屬性的存取控制；
title: 基於屬性的訪問控制端到端指南
description: 本檔案提供Adobe Experience Platform中以屬性為基礎的存取控制的端對端指南
hide: true
hidefromtoc: true
source-git-commit: 440176ea1f21db3c7c4b3572fb52771dc70c80a0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 基於屬性的訪問控制端到端指南

基於屬性的存取控制是Adobe Experience Platform的一項功能，可讓注重隱私的品牌有更大的彈性來管理使用者存取。 可將個別物件（例如結構欄位和區段）指派給使用者角色。 此功能可讓您授予或撤銷組織中特定Platform使用者對個別物件的存取權。

此功能可讓您使用定義組織或資料使用範圍的標籤，對結構欄位、區段等進行分類。 在Adobe Journey Optimizer中，您可以將這些相同的標籤套用至歷程和選件。 同時，管理員可以定義XDM結構欄位的存取原則，並更妥善地管理哪些使用者或群組（內部、外部或第三方使用者）可以存取這些欄位。

## 快速入門

本教學課程需要妥善了解下列平台元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [Adobe Experience Platform區段服務](../../segmentation/home.md):內的分段引擎 [!DNL Platform] 用於根據客戶行為和屬性，從您的客戶設定檔建立受眾區段。

### 使用案例概觀

本指南使用限制存取敏感資料的範例使用案例來示範工作流程。 您將執行一個基於屬性的訪問控制工作流示例，在該工作流中，您將建立並分配角色、標籤和策略，以配置您的用戶是否可以訪問組織中的某些資源。 此使用案例概述如下：

您是醫療保健提供商，並且想要配置對組織中資源的訪問。

* 您的內部行銷團隊應能存取 **[!UICONTROL PHI/受管制的健康資料]** 資料。
* 您的外部機構應無法訪問 **[!UICONTROL PHI/受管制的健康資料]** 資料。

要執行此操作，您必須設定角色、資源和原則。

您會：

* [為您的使用者標籤角色]{#label-roles}:以其行銷組與外部代理合作的醫療保健提供商（ACME業務組）為例。
* [標示資源（結構欄位和區段）]{#label-resources}:指派 **[!UICONTROL PHI/受管制的健康資料]** 標籤至架構資源和區段。
* [建立將它們連結在一起的策略]{#policy}:建立原則，將資源上的標籤連結至您角色中的標籤，拒絕存取架構欄位和區段。 對於沒有相符標籤的使用者，這會拒絕其存取所有沙箱中的結構欄位和區段。

## 權限

[!UICONTROL 權限] 是Experience Cloud的區域，管理員可在此定義用戶角色和訪問策略，以管理產品應用程式內功能和對象的訪問權限。

通過 [!UICONTROL 權限]，您可以建立和管理角色，並為這些角色指派所需的資源權限。 [!UICONTROL 權限] 也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。

如果您沒有管理員權限，請連絡您的系統管理員以取得存取權。

取得管理員權限後，請前往 [Adobe Experience Cloud](https://experience.adobe.com/) 並使用您的Adobe憑證登入。 登入後， **[!UICONTROL 概述]** 會針對您擁有管理員權限的組織顯示頁面。 此頁面顯示貴組織訂閱的產品，以及可新增使用者和管理員至整個組織的其他控制項。 選擇 **[!UICONTROL 權限]** 以開啟您的平台整合工作區。

![顯示在Adobe Experience Cloud中選取之權限產品的影像](../images/flac-ui/flac-select-product.png)

Platform UI的「權限」工作區隨即顯示，在 **[!UICONTROL 角色]** 頁面。

## 將標籤應用於角色 {#label-roles}

角色是將與您的Platform例項互動的使用者類型分類，並且是存取控制原則的基礎要素。 角色具有一組指定的權限，而您組織的成員可依其需要的存取範圍，指派給一或多個角色。

若要開始，請選取 **[!UICONTROL ACME Business Group]** 從 **[!UICONTROL 角色]** 頁面。

![此影像顯示在「角色」中選擇的ACME業務角色](../images/abac-end-to-end-user-guide/abac-select-role.png)

下一步，選擇 **[!UICONTROL 標籤]** 然後選取 **[!UICONTROL 新增標籤]**.

![在「標籤」頁簽上顯示「添加標籤」的影像](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

組織中所有標籤的清單隨即顯示。 選擇 **[!UICONTROL RHD]** 為添加標籤 **[!UICONTROL PHI/受管制的健康資料]**. 讓藍色勾號在標籤旁出現幾分鐘，然後選取 **[!UICONTROL 儲存]**.

![顯示正在選擇和保存的RHD標籤的影像](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

## 將標籤應用於架構欄位 {#label-resources}

現在您已使用 [!UICONTROL RHD] 標籤，下一步是將相同標籤新增至您要控制該角色的資源。

選擇 **[!UICONTROL 結構]** 從左側導覽列中，然後選取 **[!UICONTROL ACME Healthcare]** 從顯示的結構清單中。

![顯示從「結構」頁簽中選擇的ACME醫療保健結構的影像](../images/abac-end-to-end-user-guide/abac-select-schema.png)

下一步，選擇 **[!UICONTROL 標籤]** 以查看顯示與架構關聯欄位的清單。 從這裡，您可以一次將標籤指派給一或多個欄位。 選取 **[!UICONTROL 血糖]** 和 **[!UICONTROL 胰島素水準]** 欄位，然後選取 **[!UICONTROL 編輯控管標籤]**.

![顯示正在選擇的血糖和胰島素水準的影像，並編輯正在選擇的治理標籤](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

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

存取控制原則會利用標籤來定義哪些使用者角色可存取特定平台資源。 策略可以是本地策略或全局策略，也可以覆蓋其他策略。 在此範例中，對於架構欄位中沒有對應標籤的使用者，在所有沙箱中都會拒絕存取架構欄位和區段。

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
