---
title: 擴充的啟用帳戶管理
description: 瞭解如何在您的Expanded Activation帳戶上執行管理工作，例如監控授權使用和指派正確的許可權。
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 帳戶管理

若要從Audience Manager擷取受眾並將它們啟用至社交和廣告目的地，您必須先建立「展開啟用」使用者帳戶，並將帳戶指派給正確的許可權角色。

本頁說明如何在Admin Console中建立使用者帳戶，以及為「展開啟用」指派正確的許可權。

## 建立使用者帳戶 {#create-users}

開始使用 [!DNL Audience Manager Expanded Activation]，您必須建立使用者帳戶。

建立使用者帳戶的方式 [!DNL Expanded Activation]，請依照管理使用者的指示，從 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/manage-users-individually.html) 檔案。

## 將使用者新增至許可權角色 {#permissions}

建立使用者帳戶後，您必須將其新增至 [!DNL Expanded Activation] 許可權角色，在 [!DNL Expanded Activation] 使用者介面。

前往 **[!UICONTROL 管理]** -> **[!UICONTROL 許可權]** -> **[!UICONTROL 角色]**，然後選取 **[!UICONTROL 展開的啟動預設角色]**.

![展開顯示「角色」頁面的啟用使用者介面影像。](assets/expanded-activation-role.png)

前往 **[!UICONTROL 使用者]** 標籤並選取 **[!UICONTROL 新增使用者]**.

![展開顯示「使用者」頁面的啟用使用者介面影像。](assets/add-users.png)

從可用清單中選取新建的使用者，然後選取 **[!UICONTROL 儲存]**.

![展開顯示「新增使用者」頁面的啟用使用者介面影像。](assets/add-user.png)

現在已建立使用者帳戶並指派給正確的角色。 現在已準備好存取 **[!UICONTROL 擴展啟用]** 使用者介面。

## 監視授權使用情況 {#license-usage}

您的 [!DNL Audience Manager Expanded Activation] 合約指定您可以內嵌至帳戶的雜湊電子郵件數上限。

您可以前往 **[!UICONTROL 管理]** -> **[!UICONTROL 授權使用情況]** 頁面。

![展開顯示授權使用畫面的「啟動」使用者介面影像。](assets/license-usage.png)

您可以在此頁面找到下列資訊：

* **[!UICONTROL 產品]**：您已獲得授權的Adobe產品。 永遠是 **[!UICONTROL Audience Manager展開啟用]**.
* **[!UICONTROL 主要量度]**：為使用情形而追蹤的量度名稱。 永遠是 **[!UICONTROL 可定址的受眾]**.
* **[!UICONTROL 授權金額]**：您獲授權可內嵌的雜湊電子郵件最大數量。

  >[!TIP]
  >
  >您透過擷取雜湊電子郵件 [Audience Manager來源聯結器](../sources/connectors/adobe-applications/audience-manager.md). 請參閱以下檔案： [如何啟用對象](activate-audiences.md) 以取得更多詳細資料。

* **[!UICONTROL 使用狀況]**：您已內嵌的雜湊電子郵件數。
* **[!UICONTROL 使用量%]**：您已使用的授權數量百分比。

若要進一步瞭解Experience Platform中的授權使用情況，請參閱 [授權使用檔案](../dashboards/guides/license-usage.md).

## 後續步驟 {#next-steps}

現在您已設定至少一個具有正確存取擴充啟用的使用者帳戶，您可以開始使用該帳戶 [啟用對象](activate-audiences.md).
