---
title: 為Experience PlatformWeb SDK配置資料流
description: '瞭解如何配置資料流。 '
keywords: 配置；資料流；資料流；邊；資料流ID；環境設定；邊配置ID；標識；ID同步容器ID；沙盒；流入口；事件資料集；目標；客戶端代碼；屬性令牌；目標；Cookie環境ID；目標；url；分析設定塊報告套件ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 012ebbadc7149747df1414360eca6451836d6bbc
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 1%

---


# 配置資料流

Adobe Experience PlatformWeb SDK的配置分為兩個位置。 的 [configure命令](configuring-the-sdk.md) 在SDK中，控制必須在客戶端上處理的內容，如 `edgeDomain`。 資料流處理SDK的所有其它配置。 當請求發送到Adobe Experience Platform邊緣網路時， `edgeConfigId` 用於引用伺服器端配置。 這樣，您就可以更新配置，而無需在網站上進行代碼更改。

必須為您的組織設定此功能。 請聯繫您的客戶成功經理(CSM)以加入允許清單。

## 建立資料流配置

通過選擇 **[!UICONTROL 資料流]** 的子菜單。

![資料流工具導航](../images/datastreams/config.png)

>[!NOTE]
>
>當您可以訪問 [!UICONTROL 資料流] 頁籤無論您是否使用平台的標籤管理功能，您都必須具有開發人員權限才能自己管理資料流。 查看 [用戶權限](../../tags/ui/administration/user-permissions.md) 的子文檔。

通過按一下 **[!UICONTROL 新建資料流]** 在螢幕的右上角。 在提供名稱和說明後，系統會要求您提供每個環境的預設設定。 下面詳細介紹了可用設定。

建立資料流時，會自動建立三個具有相同設定的環境。 這三個環境 *開發*。 *階段*, *收縮*。 它們與標籤的三個預設環境相匹配。 在將標籤庫構建到開發環境時，庫會自動使用配置中的開發環境。 您可以編輯單個環境中的設定。

SDK中用作 `edgeConfigId` 是指定配置和環境(例如， `1c86778b-cdba-4684-9903-750e52912ad1:stage`)。 如果複合ID中不存在環境(例如， `stage` 在上例中)，則使用生產環境。

以下是每個配置環境的可用設定。 大多數節都可以啟用或禁用。 禁用後，將保存您的設定，但不處於活動狀態。

## [!UICONTROL 第三方ID] 設定

第三方ID部分是始終開啟的唯一部分。 它有兩個可用設定：&quot;[!UICONTROL 已啟用第三方ID同步]&quot;和&quot;[!UICONTROL 第三方ID同步容器ID]。

![配置UI的標識部分](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL 已啟用第三方ID同步]

控制SDK是否與第三方合作夥伴執行身份同步。

### [!UICONTROL 第三方ID同步容器ID]

ID同步可以分組到容器中，以允許在不同時間運行不同的ID同步。 這控制為給定配置ID運行哪個ID同步的容器。

## Adobe Experience Platform設定

此處列出的設定使您能夠將資料發送到Adobe Experience Platform。 只有在您購買了Adobe Experience Platform時，才應啟用此節。

![Adobe Experience Platform設定塊](../images/datastreams/platform-config.png)

| 欄位 | 說明 |
| --- | --- |
| [!UICONTROL 沙箱] | **（必需）** 選擇要向其發送資料的平台沙盒。 沙箱是Adobe Experience Platform的虛擬分區，允許您將資料和實施與組織中的其他人隔離開來。<br><br>建立資料流後，其沙盒將無法更改。 的 [!UICONTROL 沙盒] 因此，編輯現有資料流時，選擇欄位不可用。<br><br>有關沙箱在Experience Platform中角色的詳細資訊，請參見 [箱文檔](../../sandboxes/home.md)。 |
| [!UICONTROL 事件資料集] | **（必需）** 選擇將客戶事件資料流式傳輸到的平台資料集。 此架構必須使用 [XDM ExperienceEvent類](../../xdm/classes/experienceevent.md)。 |
| [!UICONTROL 配置檔案資料集] | 選擇客戶屬性資料將發送到的平台資料集。 此架構必須使用 [XDM個人配置檔案類](../../xdm/classes/individual-profile.md)。 |
| [!UICONTROL Offer Decisioning] | 選中此複選框可啟用平台Web SDK實現的Offer decisioning。 請參閱上的指南 [與平台Web SDK一起使用Offer decisioning](../personalization/offer-decisioning/offer-decisioning-overview.md) 的子菜單。 有關Offer decisioning功能的詳細資訊，請參閱 [Adobe Journey Optimizer文檔](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=zh-Hant)。 |
| [!UICONTROL 邊緣分割] | 選中此複選框以啟用 [邊緣分割](../../segmentation/ui/edge-segmentation.md) 資料流。 當平台Web SDK通過啟用邊緣分割的資料流發送資料時，響應中將返回有關配置檔案的任何更新的段成員身份。<br><br>此選項可與 [!UICONTROL 個性化目標] 為 [下一頁個性化用例](../../destinations/ui/configure-personalization-destinations.md)。 |
| [!UICONTROL 個性化目標] | 與 [!UICONTROL 邊緣分割] 複選框，此選項允許資料流連接到個性化引擎，如Adobe Target。 請參閱目標文檔以瞭解有關 [配置個性化目標](../../destinations/ui/configure-personalization-destinations.md)。 |

## Adobe Target設定

要配置Adobe Target，必須提供客戶端代碼。 其他欄位是可選的。

![Adobe Target設定塊](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>與客戶端代碼關聯的組織必須與建立配置ID的組織匹配。

### [!UICONTROL 用戶端代碼]

目標帳戶的唯一ID。 要查找此項，您可以導航到 [!UICONTROL Adobe Target] > [!UICONTROL 設定]> [!UICONTROL 實施] > [!UICONTROL 編輯設定] 的 [!UICONTROL 下載] 按鈕 [!UICONTROL at.js] 或 [!UICONTROL mbox.js]

### [!UICONTROL 屬性標籤]

[!DNL Target] 允許客戶通過使用屬性來控制權限。 詳細資訊可在 [企業權限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 的下界 [!DNL Target] 文檔。

可在中找到屬性令牌 [!UICONTROL Adobe Target] > [!UICONTROL 設定] > [!UICONTROL 屬性]

### [!UICONTROL 目標環境ID]

[環境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 在Adobe Target幫助您管理實施過程的所有階段。 此設定指定要與每個環境一起使用的環境。

Adobe建議對您的 `dev`。 `stage`, `prod` 資料流環境使事情變得簡單。 但是，如果您已經定義了Adobe Target環境，則可以使用這些環境。

## Adobe Audience Manager設定

向Adobe Audience Manager發送資料所需的只是啟用此部分。 其他設定是可選的，但是是鼓勵的。

![Adobe受眾管理設定塊](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL 已啟用Cookie目標]

允許SDK通過 [Cookie目標](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 從 [!DNL Audience Manager]。

### [!UICONTROL 已啟用URL目標]

允許SDK通過 [URL目標](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)。 這些配置在 [!DNL Audience Manager]。

## Adobe Analytics設定

控制資料是否發送到Adobe Analytics。 其他詳細資訊 [分析概述](../data-collection/adobe-analytics/analytics-overview.md)。

![Adobe Analytics設定塊](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL 報告套裝 ID]

報告套件可在Adobe Analytics管理區下 [!UICONTROL 「管理」>「報告套件」]。 如果指定了多個報表套件，則資料將複製到每個報表套件。
