---
keywords: Experience Platform；首頁；熱門主題；存取控制；adobe admin console
solution: Experience Platform
feature: Attribution AI
title: 對Attribution AI的訪問控制
description: 本文檔提供有關基於屬性的Attribution AI訪問控制的資訊。
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# 存取控制

Attribution AI的存取控制可透過Adobe Experience Platform提供，位於 [Adobe Admin Console](https://adminconsole.adobe.com/). 此功能會運用Admin Console中的產品設定檔，將使用者與權限和沙箱連結。

有關訪問控制的詳細資訊，請參見 [存取控制概觀](../../access-control/home).

## 以屬性為基礎的存取控制

>[!IMPORTANT]
>
>基於屬性的訪問控制當前僅在有限版本中可用。

[基於屬性的訪問控制](../../../help/access-control/abac/overview.md) 是Adobe Experience Platform的功能，可讓管理員根據屬性控制對特定物件和/或功能的存取。 屬性可以是新增至物件的中繼資料，例如新增至架構欄位或區段的標籤。 管理員定義了包括屬性的訪問策略以管理用戶訪問權限。

此功能可讓您以標籤來標示Experience Data Model(XDM)結構欄位，並定義組織或資料使用範圍。 同時，管理員可使用使用者和角色管理介面來定義XDM架構欄位的存取原則，並更妥善地管理指派給使用者或使用者群組（內部、外部或第三方使用者）的存取權。 此外，基於屬性的訪問控制允許管理員管理對特定段的訪問。

透過基於屬性的存取控制，管理員可以控制使用者對所有平台工作流程和資源的敏感個人資料(SPD)和個人識別資訊(PII)的存取權。 管理員可以定義只能存取特定欄位和與這些欄位對應的資料的使用者角色。

由於基於屬性的訪問控制，某些欄位和功能可能存取受限，並且對某些Attribution AI服務模型不可用。 例如「身分」、「分數定義」和「原地複製」。

在Attribution AI工作區頂端 **前瞻分析頁面**，側邊欄中顯示的詳細資料會限制存取。

![Attribution AI工作區，其中會強調顯示限制結構欄位。](./images/user-guide/access-restricted.png)

如果您在 **[!UICONTROL 建立模型工作流程]** 頁面上，資料集名稱旁會出現警告符號，並顯示訊息： [!UICONTROL 已排除受限資訊].

![Attribution AI工作區中，已反白顯示限制資料集欄位。](./images/user-guide/restricted-info-excluded.png)

在 **[!UICONTROL 建立模型工作流程]** 頁面，警告會通知您 [!UICONTROL 由於存取限制，資料集預覽中不會顯示某些資訊。]

![Attribution AI工作區，其結果為醒目顯示受限預覽結構欄位。](./images/user-guide/restricted-dataset-preview.png)

建立具有受限資訊的模型後，請繼續 **[!UICONTROL 定義目標]** 步驟中，頂端會顯示警告： [!UICONTROL 由於存取限制，設定中未顯示特定資訊。]

![Attribution AI工作區，其中模型結果的限制欄位突出顯示。](./images/user-guide/information-not-displayed-save-and-exit.png)

## 後續步驟

閱讀本指南後，您便了解了 [!DNL Experience Platform]. 您現在可以繼續 [存取控制使用手冊](./ui/overview.md) 以取得如何使用的詳細步驟 [!DNL Admin Console] 若要建立產品設定檔並指派權限 [!DNL Platform].
