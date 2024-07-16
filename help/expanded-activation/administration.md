---
title: 擴充的啟用帳戶管理
description: 瞭解如何在您的Expanded Activation帳戶上執行管理工作，例如監控授權使用和指派正確的許可權。
exl-id: ee0ec4b9-a083-447b-b7a7-e1307e90c646
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 帳戶管理

若要從Audience Manager擷取受眾並將它們啟用至社交和廣告目的地，您必須先建立「展開啟用」使用者帳戶，並將帳戶指派給正確的許可權角色。

本頁說明如何在Admin Console中建立使用者帳戶，以及為「展開啟用」指派正確的許可權。

## 建立使用者帳戶 {#create-users}

您必須先建立使用者帳戶，才能使用[!DNL Audience Manager Expanded Activation]。

若要為[!DNL Expanded Activation]建立使用者帳戶，請依照[Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/manage-users-individually.html)檔案中管理使用者的指示操作。

## 將使用者新增至許可權角色 {#permissions}

建立使用者帳戶之後，您必須將其新增至[!DNL Expanded Activation]使用者介面中的[!DNL Expanded Activation]許可權角色。

移至&#x200B;**[!UICONTROL 管理]** -> **[!UICONTROL 許可權]** -> **[!UICONTROL 角色]**，然後選取&#x200B;**[!UICONTROL 展開啟用預設角色]**。

![展開的Activation使用者介面影像顯示[角色]頁面。](assets/expanded-activation-role.png)

移至&#x200B;**[!UICONTROL 使用者]**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 新增使用者]**。

![顯示[使用者]頁面的展開啟動使用者介面影像。](assets/add-users.png)

從可用清單中選取新建立的使用者，然後選取&#x200B;**[!UICONTROL 儲存]**。

![展開的啟動使用者介面影像顯示[新增使用者]頁面。](assets/add-user.png)

現在已建立使用者帳戶並指派給正確的角色。 它現在可以存取&#x200B;**[!UICONTROL 擴充啟用]**&#x200B;使用者介面。

## 監視授權使用情況 {#license-usage}

您的[!DNL Audience Manager Expanded Activation]合約指定您可以內嵌至帳戶的雜湊電子郵件數目上限。

您可以前往&#x200B;**[!UICONTROL 管理]** -> **[!UICONTROL 授權使用情況]**&#x200B;頁面找到此資訊。

![展開的Activation使用者介面影像顯示授權使用畫面。](assets/license-usage.png)

您可以在此頁面找到下列資訊：

* **[!UICONTROL Product]**：您已獲得授權的Adobe產品。 這將永遠是&#x200B;**[!UICONTROL Audience Manager展開啟用]**。
* **[!UICONTROL 主要量度]**：要追蹤使用的量度名稱。 此一律為&#x200B;**[!UICONTROL 可定址對象]**。
* **[!UICONTROL 授權數量]**：您獲授權可內嵌的雜湊電子郵件數目上限。

  >[!TIP]
  >
  >您透過[Audience Manager來源聯結器](../sources/connectors/adobe-applications/audience-manager.md)內嵌雜湊電子郵件。 如需詳細資訊，請參閱有關[如何啟用對象](activate-audiences.md)的檔案。

* **[!UICONTROL 使用狀況]**：您已內嵌的雜湊電子郵件數目。
* **[!UICONTROL 使用量%]**：您已使用的授權數量百分比。

若要進一步瞭解Experience Platform中的授權使用情況，請參閱[授權使用情況檔案](../dashboards/guides/license-usage.md)。

## 後續步驟 {#next-steps}

現在您已設定至少一個使用者帳戶具有擴充啟用的正確存取權，您可以開始使用該帳戶[啟用對象](activate-audiences.md)。
