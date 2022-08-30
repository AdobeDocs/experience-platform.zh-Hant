---
title: 資料流概述
description: 連接您的客戶端 Experience Platform SDK 與 Adobe 產品和協力廠商目標的整合。
keywords: 配置；資料流；資料流；邊；資料流ID；環境設定；邊配置ID；標識；ID同步容器ID；沙盒；流入口；事件資料集；目標；客戶端代碼；屬性令牌；目標；Cookie目標；URL目標；分析設定塊報表ID；資料資料收集準備；資料準備；映射器；XDM映射器；邊緣上的映射器；
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 45f5d23a671c8e015ca26e0d5025685255c2fc35
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 2%

---

# 資料流概述

資料流表示實施Adobe Experience PlatformWeb和移動SDK時的伺服器端配置。 當 [configure命令](../fundamentals/configuring-the-sdk.md) 在SDK中，控制必須在客戶端上處理的內容(如 `edgeDomain`)，資料流處理SDK的所有其它配置。 當請求發送到Adobe Experience Platform邊緣網路時， `edgeConfigId` 用於引用資料流。 這樣，您就可以更新伺服器端配置，而無需在網站上進行代碼更改。

本文檔介紹在資料收集UI中配置資料流的步驟。

## 訪問 [!UICONTROL 資料流] 工作區

通過選擇 **[!UICONTROL 資料流]** 的子菜單。

![資料收集UI中的資料流頁籤](../images/datastreams/overview/datastreams-tab.png)

