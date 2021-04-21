---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage；行銷人員；行銷人員
solution: Experience Platform
title: 驗證您的Marketo源介面
topic-legacy: overview
description: 本檔案提供如何產生您的Marketo驗證認證的資訊。
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---


# （測試版）驗證[!DNL Marketo Engage]源介面

>[!IMPORTANT]
>
>[!DNL Marketo Engage]來源目前處於測試階段。 其功能和說明檔案可能會有所變更。

您必須先透過[!DNL Marketo]介面設定自訂服務，並擷取Munchkin ID、用戶端ID和用戶端機密的值，才能建立[!DNL Marketo Engage]（以下稱為&quot;[!DNL Marketo]&quot;）來源連接器。

以下文檔提供了如何獲取身份驗證憑據以建立[!DNL Marketo]源連接器的步驟。

## 設定新角色

取得驗證憑證的第一步是透過[[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1)介面設定新角色。

登入[!DNL Marketo]並從頂端導覽列選擇&#x200B;**[!DNL Admin]**。

![管理新角色](../images/marketo/home.png)

*[!DNL Users & Role]s*&#x200B;頁面包含有關使用者、角色和登入記錄的資訊。 要建立新角色，請從頂部標題中選擇&#x200B;**[!DNL Roles]**，然後選擇&#x200B;**[!DNL New Role]**。

![新角色](../images/marketo/new-role.png)

出現&#x200B;**[!DNL Create New Role]**&#x200B;對話框。 提供名稱和說明，然後選擇要授予此角色的權限。 權限僅限於特定工作區，而使用者只能在其擁有權限的工作區中執行動作。

選擇要授予的權限後，請選擇&#x200B;**[!DNL Create]**。

![create-new-role](../images/marketo/create-new-role.png)

使用[!DNL Marketo]建立角色時，您可以管理API的受限權限。 您不必選取「存取API」，而是可以透過選取下列權限，提供具有最低存取等級的角色：

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## 設定新使用者

與角色類似，您可以從&#x200B;**[!DNL Users & Roles]**&#x200B;頁面設定新用戶。 **[!DNL Users]**&#x200B;頁面提供目前在Marketo布建的作用中使用者清單。 選擇&#x200B;**[!DNL Invite New User]**&#x200B;以設定新用戶。

![invite-new-user](../images/marketo/invite-new-user.png)

出現快顯對話框菜單。 提供適合您電子郵件的資訊、名字、姓氏和原因。 在此步驟中，您也可以建立您邀請之新使用者帳戶之存取權的到期日。 完成後，選擇&#x200B;**[!DNL Next]**。

>[!IMPORTANT]
>
>設定新使用者時，您必須將存取權指派給嚴格專屬於您所建立之自訂服務的使用者。

![user-info](../images/marketo/new-user-info.png)

在&#x200B;**[!DNL Permissions]**&#x200B;步驟中選擇適當的欄位，然後選擇&#x200B;**[!DNL API Only]**&#x200B;複選框以向新用戶提供API角色。 選擇&#x200B;**[!DNL Next]**&#x200B;繼續。

![權限](../images/marketo/permissions.png)

要完成該過程，請選擇&#x200B;**[!DNL Send]**。

![消息](../images/marketo/message.png)

## 設定自訂服務

建立新用戶後，您可以設定自訂服務來擷取新的認證。 從管理頁面中，選擇&#x200B;**[!DNL LaunchPoint]**。

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

**[!DNL Installed services]**&#x200B;頁包含現有服務的清單，要建立新的自定義服務，請選擇&#x200B;**[!DNL New]**，然後選擇&#x200B;**[!DNL New Service]**。

![新服務](../images/marketo/new-service.png)

為新服務提供描述性顯示名稱，然後從&#x200B;**[!DNL Service]**&#x200B;下拉式選單中選擇&#x200B;**[!DNL Custom]**。 提供適當的說明，然後從&#x200B;**[!DNL API Only User]**&#x200B;下拉式選單中選取您要布建的使用者。 填妥必要的詳細資料後，請選取&#x200B;**[!DNL Create]**&#x200B;以建立新的自訂服務。

![creat](../images/marketo/create.png)

## 取得您的用戶端ID和用戶端密碼

建立新的自訂服務後，您現在可以擷取用戶端ID和用戶端密碼的值。 從&#x200B;**[!DNL Installed Services]**&#x200B;菜單中，找到要訪問的自定義服務，然後選擇&#x200B;**[!DNL View Details]**。

![view-details](../images/marketo/view-details.png)

隨即出現對話方塊，其中包含您的用戶端ID和用戶端密碼。

![憑證](../images/marketo/credentials.png)

## 取得您的Munchkin ID

要驗證[!DNL Marketo]源連接器，您必須完成的最後一個步驟是檢索Munchkin ID。 從管理頁面中，選擇&#x200B;**[!DNL Integration]**&#x200B;面板下的&#x200B;**[!DNL Munchkin]**。

![admin-munchkin](../images/marketo/admin-munchkin.png)

此時會出現&#x200B;*[!DNL Munchkin]*&#x200B;頁面，而您的唯一Munchkin ID會列在面板的頂端。

![蒙奇金伊德](../images/marketo/munchkin-id.png)

結合您的用戶端ID和用戶端密碼，您可以使用Munchkin ID來設定新帳戶，並在Experience Platform上建立新的 [!DNL Marketo] 來源連線](../../../tutorials/ui/create/adobe-applications/marketo.md)。[
