---
keywords: Experience Platform；使用手冊；客戶AI；熱門主題；存取控制；建立模型；
solution: Experience Platform
feature: Customer AI
title: Customer AI的存取控制
description: 本檔案提供Customer AI基於屬性的存取控制資訊。
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# 以屬性為基礎的存取控制

>[!IMPORTANT]
>
>基於屬性的訪問控制當前僅在有限版本中可用。

[基於屬性的訪問控制](../../../access-control/abac/overview.md) 是Adobe Experience Platform的功能，可讓管理員根據屬性控制對特定物件和/或功能的存取。 屬性可以是新增至物件的中繼資料，例如新增至架構欄位或區段的標籤。 管理員定義了包括屬性的訪問策略以管理用戶訪問權限。

此功能可讓您以標籤來標示Experience Data Model(XDM)結構欄位，並定義組織或資料使用範圍。 同時，管理員可使用使用者和角色管理介面來定義XDM架構欄位的存取原則，並更妥善地管理指派給使用者或使用者群組（內部、外部或第三方使用者）的存取權。 此外，基於屬性的訪問控制允許管理員管理對特定段的訪問。

透過基於屬性的存取控制，貴組織的管理員可以控制使用者對所有平台工作流程和資源的敏感個人資料(SPD)和個人識別資訊(PII)的存取權。 管理員可以定義只有特定欄位和與這些欄位對應的資料存取權的使用者角色。

由於基於屬性的訪問控制，某些欄位和功能將具有訪問限制，並且對某些Customer AI服務模型不可用。 例如「身分」、「分數定義」和「原地複製」。

![Customer AI工作區，其中反白顯示服務模型結果的限制欄位。](../images/user-guide/unavailable-functionalities.png)

在Customer AI工作區頂端 **前瞻分析頁面**，請注意側邊欄、分數定義、身分和設定檔屬性中的詳細資料都顯示為「存取受限」。

![Customer AI工作區，會醒目顯示結構的限制欄位。](../images/user-guide/access-restricted.png)

在 **[!UICONTROL 建立模型工作流程]** 頁面，警告會通知您 [!UICONTROL 由於存取限制，資料集預覽中不會顯示某些資訊。]

![Customer AI工作區，預覽資料集的限制欄位會反白顯示限制結構結果。](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

建立具有受限資訊的模型後，請繼續 **[!UICONTROL 定義目標]** 步驟中，頂端會顯示警告： [!UICONTROL 由於存取限制，設定中未顯示特定資訊。]

![Customer AI工作區，其中反白顯示服務模型結果的限制欄位。](../images/user-guide/information-not-displayed-save-and-exit.png)

使用存取控制時， **檢視Customer AI** 和 **管理Customer AI** 權限可授予Customer AI不同功能的存取權。 此 **管理Customer AI** 權限可讓您 **建立**,**更新**, **刪除**, **啟用**，或 **disable** 模型 **檢視Customer AI** 可讓您閱讀或檢視。 此 **建立**, **更新** 和 **刪除** 動作會由稽核記錄檔記錄。

請參閱檔案以了解 [為訪問控制分配權限](../../../access-control/home.md) 或方法 [使用審核日誌來監視訪問和活動](../../../landing/governance-privacy-security/audit-logs/overview.md).

## 後續步驟

閱讀本指南後，您便了解了 [!DNL Experience Platform]. 您現在可以繼續 [存取控制使用手冊](../overview.md) 以取得如何使用的詳細步驟 [!DNL Admin Console] 若要建立產品設定檔並指派權限 [!DNL Platform].