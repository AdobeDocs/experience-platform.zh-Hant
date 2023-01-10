---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: 驗證您的Marketo來源連接器
description: 本檔案提供如何產生Marketo驗證憑證的相關資訊。
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# 驗證您的 [!DNL Marketo Engage] 來源連接器

建立 [!DNL Marketo Engage] (下稱「[!DNL Marketo]&quot;)來源連接器，您必須先透過 [!DNL Marketo] 介面，以及擷取Munchkin ID、用戶端ID和用戶端密碼的值。

以下檔案提供如何取得驗證憑證以建立 [!DNL Marketo] 源連接器。

## 設定新角色

取得驗證憑證的第一步，是透過 [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) 介面。

登入 [!DNL Marketo] 選取 **[!DNL Admin]** 的上界。

![新角色的管理員](../images/marketo/home.png)

此 *[!DNL Users & Role]s* 頁面包含使用者、角色和登入記錄的相關資訊。 要建立新角色，請選擇 **[!DNL Roles]** 從頂端標題中，然後選取 **[!DNL New Role]**.

![新角色](../images/marketo/new-role.png)

隨即顯示「**[!DNL Create New Role]**」對話框。提供名稱和說明，然後選取您要為此角色授予的權限。 權限受限於特定工作區，而使用者只能在他們擁有權限的工作區中執行動作。

選取您要授予的權限後，請選取 **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

使用建立角色時，您可以管理API的限制權限 [!DNL Marketo]. 您不必選取「存取API」，而是可以透過選取下列權限，以最低的存取層級提供角色：

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

與角色類似，您可以透過 **[!DNL Users & Roles]** 頁面。 此 **[!DNL Users]** 頁面提供目前布建在Marketo中的作用中使用者清單。 選擇 **[!DNL Invite New User]** 來布建新用戶。

![invite-new-user](../images/marketo/invite-new-user.png)

彈出視窗對話方塊功能表隨即顯示。 提供您電子郵件的適當資訊、名字、姓氏和原因。 在此步驟中，您也可以為您所邀請的新使用者帳戶的存取權限建立到期日。 完成後，請選取 **[!DNL Next]**.

>[!IMPORTANT]
>
>設定新使用者時，您必須指派存取權給嚴格專屬於您所建立之自訂服務的使用者。

![user-info](../images/marketo/new-user-info.png)

在 **[!DNL Permissions]** 步驟，然後選取 **[!DNL API Only]** 核取方塊，為新使用者提供API角色。 選擇 **[!DNL Next]** 繼續。

![權限](../images/marketo/permissions.png)

要完成該過程，請選擇 **[!DNL Send]**.

![訊息](../images/marketo/message.png)

## 設定自訂服務

建立新使用者後，您可以設定自訂服務以擷取新憑證。 從管理頁面中，選取 **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

此 **[!DNL Installed services]** 頁面包含現有服務的清單，若要建立新的自訂服務，請選取 **[!DNL New]** 然後選取 **[!DNL New Service]**.

![新服務](../images/marketo/new-service.png)

為新服務提供描述性顯示名稱，然後選取 **[!DNL Custom]** 從 **[!DNL Service]** 下拉式功能表。 提供適當的說明，然後從中選取您要布建的使用者 **[!DNL API Only User]** 下拉式功能表。 填寫必要的詳細資訊後，請選取 **[!DNL Create]** 來建立新的自訂服務。

![建立](../images/marketo/create.png)

## 取得用戶端ID和用戶端密碼

建立新的自訂服務後，您現在可以擷取用戶端ID和用戶端密碼的值。 從 **[!DNL Installed Services]** 功能表，找到您要存取的自訂服務，然後選取 **[!DNL View Details]**.

![檢視詳細資訊](../images/marketo/view-details.png)

隨即出現對話方塊，其中包含您的用戶端ID和用戶端密碼。

![憑據](../images/marketo/credentials.png)

## 取得您的Munchkin ID

您必須完成最後的步驟，才能驗證您的 [!DNL Marketo] 來源連接器是要擷取您的Munchkin ID。 從管理頁面中，選取 **[!DNL Munchkin]** 在 **[!DNL Integration]** 中。

![admin-munchkin](../images/marketo/admin-munchkin.png)

此 *[!DNL Munchkin]* 頁面，而面板頂端會列出您的唯一Munchkin ID。

![蒙奇金 — 伊德](../images/marketo/munchkin-id.png)

結合用戶端ID和用戶端密碼，您可以使用Munchkin ID來設定新帳戶，並 [建立新 [!DNL Marketo] 源連接](../../../tutorials/ui/create/adobe-applications/marketo.md) Experience Platform。
