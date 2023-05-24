---
title: 設定資料流
description: 瞭解如何將客戶端Web SDK整合與其他Adobe產品和第三方目標連接。
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: 209aa63717e05fabc8742ac591102b8fdb243ee4
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 2%

---


# 設定資料流

本文檔介紹配置 [資料流](./overview.md) 的子菜單。

## 訪問 [!UICONTROL 資料流] 工作區

通過選擇Data Collection UI或Experience PlatformUI，可以建立和管理資料流 **[!UICONTROL 資料流]** 的子菜單。

![資料收集UI中的資料流頁籤](../assets/datastreams/configure/datastreams-tab.png)

的 **[!UICONTROL 資料流]** 頁籤顯示現有資料流的清單，包括其友好名稱、ID和上次修改日期。 選擇要 [查看其詳細資訊並配置服務](#view-details)。

選擇「更多」表徵圖(**...**)以顯示更多選項。 選擇 **[!UICONTROL 編輯]** 更新 [基本配置](#configure) 或選擇 **[!UICONTROL 刪除]** 刪除資料流。

![編輯或刪除現有資料流的選項](../assets/datastreams/configure/edit-datastream.png)

## 建立新資料流 {#create}

要建立資料流，請通過選擇 **[!UICONTROL 新建資料流]**。

![選擇新資料流](../assets/datastreams/configure/new-datastream-button.png)

將顯示資料流建立工作流，從配置步驟開始。 在此處，必須提供資料流的名稱和可選說明。

如果要配置此資料流以在Experience Platform中使用，並且使用平台Web SDK，則還必須選擇 [基於事件的經驗資料模型(XDM)模式](../../xdm/classes/experienceevent.md) 表示您計畫接收的資料。

![資料流的基本配置](../assets/datastreams/configure/configure.png)

選擇 **[!UICONTROL 高級選項]** 顯示配置資料流的其他控制項。

![高級配置選項](../assets/datastreams/configure/advanced-options.png) {#advanced-options}

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 地理位置] | 根據用戶的IP地址確定是否進行地理位置查找。 預設設定 **[!UICONTROL 無]** 禁用任何地理位置查找，而 **[!UICONTROL 城市]** 設定將GPS坐標設定為兩個小數位。 地理位置在 [!UICONTROL IP混淆] 不受  [!UICONTROL IP混淆] 的子菜單。 |
| [!UICONTROL IP 模糊化] | 指示要應用於資料流的IP混淆類型。 任何基於客戶IP的處理都將受IP混淆設定的影響。 這包括從資料流接收資料的所有Experience Cloud服務。 <p>可用選項：</p> <ul><li>**[!UICONTROL 無]**:禁用IP混淆。 完整用戶IP地址將通過資料流發送。</li><li>**[!UICONTROL 部分]**:對於IPv4地址，對用戶IP地址的最後一個八進位進行模糊處理。 對於IPv6地址，對地址的最後80位進行模糊處理。 <p>範例：</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL 滿]**:對整個IP地址進行模糊處理。 <p>範例：</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> IP混淆對其他Adobe產品的影響： <ul><li>**Adobe Target**:資料流級別 [!UICONTROL IP混淆] 設定優先於在Adobe Target設定的任何IP混淆選項。 例如，如果 [!UICONTROL IP混淆] 選項設定為 **[!UICONTROL 滿]** 而Adobe TargetIP混淆選項設定為 **[!UICONTROL 上次八位數模糊處理]**&#x200B;而Adobe Target將獲得完全模糊的IP。 請參閱Adobe Target文檔 [IP混淆](https://developer.adobe.com/target/before-implement/privacy/privacy/) 和 [地理位置](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=en) 的子菜單。</li><li>**Audience Manager**:資料流級別的IP混淆設定優先於Audience Manager中設定的任何IP混淆選項，並應用於所有IP地址。 由Audience Manager完成的任何地理位置查找都受資料流級別的影響 [!UICONTROL IP混淆] 的雙曲餘切值。 基於完全模糊的IP的Audience Manager中的地理位置查找將導致未知區域，並且不會實現基於結果的地理位置資料的任何段。 請參閱上的Audience Manager文檔 [IP混淆](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html?lang=en) 的子菜單。</li><li>**Adobe Analytics**:如果選擇了IP混淆選項（NONE除外）,Adobe Analytics當前將接收部分模糊化的IP地址。 要使分析接收完全模糊化的IP地址，必須在Adobe Analytics單獨配置IP模糊。 此行為將在以後的版本中更新。 見Adobe Analytics [文檔](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html) 有關如何在分析中啟用IP混淆的詳細資訊。</li></ul> |
| [!UICONTROL 第一方ID Cookie] | 啟用後，此設定將指示邊緣網路在查找 [第一方設備ID](../identity/first-party-device-ids.md)，而不是在「身份映射」中查找此值。<br><br>啟用此設定時，必須提供應儲存ID的Cookie的名稱。 |
| [!UICONTROL 第三方ID同步] | ID同步可以分組到容器中，以允許在不同時間運行不同的ID同步。 啟用此設定後，可以指定為此資料流運行ID同步的容器。 |
| [!UICONTROL 第三方ID同步容器ID] | 要用於第三方ID同步的容器的數字ID。 |
| [!UICONTROL 容器ID覆蓋] | 在本節中，您可以定義其他第三方ID同步容器ID，您可以使用這些ID覆蓋預設容器ID。 |
| [!UICONTROL 訪問類型] | 定義邊緣網路接受的資料流的驗證類型。 <ul><li>**[!UICONTROL 混合身份驗證]**:選中此選項後，邊緣網路將接受經過身份驗證的請求和未經身份驗證的請求。 當您計畫使用Web SDK或 [移動SDK](https://aep-sdks.gitbook.io/docs/)，以及 [伺服器API](../../server-api/overview.md)。 </li><li>**[!UICONTROL 僅經過身份驗證]**:選中此選項後，邊緣網路僅接受經過身份驗證的請求。 當您計畫僅使用伺服器API並希望阻止邊緣網路處理任何未經驗證的請求時，請選擇此選項。</li></ul> |

在此處，如果要配置資料流以進行Experience Platform，請按照上面的教程操作 [資料收集的資料準備](./data-prep.md) 在返回本指南之前，將資料映射到平台事件架構。 否則，選擇 **[!UICONTROL 保存]** 繼續下一節。

## 查看資料流詳細資訊 {#view-details}

配置新資料流或選擇要查看的現有資料流後，將顯示該資料流的詳細資訊頁。 在此，您可以找到有關資料流（包括其ID）的詳細資訊。

![已建立資料流的「詳細資訊」頁](../assets/datastreams/configure/view-details.png)

在資料流詳細資訊螢幕中， [添加服務](#add-services) 從您有權訪問的Adobe Experience Cloud產品啟用功能。 您還可以編輯資料流的 [基本配置](#create)，更新 [映射規則](./data-prep.md)。 [複製資料流](#copy)或將其完全刪除。

## 將服務添加到資料流 {#add-services}

在資料流的詳細資訊頁面上，選擇 **[!UICONTROL 添加服務]** 開始為該資料流添加可用服務。

![選擇添加服務以繼續](../assets/datastreams/configure/add-service.png)

在下一螢幕上，使用下拉菜單選擇要為此資料流配置的服務。 只有您有權訪問的服務才會顯示在此清單中。

![從清單中選擇服務](../assets/datastreams/configure/service-selection.png)

選擇所需的服務，填寫顯示的配置選項，然後選擇 **[!UICONTROL 保存]** 將服務添加到資料流。 所有添加的服務都顯示在資料流的詳細資訊視圖中。

![添加到資料流的服務](../assets/datastreams/configure/services-added.png)

以下各節介紹了每項服務的配置選項。

>[!NOTE]
>
>每個服務配置都包含 **[!UICONTROL 已啟用]** 切換在選擇服務時自動激活的選項。 要禁用此資料流的選定服務，請選擇 **[!UICONTROL 已啟用]** 再次切換。

### Adobe Analytics設定 {#analytics}

此服務控制資料是否以及如何發送到Adobe Analytics。 有關其他詳細資訊，請參閱上 [將資料發送到分析](../data-collection/adobe-analytics/analytics-overview.md)。

![Adobe Analytics設定塊](../assets/datastreams/configure/analytics-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 報告套裝 ID] | **（必需）** 要向其發送資料的分析報告套件的ID。 此ID可在Adobe AnalyticsUI下找到 [!UICONTROL 管理] > [!UICONTROL 報表套件]。 如果指定了多個報表套件，則資料將複製到每個報表套件。 |
| [!UICONTROL 報表套件覆蓋] | 在本節中，您可以添加可用於覆蓋預設報表套件ID的其他報表套件ID。 |

### Adobe Audience Manager設定 {#audience-manager}

此服務控制資料是否以及如何發送到Adobe Audience Manager。 將資料發送到Audience Manager所需的一切就是啟用此部分。 其他設定是可選的，但是是鼓勵的。

![Adobe受眾管理設定塊](../assets/datastreams/configure/audience-manager-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 已啟用Cookie目標] | 允許SDK通過 [cookie目標](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 從 [!DNL Audience Manager]。 |
| [!UICONTROL 已啟用URL目標] | 允許SDK通過 [URL目標](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) 從 [!DNL Audience Manager]。 |

### Adobe Experience Platform設定 {#aep}

>[!IMPORTANT]
>
>在為平台啟用資料流時，請注意您當前使用的平台沙箱，如UI頂部功能區中所示。
>
>![所選沙盒](../assets/datastreams/configure/platform-sandbox.png)
>
>沙箱是Adobe Experience Platform的虛擬分區，允許您將資料和實施與組織中的其他人隔離開來。 建立資料流後，其沙盒將無法更改。 有關沙箱在Experience Platform中角色的詳細資訊，請參見 [箱文檔](../../sandboxes/home.md)。

此服務控制資料是否以及如何發送到Adobe Experience Platform。

![Adobe Experience Platform設定塊](../assets/datastreams/configure/platform-config.png)

| 設定 | 說明 |
|---| --- |
| [!UICONTROL 事件資料集] | **（必需）** 選擇將客戶事件資料流式傳輸到的平台資料集。 此架構必須使用 [XDM ExperienceEvent類](../../xdm/classes/experienceevent.md)。 要添加其他資料集，請選擇 **[!UICONTROL 添加事件資料集]**。 |
| [!UICONTROL 配置檔案資料集] | 選擇客戶屬性資料將發送到的平台資料集。 此架構必須使用 [XDM個人配置檔案類](../../xdm/classes/individual-profile.md)。 |
| [!UICONTROL Offer Decisioning] | 選中此複選框可啟用平台Web SDK實現的Offer decisioning。 請參閱上的指南 [與平台Web SDK一起使用Offer decisioning](../personalization/offer-decisioning/offer-decisioning-overview.md) 的子菜單。<br><br>有關Offer decisioning功能的詳細資訊，請參閱 [Adobe Journey Optimizer文檔](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=zh-Hant)。 |
| [!UICONTROL 邊緣分割] | 選中此複選框以啟用 [邊緣分割](../../segmentation/ui/edge-segmentation.md) 資料流。 當SDK通過啟用邊緣分割的資料流發送資料時，在響應中將有關配置檔案的任何更新的段成員身份發回。<br><br>此選項可與 [!UICONTROL 個性化目標] 為 [下一頁個性化用例](../../destinations/ui/configure-personalization-destinations.md)。 |
| [!UICONTROL 個性化目標] | 啟用後啟用此功能時 [!UICONTROL 邊緣分割] 複選框，此選項允許資料流連接到個性化目標，如 [自定義個性化](../../destinations/catalog/personalization/custom-personalization.md)。<br><br>請參閱目標文檔以瞭解有關 [配置個性化目標](../../destinations/ui/configure-personalization-destinations.md)。 |
| [!UICONTROL Adobe Journey Optimizer] | 選中此複選框以啟用 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) 資料流。 <br><br> 啟用此選項允許資料流從Web和基於應用的入站市場活動中返回個性化內容 [!DNL Adobe Journey Optimizer]。 此選項需要 [!UICONTROL 邊緣分割] 激活。 如果 [!UICONTROL 邊緣分割] 未選中，此選項將呈灰色顯示。 |

### Adobe Target設定 {#target}

此服務控制資料是否以及如何發送到Adobe Target。

![Adobe Target設定塊](../assets/datastreams/configure/target-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 屬性標籤] | [!DNL Target] 允許客戶通過使用屬性來控制權限。 有關屬性的詳細資訊，請參見上的指南 [配置企業權限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 的 [!DNL Target] 文檔。<br><br>在Adobe TargetUI中，可以找到屬性令牌 [!UICONTROL 設定] > [!UICONTROL 屬性]。 |
| [!UICONTROL 目標環境ID] | [Adobe Target環境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 幫助您管理實施過程的所有階段。 此設定指定要與此資料流一起使用的環境。<br><br>最佳做法是為您的 `dev`。 `stage`, `prod` 資料流環境使事情變得簡單。 但是，如果您已經定義了Adobe Target環境，則可以使用這些環境。 |
| [!UICONTROL 目標第三方ID命名空間] | 的標識命名空間 `mbox3rdPartyId` 要用於此資料流。 請參閱上的指南 [實施 `mbox3rdPartyId` Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md) 的子菜單。 |
| [!UICONTROL 屬性令牌覆蓋] | 在本節中，您可以定義可用於覆蓋預設屬性標籤的附加屬性標籤。 |

### [!UICONTROL 事件轉發] 設定

此服務控制資料是否以及如何發送到 [事件轉發](../../tags/ui/event-forwarding/overview.md)。

![配置UI的「事件轉發」部分](../assets/datastreams/configure/event-forwarding-config.png)

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

![顯示 [!UICONTROL 複製] 從資料流清單視圖中選擇的選項](../assets/datastreams/configure/copy-datastream-list.png)

或者，可以選擇 **[!UICONTROL 複製資料流]** 從給定資料流的詳細資訊視圖中。

![顯示 [!UICONTROL 複製] 從資料流詳細資訊視圖中選擇的選項](../assets/datastreams/configure/copy-datastream-details.png)

此時將顯示確認對話框，提示您為要建立的新資料流提供唯一名稱，以及將複製的配置選項的詳細資訊。 準備好後，選擇 **[!UICONTROL 複製]**。

![用於複製資料流的確認對話框的影像](../assets/datastreams/configure/copy-datastream-confirm.png)

首頁 [!UICONTROL 資料流] 工作區將重新顯示，並列出新資料流。

## 後續步驟

本指南介紹了如何管理資料收集UI中的資料流。 有關如何在設定資料流後安裝和配置Web SDK的詳細資訊，請參閱 [資料收集E2E指南](../../collection/e2e.md#install)。
