---
keywords: Experience Platform；首頁；熱門主題；產品設定檔；管理許可權
solution: Experience Platform
title: 管理產品設定檔的許可權
description: Adobe Experience Platform中的存取控制可讓您使用Adobe Admin Console管理各種Platform功能的角色和許可權。 本檔案可用作如何管理Platform產品設定檔許可權的指南。
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: 1812af74e82f3071963177356b3cd4b23ea567f5
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# 管理產品設定檔的許可權

緊接在 [建立新的產品設定檔](#create-a-new-product-profile)，系統會提示您設定設定檔的許可權。 如果您正在編輯現有設定檔的許可權，請從以下位置選取設定檔： **[!UICONTROL 產品設定檔]** 標籤以開啟設定檔的詳細資訊頁面，然後選取 **[!UICONTROL 許可權]**.

![許可權](../images/permissions.png)

許可權分為不同類別，並列於本頁面。 清單會顯示類別名稱、其包含的許可權數（以及有效數量）及其說明。 請參閱中的表格 [資源許可權](/help/access-control/home.md#permissions) 以取得每個角色的可用許可權劃分。

在清單中選取任何類別以開啟 **[!UICONTROL 編輯許可權]** 頁面。

![edit-permissions](../images/edit-permissions.png)

此 **[!UICONTROL 編輯許可權]** 頁面提供工作區，可在所選產品設定檔中新增與移除許可權。 畫面左側會顯示許可權類別的清單。 選取類別會變更下顯示的許可權 **[!UICONTROL 可用的許可權專案]**.

例如，若要更新資料建模的許可權，請選取 **[!UICONTROL 資料模式]**.

![設定檔管理](../images/profile-management.png)

若要新增許可權，請選取加號 **(+)** 圖示加以存取（位於許可權名稱旁）。 或者，您可以選取 **[!UICONTROL 全部新增]** 將目前類別下的所有許可權新增到設定檔。 新增的許可權會顯示在下方 **[!UICONTROL 包含的許可權專案]**.

![add-permission](../images/add-permission.png)

>[!NOTE]
>
>此 **[!UICONTROL 包含的許可權專案]** 清單僅顯示目前所選類別的新增許可權。

若要移除許可權，請選取 **X** 圖示加以存取，或選取 **[!UICONTROL 全部移除]** 以移除目前類別下的所有許可權。 移除的許可權會重新出現在下方 **[!UICONTROL 可用的許可權專案]**.

繼續瀏覽可用類別並新增任何所需許可權。 完成後，選取 **[!UICONTROL 儲存]**.

![remove-permisson](../images/remove-permission.png)

此 **[!UICONTROL 許可權]** 產品設定檔的索引標籤會重新出現，並顯示選取的許可權現在已啟用。

![許可權已更新](../images/permissions-updated.png)

## 後續步驟

建立許可權後，您可以繼續下一步以 [管理產品設定檔的詳細資料和服務](details-and-services.md)
