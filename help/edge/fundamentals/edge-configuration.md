---
title: Edge Configuration
seo-title: Experience Platform Web SDK的Edge組態
description: '瞭解如何設定Experience Platform Edge Network。 '
seo-description: '瞭解如何設定Experience Platform Edge Network。 '
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---


# 設定Edge

Adobe Experience Platform的設定分 [!DNL Web SDK] 為兩個位置。 SDK [中的configure命令](configuring-the-sdk.md) ，可控制用戶端上必須處理的事項，例如 `edgeDomain`。 邊緣設定可處理SDK的所有其他設定。 當請求傳送至Adobe Experience Platform時， [!DNL Edge Network]會 `edgeConfigId` 用來參考伺服器端組態。 這可讓您更新設定，而不需在網站上變更程式碼。

## 建立邊配置ID

Edge組態ID可在Adobe中使 [!DNL Launch] 用Edge組態工具建立。 此工具可讓您同時建立邊緣組態以及這些組態中的環境。

![邊緣配置工具導航](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>
>
>無論客戶是否使用標籤管理器，允許清單上的邊緣設定工具 [!DNL Launch] 都可供客戶使用。 此外，使用者需要中的「開發」權限 [!DNL Launch]。 如需詳細 [資訊，請參閱](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/admin/user-permissions.html) 「使用者 [!DNL Launch] 權限」文章。

您可以按一下畫面右上方區域 **[!UICONTROL 的「新增邊緣設定」]** ，建立邊緣設定。 在您提供名稱和說明後，系統會要求您針對每個環境提供預設設定。

### 預設環境設定

這些預設設定可用來建立前三個設定相同的環境。 這三種環境 *包括* dev、 *stage*&#x200B;和 *prod*。 它們與中的三個預設環境相匹配 [!DNL Launch]。 當您建立程式庫 [!DNL Launch] 至開發環境時，程式庫會自動使用您設定中的開發環境。 您可以視需要編輯個別環境中的設定。

SDK中使用的ID是指 `edgeConfigId` 定配置和環境的複合ID。 如果沒有環境，則使用生產環境。

### 環境設定

以下是環境可用的每個設定。 大部分區域都可以啟用或禁用。 停用時，您的設定會儲存，但並未作用中。

#### [!UICONTROL 身份]

身分區段是唯一永遠開啟的區段。 它有兩個可用的設定： [!UICONTROL ID同步] , [!UICONTROL ID同步容器ID]。

![配置UI的標識部分](../../assets/edge_configuration_identity.png)

##### [!UICONTROL 啟用ID同步]

控制SDK是否與第三方合作夥伴執行身分同步。

##### [!UICONTROL ID同步容器ID]

ID同步可分組至容器，以允許在不同時間執行不同的ID同步。 這會控制為指定的設定ID執行哪個ID同步的容器。

#### Adobe Experience Platform

此處所列的設定可讓您將資料傳送至Adobe Experience Platform。 您只應在購買Adobe Experience Platform時啟用本節。

![Adobe Experience Platform設定區塊](../../assets/edge_configuration_aep.png)

##### [!UICONTROL 沙盒]

沙盒是Adobe Experience Platform中的位置，可讓客戶將資料和建置彼此隔離。 如需其運作方式的詳細資訊，請參閱「 [Sandbox」檔案](../../sandboxes/home.md)。

##### [!UICONTROL 串流入口]

串流入口是Adobe Experience Platform中的HTTP來源。 這些是在Adobe Experience Platform的 [!UICONTROL Sources] 標籤下建立為HTTP API。

##### [!UICONTROL 事件資料集]

邊緣設定支援將資料傳送至具有類別 [!UICONTROL Experience Event架構的資料集]。

#### Adobe Target

若要設定Adobe Target，您必須提供用戶端代碼。 其他欄位則為選用。

![Adobe Target設定區塊](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>
>
>與客戶端代碼關聯的組織必須與建立配置ID的組織匹配。

##### [!UICONTROL 用戶端代碼]

目標帳戶的唯一ID。 若要找到此項目，您可導覽至 [!UICONTROL Adobe Target] > [!UICONTROL Setup][!UICONTROL Implementation] >下一個要下載Button的Adobe Target. [!UICONTROL Js或Mbox.js的Adobe Target.Js.js的Adobe Button，以進行下載。]

##### [!UICONTROL 屬性Token]

[!DNL Target] 可讓客戶透過使用屬性來控制權限。 如需詳細資訊，請參 [閱檔案的](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) 「企業權限」 [!DNL Target] 區段。

屬性Token可在 [!UICONTROL Adobe Target] >設定 [!UICONTROL >屬][!UICONTROL 性]

##### [!UICONTROL 目標環境ID]

[Adobe](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) Target中的環境可協助您管理所有開發階段的實作。 此設定指定要與每個環境一起使用的環境。

Adobe建議您對每個、和邊緣組態環境 `dev`設定 `stage`此 `prod` 項，以保持簡單。 不過，如果您已定義 [!UICONTROL Adobe Target環境] ，則可使用這些環境。

#### Adobe Audience Manager

傳送資料至Adobe Audience Manager所需的一切，就是啟用此區段。 其他設定是選擇性的，但建議使用。

![Adobe Audience Manage設定區塊](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie目標已啟用]

允許SDK透過Cookie目標共用區 [段資訊](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)[!DNL Audience Manager]。

##### [!UICONTROL 啟用URL目標]

允許SDK透過 [URL目標分享區段資訊](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)。 這些配置在中 [!DNL Audience Manager]。

#### Adobe Analytics

控制資料是否傳送至Adobe Analytics。 其他詳細資訊請參閱 [Analytics概述](../solution-specific/analytics/analytics-overview.md)。

![Adobe Analytics設定區塊](../../assets/edge_configuration_aa.png)

##### [!UICONTROL 報告套裝 ID]

報表套裝位於「管理員>報表套裝」下的「Adobe Analytics管 [!UICONTROL 理員」區段]。 如果指定多個報表套裝，則資料會複製到每個報表套裝。
