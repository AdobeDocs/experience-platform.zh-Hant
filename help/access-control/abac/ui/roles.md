---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制建立角色
description: 透過Adobe Experience Cloud中的許可權介面管理角色。
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 13%

---

# 管理角色

<!-- UPDATE ROLES WITH A MORE COMPREHENSIVE EXPLANATION -->

若要開始管理角色，請導覽至&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中的](https://experience.adobe.com/){target="_blank"}，然後在左側面板中選取&#x200B;**[!UICONTROL Roles]**。

![許可權內的角色工作區。](../../images/ui/roles/roles-overview.png)

## 建立新角色 {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="建立新角色"
>abstract="建立新角色，改善與 Experience Platform 執行個體互動的使用者之分類方式。例如，您可以為內部行銷團隊建立角色並對該角色套用受監管的健康資料 (RHD) 標籤，讓您的內部行銷團隊可存取受保護的健康資訊 (PHI)。或者，您也可以為外部機構建立角色，而且該角色不會套用 RHD 標籤，藉此拒絕該角色存取 PHI 資料。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=zh-Hant" text="管理角色"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="將標籤套用至角色"

若要建立新角色，請選取&#x200B;**[!UICONTROL Create role]**。

>[!TIP]
>
>唯讀角色是現成可用的角色。 唯讀角色是一種角色，可授予使用者檢視資料、設定和UI功能的能力，而無需變更系統狀態。 管理員無法編輯這些角色，但可以將使用者與角色建立關聯。

![具有[建立角色]選項之角色的工作區已反白顯示。](../../images/ui/roles/roles-create-role.png)

**[!UICONTROL Create new role]**&#x200B;對話方塊隨即顯示。 輸入角色的&#x200B;**[!UICONTROL Name]**，並選擇性地輸入&#x200B;**[!UICONTROL Description]**，然後選取&#x200B;**[!UICONTROL Confirm]**。

![已填入「名稱」和「說明」且「確認」選項反白顯示的「建立新角色」對話方塊。](../../images/ui/roles/roles-create-new-role.png)

**[!UICONTROL Resources]**&#x200B;工作區會出現。 透過捲動或在左側面板的搜尋列中輸入資源名稱來尋找所需的資源。 選取資源名稱旁的![加號圖示](/help/images/icons/plus.png)，以新增資源。

![以個別資源的[新增]選項反白的[資源]工作區。](../../images/ui/roles/roles-resources.png)

<!-- ADD IN NOTE ABOUT THE DEFAULT SANDBOX - THIS SHOULD BE MENTIONED IN THE HIGHER LEVEL DOCS, WE MAY BE ABLE TO LINK TO IT -->

資源會新增至主要工作區。 選取資源名稱旁邊的下拉式清單，然後選取您要新增至角色的許可權。 您可以個別選擇許可權、選取&#x200B;**[!UICONTROL Add all]**，或透過在搜尋列中輸入許可權名稱來尋找特定許可權。

![已展開並反白顯示個別資源下拉式功能表的「資源」工作區。](../../images/ui/roles/roles-resources-permissions.png)

繼續選取您要新增至角色的所有資源和許可權。 完成後，選取「**[!UICONTROL Save]**」。

![反白顯示[儲存]選項的資源工作區。](../../images/ui/roles/roles-resources-permissions-save.png)

您將會收到警報，指出已成功儲存角色。 選取&#x200B;**[!UICONTROL Close]**&#x200B;以返回&#x200B;**[!UICONTROL Roles]**&#x200B;工作區。

![含有成功警示和[關閉]選項的[資源]工作區已反白顯示。](../../images/ui/roles/roles-resources-permissions-close.png)

新角色已成功建立，您被重新導向至&#x200B;**[!UICONTROL Roles]**&#x200B;頁面，您將看到新建立的角色出現在清單中。

<!-- The following video is intended to support your understanding of creating a new role and managing users for that role.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on) -->

## 複製角色

複製角色將會複製詳細資訊、許可權、標籤和沙箱。 使用者、使用者群組和API認證&#x200B;**不會**&#x200B;複製，必須手動新增至角色。

若要複製現有角色，請在&#x200B;**[!UICONTROL Roles]**&#x200B;索引標籤中尋找您要複製的角色。 選取角色名稱旁的![其他圖示](/help/images/icons/more.png)，然後從下拉式功能表中選取&#x200B;**[!UICONTROL Duplicate]**。

![角色的工作區已展開角色的下拉式功能表，並反白顯示[重複]選項。](../../images/ui/roles/role-duplicate.png)

將會顯示複製確認對話方塊。 選取&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成角色的複製。 新角色將以相同的名稱儲存，並新增`_Copy`作為尾碼。

![反白顯示[確認]選項的重複確認對話方塊。](../../images/ui/roles/role-duplicate-confirm.png)

或者，您可以從個別角色的工作區中複製角色。 選取您要從&#x200B;**[!UICONTROL Roles]**&#x200B;工作區複製的角色，然後選取&#x200B;**[!UICONTROL Duplicate]**。

![個別角色的工作區中，反白顯示[重複]選項。](../../images/ui/roles/role-duplicate-alt.png)

將會顯示複製確認對話方塊。 選取&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成角色的複製。 系統會將您重新導向新角色。

![反白顯示[確認]選項的重複確認對話方塊。](../../images/ui/roles/role-duplicate-alt-confirm.png)

## 刪除角色

若要刪除角色，請在&#x200B;**[!UICONTROL Roles]**&#x200B;索引標籤內尋找您要刪除的角色。 選取角色名稱旁的![其他圖示](/help/images/icons/more.png)，然後從下拉式功能表中選取&#x200B;**[!UICONTROL Delete]**。

![角色的工作區已展開角色的下拉式功能表，並反白顯示[重複]選項。](../../images/ui/roles/role-delete.png)

將會顯示刪除確認對話方塊。 選取&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成刪除角色。

![反白顯示[確認]選項的重複確認對話方塊。](../../images/ui/roles/role-duplicate-confirm.png)

或者，您可以從個別角色的工作區中刪除角色。 選取您要從&#x200B;**[!UICONTROL Roles]**&#x200B;工作區刪除的角色，然後選取&#x200B;**[!UICONTROL Delete]**。

![個別角色的工作區，其刪除選項已反白顯示。](../../images/ui/roles/role-delete-alt.png)

將會顯示刪除確認對話方塊。 選取&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成刪除角色。

![刪除確認對話方塊中反白顯示[確認]選項。](../../images/ui/roles/role-delete-alt-confirm.png)

<!-- ADD PERMISSIONS TO THIS PAGE -->

## 後續步驟

建立新角色後，您可以繼續下一步以[管理角色](permissions.md)的許可權。
