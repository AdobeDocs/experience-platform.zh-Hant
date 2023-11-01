---
title: Adobe Commerce來源聯結器
description: 瞭解如何使用Adobe Commerce來源將您的商務資料帶入Experience Platform。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# Adobe Commerce

Adobe Commerce是敏捷的B2B和B2C商業平台，可讓商家和品牌透過線上和實體空間以客戶為中心的數位商業體驗來加速收入。

Adobe Experience Platform來源支援Adobe Commerce的整合，可讓商家將店面和後台資料傳送至Experience Platform Edge Network，以便其他Adobe Experience Cloud產品(例如Adobe Analytics和Adobe Target)可以使用 [!DNL Commerce] 資料。

* **店面活動**：擷取購物者互動，例如 `View Page`， `View Product`、和 `Add to Cart`. 對於B2B商家，店面活動也會擷取 [請購單清單](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **後台活動**：擷取訂單狀態的相關資訊，例如是否已下訂單、已取消、已退款、已出貨或完成。

>[!NOTE]
>
>Adobe Commerce中擷取的資料不含個人識別資訊(PII)。 所有使用者識別碼（例如Cookie ID和IP位址）都需嚴格匿名處理。

## 先決條件

若要將Adobe Commerce連線至Experience Platform，您必須具備下列條件：

* Adobe Commerce 2.4.3或更新版本。
* 有效的Adobe ID和組織ID。
* 存取 [Adobe使用者端資料層擴充功能](../../../tags/extensions/client/client-data-layer/overview.md). 收集店面事件資料需要此擴充功能。
* 其他AdobeDX產品的權益。

## 入門步驟

若要讓Adobe Commerce來源帳戶完全上線，請依照下列步驟以及其對應檔案操作。

* [安裝Experience Platform聯結器擴充功能](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html) 適用於Adobe Commerce。 您可以從以下位置下載聯結器擴充功能： [Adobe市集](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* 成功安裝聯結器擴充功能後，請在Experience Cloud中登入您的Adobe帳戶並 [確認您的組織ID](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). 此ID與您布建的Experience Cloud公司相關聯。 其格式為24個字元的英數字串，並包含必要字串 `@AdobeOrg`.
* 接下來，使用商務特定欄位群組建立或更新您的Experience Data Model (XDM)結構描述。 如需將Commerce專用欄位群組新增至XDM結構的詳細步驟，請閱讀以下指南： [將欄位群組新增至XDM結構描述](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html).
* 設定結構描述後，您必須根據新結構描述建立資料集。 然後，此資料集將包含 [!DNL Commerce] 您傳送的資料。 如需如何建立資料集的詳細步驟， [!DNL Commerce] 資料，請閱讀指南： [傳送資料給Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* 接下來，建立資料串流並選取包含您的Commerce特定欄位群組的XDM結構描述。 如需資料串流的詳細資訊，請參閱 [資料串流概觀](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hant).
* 接著，您必須將Adobe Commerce執行個體連結至 [Commerce服務聯結器](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). 這可讓您的Commerce執行個體部署為SaaS （軟體即服務）。
* 完成上述所有設定後，您現在可以使用設定Commerce Services聯結器和Experience Platform聯結器來連線到Experience Platform。 [!DNL Commerce Admin]. 如需此最終步驟的詳細資訊，請閱讀以下指南： [將Commerce資料連線到Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html).
