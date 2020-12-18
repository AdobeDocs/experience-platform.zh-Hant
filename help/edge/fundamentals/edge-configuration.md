---
title: Edge Configuration
seo-title: Experience Platform Web SDK的Edge組態
description: '瞭解如何設定Experience Platform Edge Network。 '
seo-description: '瞭解如何設定Experience Platform Edge Network。 '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 94b3faf3157f4e1f4e46b6055914a04883dc44fa
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 設定Edge

Adobe Experience Platform Web SDK的組態分為兩個部分。 SDK中的[configure命令](configuring-the-sdk.md)可控制必須在用戶端上處理的事項，例如`edgeDomain`。 邊緣設定可處理SDK的所有其他設定。 當請求傳送至Adobe Experience Platform Edge Network時，`edgeConfigId`會用來參考伺服器端組態。 這可讓您更新設定，而不需在網站上變更程式碼。

您的組織必須已布建此功能。 請連絡您的客戶成功經理(CSM)，以加入允許清單。

## 建立邊配置

Edge組態可在Adobe [!DNL Experience Platform Launch]中使用Edge組態工具建立。

![邊緣配置工具導航](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>無論客戶是否使用[!DNL Experience Platform Launch]做為標籤管理器，允許清單上的客戶都可使用邊緣設定工具。 此外，使用者需要[!DNL Experience Platform Launch]中的「開發」權限。 如需詳細資訊，請參閱[!DNL Experience Platform Launch]檔案中的[使用者權限](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/admin/user-permissions.html)文章。

按一下畫面右上方區域的「新增邊緣設定」，建立邊緣設定。 ****&#x200B;在您提供名稱和說明後，系統會要求您針對每個環境提供預設設定。 可用的設定詳細如下。

在建立邊緣設定時，會自動建立3個設定相同的環境。 這三個環境是&#x200B;*dev*、*stage*&#x200B;和&#x200B;*prod*。 它們與[!DNL Experience Platform Launch]中的三個預設環境相匹配。 當您建立[!DNL Experience Platform Launch]程式庫至開發環境時，程式庫會自動使用您設定中的開發環境。 您可以視需要編輯個別環境中的設定。

SDK中用作`edgeConfigId`的ID是指定組態和環境（例如`1c86778b-cdba-4684-9903-750e52912ad1:stage`）的複合ID。 如果複合ID中沒有環境（例如，上例中`stage`），則使用生產環境。

在下面，您將找到每個配置環境的可用設定。 大部分區域都可以啟用或禁用。 停用時，您的設定會儲存，但並未作用中。

## [!UICONTROL 身分] 設定

身分區段是唯一永遠開啟的區段。 它有兩個可用的設定：&quot;[!UICONTROL ID同步]&quot;和&quot;[!UICONTROL ID同步容器ID]&quot;。

![配置UI的標識部分](../../assets/edge_configuration_identity.png)

### [!UICONTROL 啟用ID同步]

控制SDK是否與第三方合作夥伴執行身分同步。

### [!UICONTROL ID同步容器ID]

ID同步可分組至容器，以允許在不同時間執行不同的ID同步。 這會控制為指定的設定ID執行哪個ID同步的容器。

## Adobe Experience Platform設定

此處所列的設定可讓您將資料傳送至Adobe Experience Platform。 您只應在購買Adobe Experience Platform時啟用本節。

![Adobe Experience Platform設定區塊](../../assets/edge_configuration_aep.png)

### [!UICONTROL 沙盒]

沙盒是Adobe Experience Platform中的位置，可讓客戶將資料和建置彼此隔離。 如需其運作方式的詳細資訊，請參閱[沙盒檔案](../../sandboxes/home.md)。

### [!UICONTROL 串流入口]

串流入口是Adobe Experience Platform中的HTTP來源。 這些是在Adobe Experience Platform的「[!UICONTROL Sources]」標籤下建立為HTTP API。

### [!UICONTROL 事件資料集]

邊緣配置支援將資料發送到具有[!UICONTROL Experience Event]類別模式的資料集。

## Adobe Target設定

若要設定Adobe Target，您必須提供用戶端代碼。 其他欄位則為選用。

![Adobe Target設定區塊](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>與客戶端代碼關聯的組織必須與建立配置ID的組織匹配。

### [!UICONTROL 用戶端代碼]

目標帳戶的唯一ID。 若要找到此問題，您可導覽至[!UICONTROL Adobe Target] > [!UICONTROL Setup][!UICONTROL >] > [!UICONTROL [!UICONTROL 下載]按鈕旁的[!UICONTROL at.js]或&lt;a11/>設定a12/>mbox.js]][!UICONTROL 

### [!UICONTROL 屬性Token]

[!DNL Target] 可讓客戶透過使用屬性來控制權限。有關詳細資訊，請參閱[!DNL Target]文檔的[企業權限](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html)部分。

屬性Token可在[!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL 屬性]中找到

### [!UICONTROL 目標環境ID]

[Adobe ](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) Target的環境可協助您透過各個開發階段管理實作。此設定指定要與每個環境一起使用的環境。

Adobe建議您針對`dev`、`stage`和`prod`邊緣組態環境，以不同方式設定此設定，讓一切保持簡單。 不過，如果您已定義Adobe Target環境，則可使用這些環境。

## Adobe Audience Manager設定

傳送資料至Adobe Audience Manager所需的一切，就是啟用此區段。 其他設定是選擇性的，但建議使用。

![Adobe Audience Manage設定區塊](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie目標已啟用]

允許SDK透過[Cookie目標](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)從[!DNL Audience Manager]共用區段資訊。

### [!UICONTROL 啟用URL目標]

允許SDK透過[URL目標](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)分享區段資訊。 這些配置在[!DNL Audience Manager]中。

## Adobe Analytics設定

控制資料是否傳送至Adobe Analytics。 其他詳細資訊請參閱[Analytics概述](../data-collection/adobe-analytics/analytics-overview.md)。

![Adobe Analytics設定區塊](../../assets/edge_configuration_aa.png)

### [!UICONTROL 報告套裝 ID]

報表套裝位於[!UICONTROL 管理> ReportSuites]下方的「Adobe Analytics管理」區段中。 如果指定多個報表套裝，則資料會複製到每個報表套裝。
