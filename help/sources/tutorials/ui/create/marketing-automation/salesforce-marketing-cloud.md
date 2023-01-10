---
keywords: Experience Platform；首頁；熱門主題；salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: 在UI中建立SalesforceMarketing Cloud來源連線
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立SalesforceMarketing Cloud來源連線。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 建立 [!DNL Salesforce Marketing Cloud] UI中的源連接

>[!NOTE]
>
> 此 [!DNL Salesforce Marketing Cloud] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供建立 [!DNL Salesforce Marketing Cloud] 來源連接器。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有 [!DNL Salesforce Marketing Cloud] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/marketing-automation.md).

### 收集所需憑據

若要存取 [!DNL Salesforce Marketing Cloud] 帳戶，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 應用程式的主機伺服器。 這通常是您的子網域。 **注意：** 輸入 `host` 值時，您只需指定子網域，而非整個URL。 例如，若您的主機URL為 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則您只需輸入 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 作為您的主機值。 |
| `clientId` | 與您的 [!DNL Salesforce Marketing Cloud] 應用程式。 |
| `clientSecret` | 與您的 [!DNL Salesforce Marketing Cloud] 應用程式。 |

如需快速入門的詳細資訊，請參閱 [[!DNL Salesforce Marketing Cloud] 檔案](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 連接您的 [!DNL Salesforce Marketing Cloud] 帳戶

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Salesforce Marketing Cloud] 帳戶至Platform。

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以為其建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 您也可以使用搜尋列來縮小顯示的連接器。

在 [!UICONTROL 行銷自動化] 類別，選擇 **[!UICONTROL SalesforceMarketing Cloud]** 然後選取 **[!UICONTROL 設定]**.

![目錄](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

此 **[!UICONTROL 連接到SalesforceMarketing Cloud]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的 [!DNL Salesforce Marketing Cloud] 憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Salesforce Marketing Cloud] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL Salesforce Marketing Cloud] 帳戶。 您現在可以繼續下一個教學課程，以及 [設定資料流以將行銷自動化系統資料匯入Platform](../../dataflow/marketing-automation.md).
