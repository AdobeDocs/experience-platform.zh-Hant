---
keywords: Experience Platform；首頁；熱門主題；Salesforce;Salesforce
solution: Experience Platform
title: 在UI中建立Salesforce來源連線
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Salesforce來源連線。
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# 建立 [!DNL Salesforce] UI中的源連接

Adobe Experience Platform中的來源連接器可讓您排程內嵌外部來源的CRM資料。 本教學課程提供建立 [!DNL Salesforce] 源連接器使用 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL Salesforce] 帳戶，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/crm.md).

### 收集所需憑據

| 憑據 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | 的URL [!DNL Salesforce] 源實例。 |
| `username` | 的使用者名稱 [!DNL Salesforce] 使用者帳戶。 |
| `password` | 的密碼 [!DNL Salesforce] 使用者帳戶。 |
| `securityToken` | 的安全令牌 [!DNL Salesforce] 使用者帳戶。 |

如需快速入門的詳細資訊，請參閱 [此Salesforce文檔](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

## 連接您的 [!DNL Salesforce] 帳戶

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Salesforce] 帳戶 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以為其建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL Salesforce]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 來建立新的Salesforce連接器。

![目錄](../../../../images/tutorials/create/salesforce/catalog.png)

此 **[!UICONTROL 連接到Salesforce]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的 [!DNL Salesforce] 憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![connect](../../../../images/tutorials/create/salesforce/new.png)

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Salesforce] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 來繼續。

![現有](../../../../images/tutorials/create/salesforce/existing.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL Salesforce] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/crm.md).
