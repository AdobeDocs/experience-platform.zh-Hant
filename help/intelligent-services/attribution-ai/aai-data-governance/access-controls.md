---
keywords: Experience Platform；首頁；熱門主題；訪問控制；adobe管理控制台
solution: Experience Platform
feature: Attribution AI
title: 用於Attribution AI的訪問控制
description: 本文檔提供有關基於屬性的Attribution AI訪問控制的資訊。
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 存取控制

Attribution AI的訪問控制通過Adobe Experience Platform提供。 [Adobe Admin Console](https://adminconsole.adobe.com/)。 此功能利用Admin Console中的產品配置檔案，將用戶與權限和沙箱連結起來。

有關訪問控制的詳細資訊，請參見 [訪問控制概述](../../../access-control/home.md)。

## 以屬性為基礎的存取控制

>[!IMPORTANT]
>
>基於屬性的訪問控制目前僅在有限版本中可用。

[基於屬性的訪問控制](../../../access-control/abac/overview.md) 是Adobe Experience Platform的一種功能，使管理員能夠根據屬性控制對特定對象和/或權能的訪問。 屬性可以是添加到對象的元資料，如添加到架構欄位或段的標籤。 管理員定義包括屬性的訪問策略以管理用戶訪問權限。

此功能允許您用定義組織或資料使用範圍的標籤來標籤體驗資料模型(XDM)架構欄位。 同時，管理員可以使用用戶和角色管理介面來定義圍繞XDM架構欄位的訪問策略，並更好地管理授予用戶或用戶組（內部、外部或第三方用戶）的訪問。 此外，基於屬性的訪問控制允許管理員管理對特定段的訪問。

通過基於屬性的訪問控制，管理員可以控制用戶對所有平台工作流和資源中敏感個人資料(SPD)和個人身份資訊(PII)的訪問。 管理員可以定義只能訪問特定欄位和與這些欄位對應的資料的用戶角色。

由於基於屬性的訪問控制，某些欄位和功能可能具有訪問限制，並且對某些Attribution AI服務模型不可用。 示例包括「Identity」、「Score Definition」和「Clone」。

在Attribution AI工作區頂部 **insights頁**，邊欄中顯示的詳細資訊具有限制訪問權限。

![Attribution AI工作區，其中突出顯示了受限架構欄位。](../images/user-guide/access-restricted.png)

如果您選擇的資料集上具有受限架構 **[!UICONTROL 建立模型工作流]** 頁，資料集名稱旁邊將顯示一個警告符號，消息為： [!UICONTROL 已排除受限資訊]。

![Attribution AI工作區，其中突出顯示了受限資料集欄位。](../images/user-guide/restricted-info-excluded.png)

在上預覽具有受限架構的資料集時 **[!UICONTROL 建立模型工作流]** 頁，警告會告訴您 [!UICONTROL 由於訪問限制，某些資訊不會顯示在資料集預覽中。]

![Attribution AI工作區，其中突出顯示了受限制的預覽架構欄位的結果。](../images/user-guide/restricted-dataset-preview.png)

在建立具有受限資訊的模型後，繼續 **[!UICONTROL 定義目標]** 步驟，頂部將顯示警告： [!UICONTROL 由於訪問限制，配置中不顯示某些資訊。]

![帶模型結果的受限欄位的Attribution AI工作區加亮顯示。](../images/user-guide/information-not-displayed-save-and-exit.png)

## 後續步驟

通過閱讀本指南，您已介紹了 [!DNL Experience Platform]。 您現在可以繼續 [訪問控制使用手冊](../overview.md) 有關如何使用的詳細步驟 [!DNL Admin Console] 建立產品配置檔案並分配權限 [!DNL Platform]。