的 [!UICONTROL 資料流] 頁籤顯示現有資料流的清單，包括其友好名稱、ID和上次修改日期。 選擇要 [查看其詳細資訊並配置服務](#view-details)。

選擇「更多」表徵圖(**...**)以顯示更多選項。 選擇 **[!UICONTROL 編輯]** 更新 [基本配置](#configure) 或選擇 **[!UICONTROL 刪除]** 刪除資料流。

![要編輯或刪除的選項和現有的資料流](../images/datastreams/overview/edit-datastream.png)

## 建立新資料流 {#create}

要建立資料流，請通過選擇 **[!UICONTROL 新建資料流]**。

![選擇新資料流](../images/datastreams/overview/new-datastream-button.png)

將顯示資料流建立工作流，從配置步驟開始。 在此處，必須提供資料流的名稱和可選說明。

如果要配置此資料流以在Experience Platform中使用，並且使用平台Web SDK，則還必須選擇 [基於事件的經驗資料模型(XDM)模式](../../xdm/classes/experienceevent.md) 表示您計畫接收的資料。

![資料流的基本配置](../images/datastreams/overview/configure.png)

選擇 **[!UICONTROL 高級選項]** 顯示配置資料流的其他控制項。

![高級配置選項](../images/datastreams/overview/advanced-options.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 地理位置] | 根據用戶的IP地址確定GPS查找是否發生。 預設設定 **[!UICONTROL 無]** 禁用任何GPS查找，而 **[!UICONTROL 城市]** 設定將GPS坐標設定為兩個小數位。 |
| [!UICONTROL 第一方ID Cookie] | 啟用後，此設定將指示邊緣網路在查找 [第一方設備ID](../identity/first-party-device-ids.md)，而不是在「身份映射」中查找此值。<br><br>啟用此設定時，必須提供應儲存ID的Cookie的名稱。 |
| [!UICONTROL 第三方ID同步] | ID同步可以分組到容器中，以允許在不同時間運行不同的ID同步。 啟用此設定後，可以指定為此資料流運行ID同步的容器。 |
| [!UICONTROL 訪問類型] | 定義驗證類型 [!DNL Edge Network] 接受資料流。 <ul><li>**[!UICONTROL 混合身份驗證]**:選中此選項後，邊緣網路將接受經過身份驗證的請求和未經身份驗證的請求。 當您計畫使用Web SDK或 [移動SDK](https://aep-sdks.gitbook.io/docs/)，以及 [伺服器API](../../server-api/overview.md)。 </li><li>**[!UICONTROL 僅經過身份驗證]**:選中此選項後，邊緣網路僅接受經過身份驗證的請求。 當您計畫僅使用伺服器API並希望阻止任何未經驗證的請求由 [!DNL Edge Network]。 </li></ul> |

在此處，如果要配置資料流以進行Experience Platform，請按照上面的教程操作 [資料收集的資料準備](./data-prep.md) 在返回本指南之前，將資料映射到平台事件架構。 否則，選擇 **[!UICONTROL 保存]** 繼續下一節。

## 查看資料流詳細資訊 {#view-details}

配置新資料流或選擇要查看的現有資料流後，將顯示該資料流的詳細資訊頁。 在此，您可以找到有關資料流（包括其ID）的詳細資訊。

![已建立資料流的「詳細資訊」頁](../images/datastreams/overview/view-details.png)

在資料流詳細資訊螢幕中， [添加服務](#add-services) 從您有權訪問的Adobe Experience Cloud產品啟用功能。 您還可以編輯資料流的 [基本配置](#create)，更新 [映射規則](./data-prep.md)。 [複製資料流](#copy)或將其完全刪除。

## 將服務添加到資料流 {#add-services}

在資料流的詳細資訊頁面上，選擇 **[!UICONTROL 添加服務]** 開始為該資料流添加可用服務。

![選擇添加服務以繼續](../images/datastreams/overview/add-service.png)

在下一螢幕上，使用下拉菜單選擇要為此資料流配置的服務。 只有您有權訪問的服務才會顯示在此清單中。

![從清單中選擇服務](../images/datastreams/overview/service-selection.png)

選擇所需的服務，填寫顯示的配置選項，然後選擇 **[!UICONTROL 保存]** 將服務添加到資料流。 所有添加的服務都顯示在資料流的詳細資訊視圖中。

![添加到資料流的服務](../images/datastreams/overview/services-added.png)

以下各節介紹了每項服務的配置選項。

>[!NOTE]
>
>每個服務配置都包含 **[!UICONTROL 已啟用]** 切換在選擇服務時自動激活的選項。 要禁用此資料流的選定服務，請選擇 **[!UICONTROL 已啟用]** 再次切換。

### Adobe Analytics設定 {#analytics}

此服務控制資料是否以及如何發送到Adobe Analytics。 有關其他詳細資訊，請參閱上 [將資料發送到分析](../data-collection/adobe-analytics/analytics-overview.md)。

![Adobe Analytics設定塊](../images/datastreams/overview/analytics-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 報告套裝 ID] | **（必需）** 要向其發送資料的分析報告套件的ID。 此ID可在Adobe AnalyticsUI下找到 [!UICONTROL 管理] > [!UICONTROL 報表套件]。 如果指定了多個報表套件，則資料將複製到每個報表套件。 |

### Adobe Audience Manager設定 {#audience-manager}

此服務控制資料是否以及如何發送到Adobe Audience Manager。 將資料發送到Audience Manager所需的一切就是啟用此部分。 其他設定是可選的，但是是鼓勵的。

![Adobe受眾管理設定塊](../images/datastreams/overview/audience-manager-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 已啟用Cookie目標] | 允許SDK通過 [cookie目標](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 從 [!DNL Audience Manager]。 |
| [!UICONTROL 已啟用URL目標] | 允許SDK通過 [URL目標](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) 從 [!DNL Audience Manager]。 |

### Adobe Experience Platform設定 {#aep}

>[!IMPORTANT]
>
>在為平台啟用資料流時，請注意您當前使用的平台沙箱，如資料收集UI頂部功能區中所示。
>
>![所選沙盒](../images/datastreams/overview/platform-sandbox.png)
>
>沙箱是Adobe Experience Platform的虛擬分區，允許您將資料和實施與組織中的其他人隔離開來。 建立資料流後，其沙盒將無法更改。 有關沙箱在Experience Platform中角色的詳細資訊，請參見 [箱文檔](../../sandboxes/home.md)。

此服務控制資料是否以及如何發送到Adobe Experience Platform。

![Adobe Experience Platform設定塊](../images/datastreams/overview/platform-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 事件資料集] | **（必需）** 選擇將客戶事件資料流式傳輸到的平台資料集。 此架構必須使用 [XDM ExperienceEvent類](../../xdm/classes/experienceevent.md)。 |
| [!UICONTROL 配置檔案資料集] | 選擇客戶屬性資料將發送到的平台資料集。 此架構必須使用 [XDM個人配置檔案類](../../xdm/classes/individual-profile.md)。 |
| [!UICONTROL Offer Decisioning] | 選中此複選框可啟用平台Web SDK實現的Offer decisioning。 請參閱上的指南 [與平台Web SDK一起使用Offer decisioning](../personalization/offer-decisioning/offer-decisioning-overview.md) 的子菜單。 有關Offer decisioning功能的詳細資訊，請參閱 [Adobe Journey Optimizer文檔](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=zh-Hant)。 |
| [!UICONTROL 邊緣分割] | 選中此複選框以啟用 [邊緣分割](../../segmentation/ui/edge-segmentation.md) 資料流。 當SDK通過啟用邊緣分割的資料流發送資料時，在響應中將有關配置檔案的任何更新的段成員身份發回。<br><br>此選項可與 [!UICONTROL 個性化目標] 為 [下一頁個性化用例](../../destinations/ui/configure-personalization-destinations.md)。 |
| [!UICONTROL 個性化目標] | 與 [!UICONTROL 邊緣分割] 複選框，此選項允許資料流連接到個性化引擎，如Adobe Target。 請參閱目標文檔以瞭解有關 [配置個性化目標](../../destinations/ui/configure-personalization-destinations.md)。 |

### Adobe Target設定 {#target}

此服務控制資料是否以及如何發送到Adobe Target。

![Adobe Target設定塊](../images/datastreams/overview/target-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 屬性標籤] | [!DNL Target] 允許客戶通過使用屬性來控制權限。 有關屬性的詳細資訊，請參見上的指南 [配置企業權限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 的 [!DNL Target] 文檔。<br><br>在Adobe TargetUI中，可以找到屬性令牌 [!UICONTROL 設定] > [!UICONTROL 屬性]。 |
| [!UICONTROL 目標環境ID] | [Adobe Target環境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 幫助您管理實施過程的所有階段。 此設定指定要與此資料流一起使用的環境。<br><br>最佳做法是為您的 `dev`。 `stage`, `prod` 資料流環境使事情變得簡單。 但是，如果您已經定義了Adobe Target環境，則可以使用這些環境。 |
| [!UICONTROL 目標第三方ID命名空間] | 的標識命名空間 `mbox3rdPartyId` 要用於此資料流。 請參閱上的指南 [實施 `mbox3rdPartyId` Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md) 的子菜單。 |

### [!UICONTROL 事件轉發] 設定

此服務控制資料是否以及如何發送到 [事件轉發](../../tags/ui/event-forwarding/overview.md)。

![配置UI的「事件轉發」部分](../images/datastreams/overview/event-forwarding-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 啟動屬性] | **（必需）** 要向其發送資料的事件轉發屬性。 |
| [!UICONTROL 啟動環境] | **（必需）** 要向其發送資料的選定屬性中的環境。 |

>[!NOTE]
>
>可以選擇 **[!UICONTROL 手動輸入ID]** 鍵入屬性和環境名稱，而不是使用下拉菜單。

## 複製資料流 {#copy}

您可以建立現有資料流的副本，並根據需要更改其詳細資訊。

>[!NOTE]
>
>只能在同一資料流內複製資料流 [沙坑](../../sandboxes/home.md)。 換句話說，不能將資料流從一個沙箱複製到另一個沙箱。

從 [!UICONTROL 資料流] 工作區，選擇省略號(**...。**)，然後選擇 **[!UICONTROL 複製]**。

![顯示 [!UICONTROL 複製] 從資料流清單視圖中選擇的選項](../images/datastreams/overview/copy-datastream-list.png)

或者，可以選擇 **[!UICONTROL 複製資料流]** 從給定資料流的詳細資訊視圖中。

![顯示 [!UICONTROL 複製] 從資料流詳細資訊視圖中選擇的選項](../images/datastreams/overview/copy-datastream-details.png)

此時將顯示確認對話框，提示您為要建立的新資料流提供唯一名稱，以及將複製的配置選項的詳細資訊。 準備好後，選擇 **[!UICONTROL 複製]**。

![用於複製資料流的確認對話框的影像](../images/datastreams/overview/copy-datastream-confirm.png)

首頁 [!UICONTROL 資料流] 工作區將重新顯示，並列出新資料流。

## 後續步驟

本指南介紹了如何管理資料收集UI中的資料流。 有關如何在設定資料流後安裝和配置Web SDK的詳細資訊，請參閱 [資料收集E2E指南](../../collection/e2e.md#install)。
