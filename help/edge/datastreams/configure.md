---
title: 設定資料流
description: 連接您的客戶端 Experience Platform SDK 與 Adobe 產品和協力廠商目標的整合。
source-git-commit: 82703fae72e8637bb7d5e08a6699d9e1466afd8b
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 3%

---

# 設定資料流

本檔案說明設定 [資料流](./overview.md) 在UI中。

## 存取 [!UICONTROL 資料流] 工作區

您可以在資料收集UI或Experience PlatformUI中，透過選取 **[!UICONTROL 資料流]** 的下一頁。

![資料收集UI中的「資料流」索引標籤](../assets/datastreams/configure/datastreams-tab.png)

此 [!UICONTROL 資料流] 索引標籤會顯示現有資料流的清單，包括其易記名稱、ID和上次修改日期。 選取資料流的名稱 [查看其詳細資訊並配置服務](#view-details).

選取「更多」圖示(**...**)以顯示更多選項。 選擇 **[!UICONTROL 編輯]** 更新 [基本配置](#configure) ，或選取 **[!UICONTROL 刪除]** 移除資料流。

![編輯或刪除現有資料流的選項](../assets/datastreams/configure/edit-datastream.png)

## 建立新資料流 {#create}

若要建立資料流，請從選取 **[!UICONTROL 新資料流]**.

![選擇新資料流](../assets/datastreams/configure/new-datastream-button.png)

從設定步驟開始，資料流建立工作流程隨即顯示。 您必須在此提供資料流的名稱和可選說明。

如果您要設定此資料流以用於Experience Platform，且使用Platform Web SDK，您也必須選取 [事件型Experience Data Model(XDM)結構](../../xdm/classes/experienceevent.md) 來表示您計畫擷取的資料。

![資料流的基本配置](../assets/datastreams/configure/configure.png)

選擇 **[!UICONTROL 進階選項]** 以顯示設定資料流的其他控制項。

![進階設定選項](../assets/datastreams/configure/advanced-options.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 地理位置] | 根據用戶的IP地址確定GPS查找是否發生。 預設設定 **[!UICONTROL 無]** 會停用任何GPS查閱，而 **[!UICONTROL 城市]** 設定可提供兩位小數的GPS座標。 |
| [!UICONTROL 第一方ID Cookie] | 啟用後，此設定會在查詢 [第一方裝置ID](../identity/first-party-device-ids.md)，而非在「身分對應」中查詢此值。<br><br>啟用此設定時，您必須提供預期會儲存ID之Cookie的名稱。 |
| [!UICONTROL 第三方ID同步] | ID同步可分組為容器，以便在不同時間執行不同的ID同步。 啟用後，此設定可讓您指定要為此資料流執行哪個ID同步容器。 |
| [!UICONTROL 存取類型] | 定義邊緣網路接受的資料流的驗證類型。 <ul><li>**[!UICONTROL 混合驗證]**:選取此選項時，邊緣網路會接受已驗證和未驗證的請求。 當您打算使用Web SDK時，請選取此選項，或 [行動SDK](https://aep-sdks.gitbook.io/docs/)，連同 [伺服器API](../../server-api/overview.md). </li><li>**[!UICONTROL 僅驗證]**:選取此選項時，邊緣網路僅接受已驗證的請求。 當您打算只使用伺服器API，並想要防止邊緣網路處理任何未驗證的請求時，請選取此選項。</li></ul> |

若要在此設定資料流以供Experience Platform，請依照 [資料收集的資料準備](./data-prep.md) 若要先將資料對應至Platform事件結構，再返回本指南。 否則，請選取 **[!UICONTROL 儲存]** 並繼續下一節。

## 檢視資料流詳細資訊 {#view-details}

設定新資料流或選取要檢視的現有資料流後，該資料流的詳細資訊頁面隨即顯示。 您可在這裡找到資料流的詳細資訊，包括其ID。

![已建立資料流的詳細資訊頁面](../assets/datastreams/configure/view-details.png)

從資料流詳細資訊螢幕，您可以 [新增服務](#add-services) 若要從您可存取的Adobe Experience Cloud產品啟用功能。 您也可以編輯資料流的 [基本配置](#create)，更新 [對應規則](./data-prep.md), [複製資料流](#copy)，或將其完全刪除。

## 新增服務至資料流 {#add-services}

在資料流的詳細資訊頁面上，選取 **[!UICONTROL 添加服務]** 開始為該資料流添加可用服務。

![選擇添加服務以繼續](../assets/datastreams/configure/add-service.png)

在下一個畫面中，使用下拉式選單來選取要針對此資料流設定的服務。 只有您有權存取的服務才會顯示在此清單中。

![從清單中選擇服務](../assets/datastreams/configure/service-selection.png)

選取所需的服務，填入顯示的設定選項，然後選取 **[!UICONTROL 儲存]** 將服務新增至資料流。 所有新增的服務都會顯示在資料流的詳細資訊檢視中。

![新增至資料流的服務](../assets/datastreams/configure/services-added.png)

以下子節說明每個服務的設定選項。

>[!NOTE]
>
>每個服務配置都包含 **[!UICONTROL 已啟用]** 切換選取服務時自動啟用的選項。 若要停用此資料流的所選服務，請選取 **[!UICONTROL 已啟用]** 切換。

### Adobe Analytics設定 {#analytics}

此服務會控制資料是否以及如何傳送至Adobe Analytics。 如需其他詳細資訊，請參閱 [傳送資料至Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics設定區塊](../assets/datastreams/configure/analytics-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 報告套裝 ID] | **（必要）** 您要傳送資料的目的地Analytics報表套裝ID。 此ID可在Adobe Analytics UI的 [!UICONTROL 管理] > [!UICONTROL 報表套裝]. 若指定多個報表套裝，則資料會複製到每個報表套裝。 |

### Adobe Audience Manager設定 {#audience-manager}

此服務會控制資料是否以及如何傳送至Adobe Audience Manager。 將資料傳送至Audience Manager所需的全部是啟用此區段。 其他設定為選用，但建議使用。

![Adobe對象管理設定區塊](../assets/datastreams/configure/audience-manager-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL Cookie目的地已啟用] | 允許SDK透過共用區段資訊 [cookie目的地](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 從 [!DNL Audience Manager]. |
| [!UICONTROL 已啟用URL目的地] | 允許SDK透過共用區段資訊 [URL目的地](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) 從 [!DNL Audience Manager]. |

### Adobe Experience Platform設定 {#aep}

>[!IMPORTANT]
>
>為Platform啟用資料流時，請記下您目前使用的Platform沙箱，如UI頂端功能區所示。
>
>![所選沙箱](../assets/datastreams/configure/platform-sandbox.png)
>
>沙箱是Adobe Experience Platform中的虛擬分區，可讓您將資料和實施與組織中的其他項目隔離開來。 建立資料流後，其沙箱便無法變更。 如需沙箱在Experience Platform中角色的詳細資訊，請參閱 [沙箱檔案](../../sandboxes/home.md).

此服務會控制資料是否以及如何傳送至Adobe Experience Platform。

![Adobe Experience Platform設定區塊](../assets/datastreams/configure/platform-config.png)

| 設定 | 說明 |
|---| --- |
| [!UICONTROL 事件資料集] | **（必要）** 選取客戶事件資料要串流至的Platform資料集。 此架構必須使用 [XDM ExperienceEvent類別](../../xdm/classes/experienceevent.md). |
| [!UICONTROL 設定檔資料集] | 選取客戶屬性資料要傳送至的Platform資料集。 此架構必須使用 [XDM個別設定檔類別](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | 選取此核取方塊以啟用Platform Web SDK實作的Offer decisioning。 請參閱 [搭配Platform Web SDK使用Offer decisioning](../personalization/offer-decisioning/offer-decisioning-overview.md) 以取得更多實作詳細資訊。<br><br>如需Offer decisioning功能的詳細資訊，請參閱 [Adobe Journey Optimizer檔案](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=zh-Hant). |
| [!UICONTROL 邊緣分割] | 選中此複選框以啟用 [邊緣分割](../../segmentation/ui/edge-segmentation.md) 資料流。 當SDK透過啟用邊緣分段的資料流傳送資料時，回應中會傳回相關設定檔的任何更新區段成員資格。<br><br>此選項可與 [!UICONTROL 個人化目的地] for [下一頁個人化使用案例](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL 個人化目的地] | 若在啟用 [!UICONTROL 邊緣分割] 核取方塊，此選項可讓資料流連線至個人化目的地，例如 [自訂個人化](../../destinations/catalog/personalization/custom-personalization.md).<br><br>如需的特定步驟，請參閱目的地檔案 [設定個人化目的地](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Adobe Journey Optimizer] | 選中此複選框以啟用 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) 資料流。 <br><br> 啟用此選項可讓資料流從以下的網頁和應用程式為基礎的傳入促銷活動，傳回個人化內容： [!DNL Adobe Journey Optimizer]. 此選項需要 [!UICONTROL 邊緣分割] 活動。 若 [!UICONTROL 邊緣分割] 未勾選，此選項會反灰。 |

### Adobe Target設定 {#target}

此服務會控制資料是否以及如何傳送至Adobe Target。

![Adobe Target設定區塊](../assets/datastreams/configure/target-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 屬性代號] | [!DNL Target] 可讓客戶透過使用屬性來控制權限。 如需屬性的詳細資訊，請參閱 [配置企業權限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 在 [!DNL Target] 檔案。<br><br>您可以在Adobe Target UI的下方找到屬性代號 [!UICONTROL 設定] > [!UICONTROL 屬性]. |
| [!UICONTROL 目標環境ID] | [Adobe Target環境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 可協助您管理所有開發階段的實作。 此設定會指定您要與此資料流搭配使用的環境。<br><br>最佳實務是以不同方式為每個 `dev`, `stage`，和 `prod` 資料流環境，讓事情保持簡單。 不過，如果您已定義Adobe Target環境，則可使用這些環境。 |
| [!UICONTROL Target第三方ID命名空間] | 的身分識別命名空間 `mbox3rdPartyId` 您想要用於此資料流。 請參閱 [實施 `mbox3rdPartyId` 與Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md) 以取得更多資訊。 |

### [!UICONTROL 事件轉送] 設定

此服務會控制資料是否及如何傳送至 [事件轉送](../../tags/ui/event-forwarding/overview.md).

![設定UI的「事件轉送」區段](../assets/datastreams/configure/event-forwarding-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL Launch屬性] | **（必要）** 您要將資料傳送至的事件轉送屬性。 |
| [!UICONTROL Launch環境] | **（必要）** 您要傳送資料的目標屬性內的環境。 |

>[!NOTE]
>
>您可以選取 **[!UICONTROL 手動輸入ID]** 輸入屬性和環境名稱，而非使用下拉式功能表。

## 複製資料流 {#copy}

您可以建立現有資料流的復本，並視需要變更其詳細資訊。

>[!NOTE]
>
>資料流只能複製在 [沙箱](../../sandboxes/home.md). 換言之，您無法將資料流從一個沙箱複製到另一個沙箱。

從 [!UICONTROL 資料流] 工作區，選取省略號(**....**)，然後選取 **[!UICONTROL 複製]**.

![顯示 [!UICONTROL 複製] 從資料流清單視圖中選擇的選項](../assets/datastreams/configure/copy-datastream-list.png)

或者，您也可以選取 **[!UICONTROL 複製資料流]** 從指定資料流的詳細資訊檢視。

![顯示 [!UICONTROL 複製] 從資料流詳細資訊檢視中選取的選項](../assets/datastreams/configure/copy-datastream-details.png)

此時會出現確認對話方塊，提示您為要建立的新資料流提供唯一名稱，以及將複製的配置選項的詳細資訊。 準備就緒時，請選取 **[!UICONTROL 複製]**.

![用於複製資料流的確認對話框的影像](../assets/datastreams/configure/copy-datastream-confirm.png)

的主要頁面 [!UICONTROL 資料流] 工作區會重新顯示，並列出新的資料流。

## 後續步驟

本指南說明如何在資料收集UI中管理資料流。 如需設定資料流後如何安裝和設定Web SDK的詳細資訊，請參閱 [資料收集E2E指南](../../collection/e2e.md#install).
