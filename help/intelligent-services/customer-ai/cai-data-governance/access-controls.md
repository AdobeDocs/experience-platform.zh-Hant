---
keywords: Experience Platform；使用手冊；客戶；熱門主題；訪問控制；建立模型；
solution: Experience Platform
feature: Customer AI
title: 客戶AI的訪問控制
description: 本文檔提供有關客戶AI基於屬性的訪問控制的資訊。
exl-id: 02e3b6a4-304a-4ac4-b07c-010531101feb
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 以屬性為基礎的存取控制

>[!IMPORTANT]
>
>基於屬性的訪問控制目前僅在有限版本中可用。

[基於屬性的訪問控制](../../../access-control/abac/overview.md) 是Adobe Experience Platform的一種功能，使管理員能夠根據屬性控制對特定對象和/或權能的訪問。 屬性可以是添加到對象的元資料，如添加到架構欄位或段的標籤。 管理員定義包括屬性的訪問策略以管理用戶訪問權限。

此功能允許您用定義組織或資料使用範圍的標籤來標籤體驗資料模型(XDM)架構欄位。 同時，管理員可以使用用戶和角色管理介面來定義圍繞XDM架構欄位的訪問策略，並更好地管理授予用戶或用戶組（內部、外部或第三方用戶）的訪問。 此外，基於屬性的訪問控制允許管理員管理對特定段的訪問。

通過基於屬性的訪問控制，您組織的管理員可以控制用戶對所有平台工作流和資源中敏感個人資料(SPD)和個人識別資訊(PII)的訪問。 管理員可以定義只能訪問特定欄位和與這些欄位對應的資料的用戶角色。

由於基於屬性的訪問控制，某些欄位和功能將受限於某些客戶AI服務模型，並且不可用。 示例包括「Identity」、「Score Definition」和「Clone」。

![突出顯示服務模型結果的受限欄位的客戶AI工作區。](../images/user-guide/unavailable-functionalities.png)

在客戶AI工作區頂部 **insights頁**，請注意邊欄、分數定義、標識和配置檔案屬性中的詳細資訊都顯示「訪問受限」。

![突出顯示了模式的受限欄位的Customer AI工作區。](../images/user-guide/access-restricted.png)

在上預覽具有受限架構的資料集時 **[!UICONTROL 建立模型工作流]** 頁，警告會告訴您 [!UICONTROL 由於訪問限制，某些資訊不會顯示在資料集預覽中。]

![突出顯示了預覽資料集的受限欄位的客戶AI工作區，其中包含受限架構結果。](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

在建立具有受限資訊的模型後，繼續 **[!UICONTROL 定義目標]** 步驟，頂部將顯示警告： [!UICONTROL 由於訪問限制，配置中不顯示某些資訊。]

![突出顯示服務模型結果的受限欄位的客戶AI工作區。](../images/user-guide/information-not-displayed-save-and-exit.png)

使用訪問控制時， **查看客戶AI** 和 **管理客戶AI** 權限授予對客戶AI的不同功能的訪問權限。 的 **管理客戶AI** 權限允許 **建立**。**更新**。 **刪除**。 **啟用**&#x200B;或 **禁用** 模特 **查看客戶AI** 讓您閱讀或查看。 的 **建立**。 **更新** 和 **刪除** 操作由審核日誌記錄。

請參閱要瞭解的文檔 [分配訪問控制權限](../../../access-control/home.md) 或如何 [使用審核日誌來監視訪問和活動](../../../landing/governance-privacy-security/audit-logs/overview.md)。

## 後續步驟

通過閱讀本指南，您已介紹了 [!DNL Experience Platform]。 您現在可以繼續 [訪問控制使用手冊](../overview.md) 有關如何使用的詳細步驟 [!DNL Admin Console] 建立產品配置檔案並分配權限 [!DNL Platform]。
