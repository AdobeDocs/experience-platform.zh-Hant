---
keywords: Experience Platform；首頁；熱門主題；Microsoft動態；microsoft動態；動態；動態
solution: Experience Platform
title: 在UI中建立MicrosoftDynamics源連接
type: Tutorial
description: 瞭解如何使用MicrosoftUI建立Adobe Experience PlatformDynamics源連接。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 建立 [!DNL Microsoft Dynamics] UI中的源連接

本教程提供建立 [!DNL Microsoft Dynamics] (以下簡稱：[!DNL Dynamics]&quot;)使用Adobe Experience PlatformUI的源連接。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL Dynamics] 帳戶，您可以跳過本文檔的其餘部分，繼續學習本教程。 [為CRM源配置資料流](../../dataflow/crm.md)。

### 收集所需憑據

| 憑據 | 說明 |
| ---------- | ----------- |
| `serviceUri` | 您的服務URL [!DNL Dynamics] 實例。 |
| `username` | 您的用戶名 [!DNL Dynamics] 用戶帳戶。 |
| `password` | 您的密碼 [!DNL Dynamics] 帳戶。 |
| `servicePrincipalId` | 您的客戶端ID [!DNL Dynamics] 帳戶。 使用服務主體和基於密鑰的身份驗證時需要此ID。 |
| `servicePrincipalKey` | 服務主密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |

有關入門的詳細資訊，請參閱 [這個 [!DNL Dynamics] 文檔](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 連接 [!DNL Dynamics] 帳戶

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Dynamics] 帳戶到平台。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL CRM]** 類別，選擇 **[!UICONTROL Microsoft動力]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 新建 [!DNL Dynamics] 連接器。

![目錄](../../../../images/tutorials/create/ms-dynamics/catalog.png)

的 **[!UICONTROL 連接到Dynamics]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，為新表單提供名稱和可選說明 [!DNL Dynamics] 帳戶。

的 [!DNL Dynamics] 連接器為訪問提供了不同的身份驗證類型。 下 [!UICONTROL 帳戶驗證] 選擇 **[!UICONTROL 基本身份驗證]** 使用基於密碼的憑據。

完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新賬戶留些時間。

![基本認證](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

或者，可以選擇 **[!UICONTROL 服務主體和密鑰身份驗證]** 連接 [!DNL Dynamics] 帳戶使用 [!UICONTROL 服務主體ID] 和 [!UICONTROL 服務主密鑰]。

>[!IMPORTANT]
>
> 中的基本身份驗證 [!DNL Dynamics] 可能會被雙因素身份驗證阻止，平台當前不支援此身份驗證。 在這種情況下，建議使用基於密鑰的身份驗證建立源連接器 [!DNL Dynamics]。

![基於密鑰的身份驗證](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| 憑據 | 說明 |
| ---------- | ----------- |
| [!UICONTROL 服務主體ID] | 您的客戶端ID [!DNL Dynamics] 帳戶。 使用服務主體和基於密鑰的身份驗證時需要此ID。 |
| [!UICONTROL 服務主密鑰] | 服務主密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL Dynamics] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 在右上角繼續。

![現有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 後續步驟

按照本教程，您已建立到 [!DNL Dynamics] 帳戶。 現在，您可以繼續下一個教程， [配置資料流以將資料引入平台](../../dataflow/crm.md)。
