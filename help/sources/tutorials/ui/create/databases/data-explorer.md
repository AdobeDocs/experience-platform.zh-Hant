---
keywords: Experience Platform；首頁；熱門主題；AzureData Explorer;azure資料總管；資料總管；Data Explorer
solution: Experience Platform
title: 在UI中建立AzureData Explorer源連接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立AzureData Explorer來源連線。
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# 建立 [!DNL Azure Data Explorer] UI中的源連接

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供建立 [!DNL Azure Data Explorer] (下稱「[!DNL Data Explorer]&quot;)源連接器，使用 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL Data Explorer] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/databases.md).

### 收集所需憑據

若要存取 [!DNL Data Explorer] 帳戶 [!DNL Platform]，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `endpoint` | 的端點 [!DNL Data Explorer] 伺服器。 |
| `database` | 的名稱 [!DNL Data Explorer] 資料庫。 |
| `tenant` | 用來連線至的不重複租用戶ID [!DNL Data Explorer] 資料庫。 |
| `servicePrincipalId` | 用於連接到的唯一服務主體ID [!DNL Data Explorer] 資料庫。 |
| `servicePrincipalKey` | 用於連接到的唯一服務主體密鑰 [!DNL Data Explorer] 資料庫。 |

如需快速入門的詳細資訊，請參閱 [此 [!DNL Data Explorer] 檔案](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## 連接您的 [!DNL Azure Data Explorer] 帳戶

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Data Explorer] 帳戶 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL AzureData Explorer]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 來建立新Data Explorer連接器。

![目錄](../../../../images/tutorials/create/data-explorer/catalog.png)

此 **[!UICONTROL 連接到AzureData Explorer]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的 [!DNL Data Explorer] 憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Data Explorer] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/data-explorer/existing.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL Data Explorer] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).
