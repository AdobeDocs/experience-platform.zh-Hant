---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: 驗證您的Marketo來源連接器
topic-legacy: overview
description: 本檔案提供如何產生Marketo驗證憑證的相關資訊。
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 50e92ac8c1eccc9ccfb6b078ad8b996817a6d693
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# 驗證[!DNL Marketo Engage]源連接器

在建立[!DNL Marketo Engage]（下稱為「[!DNL Marketo]」）源連接器之前，您必須先通過[!DNL Marketo]介面設定自定義服務，並檢索Munchkin ID、客戶端ID和客戶端密碼的值。

以下文檔提供了如何獲取身份驗證憑據以建立[!DNL Marketo]源連接器的步驟。

## 設定新角色

取得驗證憑證的第一步是透過[[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1)介面設定新角色。

登入[!DNL Marketo]，然後從頂端導覽列選取&#x200B;**[!DNL Admin]**。

![新角色的管理員](../images/marketo/home.png)

*[!DNL Users & Role]s*&#x200B;頁面包含有關使用者、角色和登入記錄的資訊。 要建立新角色，請從頂部標題中選擇&#x200B;**[!DNL Roles]**，然後選擇&#x200B;**[!DNL New Role]**。

![新角色](../images/marketo/new-role.png)

隨即顯示「**[!DNL Create New Role]**」對話框。提供名稱和說明，然後選取您要為此角色授予的權限。 權限受限於特定工作區，而使用者只能在他們擁有權限的工作區中執行動作。

選擇要授予的權限後，選擇&#x200B;**[!DNL Create]**。

![create-new-role](../images/marketo/create-new-role.png)

使用[!DNL Marketo]建立角色時，您可以管理API上的限制權限。 您不必選取「存取API」，而是可以透過選取下列權限，以最低的存取層級提供角色：

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

與角色類似，您可以從&#x200B;**[!DNL Users & Roles]**&#x200B;頁面設定新使用者。 **[!DNL Users]**&#x200B;頁面提供目前布建於Marketo中的作用中使用者清單。 選擇&#x200B;**[!DNL Invite New User]**&#x200B;以布建新用戶。

![invite-new-user](../images/marketo/invite-new-user.png)

彈出視窗對話方塊功能表隨即顯示。 提供您電子郵件的適當資訊、名字、姓氏和原因。 在此步驟中，您也可以為您所邀請的新使用者帳戶的存取權限建立到期日。 完成後，選擇&#x200B;**[!DNL Next]**。

>[!IMPORTANT]
>
>設定新使用者時，您必須指派存取權給嚴格專屬於您所建立之自訂服務的使用者。

![user-info](../images/marketo/new-user-info.png)

在&#x200B;**[!DNL Permissions]**&#x200B;步驟中選取適當欄位，然後選取&#x200B;**[!DNL API Only]**&#x200B;核取方塊，為新使用者提供API角色。 選擇&#x200B;**[!DNL Next]**&#x200B;以繼續。

![權限](../images/marketo/permissions.png)

要完成該過程，請選擇&#x200B;**[!DNL Send]**。

![訊息](../images/marketo/message.png)

## 設定自訂服務

建立新使用者後，您可以設定自訂服務以擷取新憑證。 從管理頁面中，選擇&#x200B;**[!DNL LaunchPoint]**。

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

**[!DNL Installed services]**&#x200B;頁包含現有服務的清單，要建立新的自定義服務，請選擇&#x200B;**[!DNL New]**，然後選擇&#x200B;**[!DNL New Service]**。

![新服務](../images/marketo/new-service.png)

為新服務提供描述性顯示名稱，然後從&#x200B;**[!DNL Service]**&#x200B;下拉式選單中選取&#x200B;**[!DNL Custom]**。 提供適當的說明，然後從&#x200B;**[!DNL API Only User]**&#x200B;下拉式選單中選取您要布建的使用者。 填寫必要的詳細資訊後，請選擇&#x200B;**[!DNL Create]**&#x200B;以建立新的自定義服務。

![建立](../images/marketo/create.png)

## 取得用戶端ID和用戶端密碼

建立新的自訂服務後，您現在可以擷取用戶端ID和用戶端密碼的值。 從&#x200B;**[!DNL Installed Services]**&#x200B;功能表中，找出您要存取的自訂服務，然後選取&#x200B;**[!DNL View Details]**。

![檢視詳細資訊](../images/marketo/view-details.png)

隨即出現對話方塊，其中包含您的用戶端ID和用戶端密碼。

![憑據](../images/marketo/credentials.png)

## 取得您的Munchkin ID

要驗證[!DNL Marketo]源連接器，您必須完成的最後一步是檢索Munchkin ID。 從管理頁面，選擇&#x200B;**[!DNL Integration]**&#x200B;面板下的&#x200B;**[!DNL Munchkin]**。

![admin-munchkin](../images/marketo/admin-munchkin.png)

此時會出現&#x200B;*[!DNL Munchkin]*&#x200B;頁面，面板頂端會列出您的唯一Munchkin ID。

![蒙奇金 — 伊德](../images/marketo/munchkin-id.png)

結合您的用戶端ID和用戶端密碼，您可以使用Munchkin ID來設定新帳戶，並在Experience Platform上建立新的 [!DNL Marketo] 來源連線](../../../tutorials/ui/create/adobe-applications/marketo.md)。[
