---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制瀏覽
description: 本檔案提供在Adobe Experience Platform中使用許可權介面的相關資訊
exl-id: 39634bde-8858-44a6-b39a-776846654fc1
source-git-commit: 73d9c81aa80d82525bd04904ba5de83fb57dbeb3
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 2%

---

# 許可權指南

[!UICONTROL 許可權] 是Adobe Experience Platform的區域，管理員可在此定義使用者角色和存取原則，以管理產品應用程式內功能和物件的存取許可權。

替換為 [!UICONTROL 許可權]，您可以設定：

* [存取原則](./policies.md)
* [標記](./labels.md)
* [權限](./permissions.md)
* [角色](./roles.md)
* [沙箱](./sandboxes.md)
* [使用者](./users.md)

為了存取屬性型存取控制許可權 [!DNL Adobe Experience Platform]，您必須是貴組織的管理員，該組織訂閱了 [!DNL Adobe Experience Platform]. 雖然Adobe支援組織有彈性的管理員階層，但您必須是產品的管理員 [!DNL Adobe Experience Platform] 以設定許可權。 請參閱Adobe Help Center文章，位置在： [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 以取得詳細資訊。

如果您沒有管理員許可權，請聯絡您的系統管理員以獲得存取權。

取得管理員許可權後，請前往 [Adobe Experience Platform](https://experience.adobe.com/) 並使用您的 [!DNL Adobe] 認證。 登入後， **[!UICONTROL 概觀]** 此時會出現您擁有管理員許可權之組織的頁面。 此頁面顯示貴組織訂閱的產品，以及其他可將使用者和管理員新增至整個組織的控制項。 選取 **[!UICONTROL 許可權]** 以開啟您Platform整合的屬性型存取控制工作區。

![flac-select-product](../../images/flac-ui/flac-select-product.png)

Platform的屬性型存取控制工作區隨即出現，並開啟於 **[!UICONTROL 角色]** 頁面。 此頁面可讓您檢視所有角色並管理本檔案中概述的各種設定。

>[!IMPORTANT]
>
>若要管理組織中使用者、功能、標籤和其他資源的許可權，您現在應該對以下專案使用許可權： [!DNL Adobe Experience Platform] 而非中的角色 [!DNL Adobe Admin Console].

您現在應該使用許可權於 [!DNL Adobe Experience Platform]，而非Adobe Admin Console中的角色，來管理組織中使用者、功能、標籤和其他資源的許可權。

![flac-select-roles](../../images/flac-ui/flac-select-roles.png)

本使用手冊著重於如何使用 [!DNL Adobe Experience Platform] 以指派Platform的存取許可權。 如需如何導覽的詳細一般資訊，請參閱 [!DNL Admin Console]，請參閱 [Admin Console使用手冊](https://helpx.adobe.com/tw/enterprise/using/admin-console.html).

## 後續步驟

導覽許可權工作區後，請繼續前往的下一個步驟 [建立新角色](roles.md).
