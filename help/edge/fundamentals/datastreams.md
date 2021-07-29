---
title: 配置Experience PlatformWeb SDK的資料流
description: '了解如何設定資料流。 '
keywords: 設定；資料流；datastreamId;edge；資料流ID；環境設定；edgeConfigId；啟用身分；ID同步；ID同步容器ID；沙箱；串流入口；事件資料集；目標；用戶端代碼；屬性代號；目標環境ID;Cookie目的地；URL目的地；Analytics設定區塊報表套裝ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---


# 設定資料流

Adobe Experience Platform Web SDK的設定分為兩個位置。 SDK中的[configure命令](configuring-the-sdk.md)控制必須在用戶端上處理的項目，例如`edgeDomain`。 資料流會處理SDK的所有其他設定。 當請求傳送至Adobe Experience Platform邊緣網路時，會使用`edgeConfigId`參考伺服器端設定。 這可讓您更新設定，而無須在網站上變更程式碼。

您的組織必須布建此功能。 請連絡您的客戶成功經理(CSM)，以取得允許清單。

## 建立資料流配置

您可以使用資料流配置工具在資料收集UI中建立資料流。

![datastreams工具導航](../images/datastreams/config.png)

>[!NOTE]
>
>無論客戶是否使用Platform作為標籤管理員，資料流設定工具都可供允許清單上的客戶使用。 此外，使用者需要開發權限。 如需詳細資訊，請參閱標籤檔案中的[使用者權限](../../tags/ui/administration/user-permissions.md)文章。

按一下畫面右上方區域的&#x200B;**[!UICONTROL 新資料流]**，建立資料流。 提供名稱和說明後，系統會要求您提供每個環境的預設設定。 可用的設定將於下文詳細說明。

建立資料流時，系統會以相同設定自動建立三個環境。 這三個環境分別是&#x200B;*dev*、*stage*&#x200B;和&#x200B;*prod*。 它們符合標籤的三個預設環境。 當您建置標籤程式庫至開發環境時，程式庫會自動使用您設定中的開發環境。 您可以視需要編輯個別環境中的設定。

SDK中作為`edgeConfigId`使用的ID是指定設定和環境（例如`1c86778b-cdba-4684-9903-750e52912ad1:stage`）的複合ID。 如果複合ID中沒有任何環境（例如，上一個範例中的`stage`），則會使用生產環境。

以下是每個配置環境的可用設定。 大部分區段都可以啟用或停用。 停用時，會儲存您的設定，但未啟用。

## [!UICONTROL 第三方] IDSettings

第三方ID區段是唯一一律開啟的區段。 它有兩個可用的設定：&quot;[!UICONTROL 第三方ID同步已啟用]&quot;和&quot;[!UICONTROL 第三方ID同步容器ID]&quot;。

![設定UI的身分區段](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL 已啟用第三方ID同步]

控制SDK是否執行與第三方合作夥伴的身分同步。

### [!UICONTROL 第三方ID同步容器ID]

ID同步可分組為容器，以便在不同時間執行不同的ID同步。 這會控制為指定的設定ID執行哪個ID同步的容器。

## Adobe Experience Platform設定

此處列出的設定可讓您將資料傳送至Adobe Experience Platform。 只有在您已購買Adobe Experience Platform時，才應啟用此區段。

![Adobe Experience Platform設定區塊](../images/datastreams/edge_configuration_aep.png)

### [!UICONTROL 沙箱]

沙箱是Adobe Experience Platform中的位置，可讓客戶將其資料和實作彼此隔離。 如需其運作方式的詳細資訊，請參閱[沙箱檔案](../../sandboxes/home.md)。

### [!UICONTROL 串流入口]

串流入口是Adobe Experience Platform中的HTTP來源。 這些ID會在Adobe Experience Platform的「[!UICONTROL Sources]」標籤下以HTTP API形式建立。

### [!UICONTROL 事件資料集]

資料流支援將資料傳送至具有[!UICONTROL 體驗事件]結構的資料集。

## Adobe Target設定

若要設定Adobe Target，您必須提供用戶端代碼。 其他欄位為選用。

![Adobe Target設定區塊](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>與用戶端代碼相關聯的組織必須符合建立設定ID的組織。

### [!UICONTROL 用戶端代碼]

目標帳戶的唯一ID。 若要找到此資訊，您可以導覽至[!UICONTROL Adobe Target] > [!UICONTROL [!UICONTROL > ]實作] > [!UICONTROL 編輯]旁的設定[!UICONTROL ，適用於[!UICONTROL at.js]或[!UICONTROL mbox.js]]

### [!UICONTROL 屬性代號]

[!DNL Target] 可讓客戶透過使用屬性來控制權限。詳細資訊可在[!DNL Target]檔案的[企業權限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html)區段中找到。

您可以在[!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]中找到屬性代號

### [!UICONTROL 目標環境ID]

[](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Adobe Target中的環境可協助您透過所有開發階段管理實作。此設定會指定您要與每個環境搭配使用的環境。

Adobe建議您針對`dev`、`stage`和`prod`資料流環境分別以不同方式設定此設定，以保持簡單。 不過，如果您已定義Adobe Target環境，則可使用這些環境。

## Adobe Audience Manager設定

將資料傳送至Adobe Audience Manager所需的全部是啟用此區段。 其他設定為選用，但建議使用。

![Adobe對象管理設定區塊](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Cookie目的地已啟用]

允許SDK透過[Cookie目的地](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)從[!DNL Audience Manager]共用區段資訊。

### [!UICONTROL 已啟用URL目的地]

允許SDK透過[URL目的地](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)共用區段資訊。 這些設定在[!DNL Audience Manager]中。

## Adobe Analytics設定

控制資料是否傳送至Adobe Analytics。 其他詳細資訊位於[Analytics概述](../data-collection/adobe-analytics/analytics-overview.md)中。

![Adobe Analytics設定區塊](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL 報告套裝 ID]

您可在「Adobe Analytics管理員」區段的「[!UICONTROL 管理員>報表套裝]」下找到報表套裝。 若指定多個報表套裝，則資料會複製到每個報表套裝。
