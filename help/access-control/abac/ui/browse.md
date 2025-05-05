---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制瀏覽
description: 本檔案提供在Adobe Experience Platform中使用許可權介面的相關資訊
exl-id: 39634bde-8858-44a6-b39a-776846654fc1
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 2%

---

# 許可權指南

[!UICONTROL 許可權]是Adobe Experience Platform的區域，管理員可在此定義使用者角色和存取原則，以管理產品應用程式內功能和物件的存取許可權。

透過[!UICONTROL 許可權]，您可以設定：

* [存取原則](./policies.md)
* [標記](./labels.md)
* [權限](./permissions.md)
* [角色](./roles.md)
* [沙箱](./sandboxes.md)
* [使用者](./users.md)

若要存取[!DNL Adobe Experience Platform]的屬性型存取控制許可權，您必須是擁有[!DNL Adobe Experience Platform]訂閱的組織管理員。 雖然Adobe支援組織有彈性的管理員階層，但您必須是[!DNL Adobe Experience Platform]的產品管理員才能設定許可權。 如需詳細資訊，請參閱[管理角色](https://helpx.adobe.com/tw/enterprise/using/admin-roles.html)上的Adobe說明中心文章。

如果您沒有管理員許可權，請聯絡您的系統管理員以獲得存取權。

一旦您擁有管理員許可權，請移至[Adobe Experience Platform](https://experience.adobe.com/)並使用您的[!DNL Adobe]認證登入。 登入後，會針對您擁有管理員許可權的組織顯示&#x200B;**[!UICONTROL 總覽]**&#x200B;頁面。 此頁面顯示貴組織訂閱的產品，以及其他可將使用者和管理員新增至整個組織的控制項。 選取&#x200B;**[!UICONTROL 許可權]**&#x200B;以開啟Experience Platform整合的屬性式存取控制工作區。

![flac-select-product](../../images/flac-ui/flac-select-product.png)

Experience Platform的屬性型存取控制工作區隨即顯示，並在&#x200B;**[!UICONTROL 角色]**&#x200B;頁面上開啟。 此頁面可讓您檢視所有角色並管理本檔案中概述的各種設定。

>[!IMPORTANT]
>
>若要管理組織中使用者、功能、標籤和其他資源的許可權，您現在應該使用[!DNL Adobe Experience Platform]的許可權，而不是[!DNL Adobe Admin Console]中的角色。

您現在應該使用[!DNL Adobe Experience Platform]的許可權(而不是Adobe Admin Console中的角色)來管理組織中使用者、功能、標籤和其他資源的許可權。

![flac-select-roles](../../images/flac-ui/flac-select-roles.png)

本使用手冊著重於如何使用[!DNL Adobe Experience Platform]指派Experience Platform的存取許可權。 如需如何導覽[!DNL Admin Console]的一般資訊，請參閱[Admin Console使用手冊](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

## 後續步驟

瀏覽許可權工作區後，繼續下一步以[建立新角色](roles.md)。
