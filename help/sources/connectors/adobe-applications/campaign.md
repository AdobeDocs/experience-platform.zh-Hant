---
keywords: Experience Platform；首頁；熱門主題；Adobe Campaign Managed Cloud Services；行銷活動；campaign managed services
title: Adobe Campaign Managed Cloud Services
description: 瞭解如何使用使用者介面將Campaign ManagedCloud Service連結至Platform
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: 39a503b14c731aeed279bbbfa8c814c2ec26ed92
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 1%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Adobe Campaign Managed Cloud Services為跨頻道客戶體驗設計提供了Managed Services平台，同時為視覺行銷活動的策劃、即時互動管理和跨頻道執行提供適合環境。 造訪 [Adobe Campaign v8檔案](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=en) 以取得詳細資訊。

Adobe Campaign Managed Cloud Services來源可讓您將Adobe Campaign v8傳送記錄檔和追蹤記錄檔資料帶入Adobe Experience Platform。

## 先決條件

建立來源連線以Experience PlatformCampaign v8之前，您必須先完成下列必要條件：

* [使用Adobe Campaign使用者端主控台設定事件記錄檔匯入](#view-delivery-and-tracking-log-data)
* [建立XDM ExperienceEvent結構描述](#create-a-schema)
* [建立資料集](#create-a-dataset)

### 檢視傳遞和追蹤記錄資料 {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>您必須能存取Adobe Campaign v8使用者端主控台，才能在Campaign中檢視記錄資料。 造訪 [Campaign v8檔案](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=en) 有關如何下載和安裝使用者端主控台的資訊。

透過使用者端主控台登入您的Campaign v8執行個體。 在 [!DNL Explorer] 索引標籤，選取 [!DNL Administration] 然後選取 [!DNL Configuration]. 接下來，選取 [!DNL Data schemas] 然後套用 `broadLog` 篩選名稱或標籤。 在出現的清單中，選取名稱為的收件者傳遞記錄來源結構描述 `broadLogRcp`.

![Adobe Campaign v8使用者端主控台已選取瀏覽器索引標籤，管理、設定和資料結構描述節點已展開，篩選設定為「廣泛」。](./images/campaign/explorer.png)

接下來，選取 **資料** 標籤。

![已選取資料索引標籤的Adobe Campaign v8使用者端主控台。](./images/campaign/data.png)

在資料面板中按一下滑鼠右鍵/按一下滑鼠鍵以開啟內容功能表。 從這裡，選擇 **設定清單……**

![開啟內容功能表並選取「設定清單」選項的Adobe Campaign v8使用者端主控台。](./images/campaign/configure.png)

清單設定視窗會出現，為您提供介面，您可以在其中將任何所需欄位新增到預先存在的清單中，以在資料面板中檢視資料。

![收件者傳遞記錄的設定清單，可新增以供檢視。](./images/campaign/list-configuration.png)

現在您可以檢視收件者傳遞記錄，包括上一步驟中新增的設定欄位。

>[!TIP]
>
>您可以重複相同的步驟，但篩選為 `tracking` 以檢視您的追蹤記錄檔資料。

![收件者傳遞記錄會顯示其上次修改的名稱、傳遞管道、內部傳遞名稱和標籤的資訊。](./images/campaign/recipient-delivery-logs.png)

### 建立結構描述 {#create-a-schema}

接下來，針對傳送記錄檔和追蹤記錄檔建立XDM ExperienceEvent結構。 您必須將「行銷活動傳送記錄」欄位群組套用至您的傳送記錄綱要，並將「行銷活動追蹤記錄」欄位群組套用至您的追蹤記錄綱要。 您也必須定義 `externalID` 欄位做為結構描述的主要身分識別。

>[!NOTE]
>
>您的XDM ExperienceEvent結構描述必須已啟用設定檔，才能將您的Campaign資料擷取至 [!DNL Real-Time Customer Profile].

如需如何建立結構的詳細指示，請閱讀以下指南： [在UI中建立XDM結構描述](../../../xdm/tutorials/create-schema-ui.md).

### 建立資料集 {#create-a-dataset}

最後，您必須為結構描述建立資料集。 如需如何建立資料集的詳細指示，請閱讀以下指南： [在UI中建立資料集](../../../catalog/datasets/user-guide.md).

## 使用Platform UI建立Adobe Campaign Managed Cloud Services來源連線

現在您已在Campaign使用者端主控台中存取資料記錄、建立結構描述和資料集，接著可以繼續建立來源連線，將您的Campaign Managed Services資料引進Platform。

如需將Campaign v8傳送記錄檔和追蹤記錄檔資料帶入Experience Platform的詳細指示，請閱讀以下指南： [在UI中建立Campaigned Managed Services來源連線](../../tutorials/ui/create/adobe-applications/campaign.md).

>[!IMPORTANT]
>
>在邊緣案例中，最近移除的電子郵件收件者與電子郵件的互動，可能會將個人資訊重新擷取到Experience Platform。 在某些情況下，這可能會重新啟用該使用者的行銷。
>
>* 此情境僅在Experience Platform中執行隱私權要求與在Adobe Campaign Classic中執行之間有效。 在Campaign中執行要求後，會進行檢查以確保記錄未匯出至Campaign。 請在執行72小時後重新發出GDPR請求以解決此問題。