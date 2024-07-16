---
keywords: Experience Platform；首頁；熱門主題；存取控制；adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Attribution AI的存取控制
description: 本檔案提供Attribution AI的屬性型存取控制相關資訊。
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Attribution AI中的存取控制

透過[Adobe Admin Console](https://adminconsole.adobe.com/)中的Adobe Experience Platform提供Attribution AI的存取控制。 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。

如需存取控制的詳細資訊，請參閱[存取控制總覽](../../../access-control/home.md)。

## 屬性型存取控制

>[!IMPORTANT]
>
>以屬性為基礎的存取控制目前僅在有限版本中可用。

[以屬性為基礎的存取控制](../../../access-control/abac/overview.md)是Adobe Experience Platform的一項功能，可讓管理員根據屬性控制特定物件和/或功能的存取。 屬性可以是新增至物件的中繼資料，例如新增至結構欄位或區段的標籤。 管理員定義存取原則，其中包含管理使用者存取許可權的屬性。

此功能可讓您使用定義組織或資料使用範圍的標籤，來標籤Experience Data Model (XDM)結構描述欄位。 同時，管理員可以使用使用者和角色管理介面來定義有關XDM結構描述欄位的存取原則，並更好地管理使用者或使用者群組（內部、外部或第三方使用者）的存取許可權。 此外，屬性型存取控制可讓管理員管理特定區段的存取權。

透過屬性型存取控制，管理員可控制使用者對所有Platform工作流程與資源的敏感個人資料(SPD)和個人識別資訊(PII)的存取權。 管理員可以定義僅能存取特定欄位以及對應至這些欄位之資料的使用者角色。

由於基於屬性的存取控制，某些欄位和功能可能會限制存取，並且無法用於某些Attribution AI服務模型。 範例包括「身分」、「評分定義」和「原地複製」。

在Attribution AI工作區&#x200B;**深入分析頁面**&#x200B;頂端，側邊欄中顯示的詳細資訊具有受限制的存取權。

![反白顯示限制結構描述欄位的Attribution AI工作區。](../images/user-guide/access-restricted.png)

如果您在&#x200B;**[!UICONTROL 建立模型工作流程]**&#x200B;頁面上選取包含受限制結構描述的資料集，資料集名稱旁會顯示警告符號，訊息為： [!UICONTROL 已排除受限制的資訊]。

![已反白限制資料集欄位的Attribution AI工作區。](../images/user-guide/restricted-info-excluded.png)

當您在&#x200B;**[!UICONTROL 建立模型工作流程]**&#x200B;頁面上預覽包含受限制結構描述的資料集時，會出現警告以通知您[!UICONTROL 由於存取限制，某些資訊不會顯示在資料集預覽中。]

![含有已限制預覽結構描述欄位結果的Attribution AI工作區反白顯示。](../images/user-guide/restricted-dataset-preview.png)

當您使用受限制的資訊建立模型並繼續&#x200B;**[!UICONTROL 定義目標]**&#x200B;步驟後，會在頂端顯示警告： [!UICONTROL 由於存取限制，某些資訊不會顯示在設定中。]

![模型結果限制欄位反白顯示的Attribution AI工作區。](../images/user-guide/information-not-displayed-save-and-exit.png)

## 後續步驟

閱讀本指南後，您已經瞭解[!DNL Experience Platform]中存取控制的主要原則。 您現在可以繼續參閱[存取控制使用手冊](../overview.md)，以取得有關如何使用[!DNL Admin Console]建立產品設定檔及為[!DNL Platform]指派許可權的詳細步驟。
