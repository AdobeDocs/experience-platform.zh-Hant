---
keywords: target個人化；目的地；experience platform target目的地；adobe target目的地；
title: Adobe Target連線
description: Adobe Target應用程式可在跨網站、行動應用程式等處的所有傳入客戶互動中提供即時的AI支援個人化和實驗功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 15%

---

# Adobe Target連線 {#adobe-target-connection}

## 目的地變更記錄檔 {#changelog}

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2024 年 1 月 | 功能和檔案更新。 | 您現在可以為預設的生產沙箱和其他非預設沙箱將受眾和設定檔屬性共用到Adobe Target連線。 |
| 2023 年 6 月 | 功能和檔案更新 | 自2023年6月起，當您設定新的Adobe Target目的地連線時，可以選取您要共用對象的Adobe Target工作區。 如需詳細資訊，請參閱「[連線參數](#parameters)」一節。另外，如需有關工作區的詳細資訊，請參閱 Adobe Target 中有關[設定工作區](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=zh-Hant)的教學課程。 |
| 2023 年 5 月 | 功能和檔案更新 | 截至2023年5月， **[!UICONTROL Adobe Target]** 連線支援 [屬性型個人化](../../ui/activate-edge-personalization-destinations.md#map-attributes) 並且通常可供所有客戶使用。 |

{style="table-layout:auto"}

## 概觀 {#overview}

Adobe Target應用程式可在跨網站、行動應用程式等處的所有傳入客戶互動中提供即時的AI支援個人化和實驗功能。

Adobe Target是Adobe Experience Platform目標目錄中的個人化連線。

## 影片概述 {#video-overview}

如需如何在Experience Platform中設定Adobe Target連線的簡短概觀，請觀看下方的影片。

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## 先決條件 {#prerequisites}

### 資料串流ID {#datastream-id}

將Adobe Target連線設定為時 [使用資料串流ID](#parameters)，您必須擁有 [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) 已實作。

在不使用資料串流ID的情況下設定Adobe Target連線，不需要您實作Web SDK。

>[!IMPORTANT]
>
>建立之前 [!DNL Adobe Target] connection，閱讀操作指南 [設定相同頁面和下一頁個人化的個人化目的地](../../ui/activate-edge-personalization-destinations.md). 本指南會針對跨多個Experience Platform元件的相同頁面和下一頁個人化使用案例，引導您進行所需設定步驟。 若要實現相同頁面和下一頁個人化使用案例，在設定Adobe Target連線時，您必須使用資料串流ID。

### Adobe Target的必要條件 {#prerequisites-in-adobe-target}

在Adobe Target中，確定您的使用者具有：

* 存取 [預設工作區](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace)；
* 此 **核准者** [角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

閱讀更多有關授與許可權的資訊 [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 和 [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | X | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!DNL Profile request]** | 您正在請求已對應至Adobe Target目的地的所有受眾，以獲得單一設定檔。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="關於資料流 ID"
>abstract="此選項會確定哪個資料集合資料流中將包含對象。下拉選單僅顯示已啟用目標設定的資料流。若要使用邊緣分段，您必須選取一個資料流 ID。選取不停用所有使用邊緣分段的使用案例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=zh-Hant#parameters" text="了解有關選取資料流的詳細資訊"

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

Adobe Experience Platform會自動連線至貴公司的Adobe Target執行個體。 不需要驗證。

### 連線參數 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="關於 Adobe Target 工作區"
>abstract="選取將共用對象的 Adobe Target 工作區。您可以為每個 Adobe Target 連線選取一個工作區。啟動後，對象將被導向到選取的工作區，同時依循適用的 Experience Platform 資料使用標籤。"
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=zh-Hant" text="進一步了解 Adobe Target 工作區"

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **名稱**：填寫此目的地的偏好名稱。
* **說明**：輸入目的地的說明。 例如，您可以提及要將此目的地用於哪個行銷活動。 此欄位為選用。
* **資料串流ID**：這會決定要將對象包含在哪個資料收集資料串流中。 下拉式功能表只會顯示已啟用Target和Adobe Experience Platform服務的資料串流。 另請參閱 [設定資料串流](../../../datastreams/configure.md#aep) 以取得如何為Adobe Experience Platform和Adobe Target設定資料流的詳細資訊。
   * **[!UICONTROL 無]**：如果您需要設定Adobe Target個人化，但無法實施 [Experience PlatformWeb SDK](/help/web-sdk/home.md). 使用此選項時，從Experience Platform匯出至Target的受眾僅支援下一次工作階段個人化，且會停用邊緣細分。 如需詳細資訊，請參閱下表。

  | Adobe Target實施（不含Web SDK） | Web SDK實作 |
  |---|---|
  | <ul><li>資料流不是必要專案。 Adobe Target可透過以下方式部署： [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html)， [伺服器端](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation)，或 [混合式](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) 實作方法。</li><li>[邊緣細分](../../../segmentation/ui/edge-segmentation.md) 不受支援。</li><li>[相同頁面和下一頁個人化](../../ui/activate-edge-personalization-destinations.md) 不受支援。</li><li>您可以將對象和設定檔屬性共用至Adobe Target連線，用於 *預設生產沙箱* 以及非預設的沙箱。</li><li>若要在不使用資料流ID的情況下設定下一個工作階段個人化，請使用 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>需要具有Adobe Target和Experience Platform設定為服務的資料流。</li><li>邊緣細分如預期運作。</li><li>[相同頁面和下一頁個人化](../../ui/activate-edge-personalization-destinations.md) 支援。</li><li>支援從其他沙箱共用對象和設定檔屬性。</li></ul> |

* **工作區**：選取Adobe Target [工作區](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=zh-Hant) 對象將共用的目標。 您可以為每個 Adobe Target 連線選取一個工作區。啟用後，在遵循適用的同時，會將對象路由到選取的工作區 [Experience Platform資料使用標籤](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>針對使用自訂Target工作區時 [使用屬性的相同頁面和下一頁個人化](../../ui/activate-edge-personalization-destinations.md)，僅限 [選取的對象](../../ui/activate-edge-personalization-destinations.md#select-audiences) 會傳送至選取的Target工作區。 此 [對應的屬性](../../ui/activate-edge-personalization-destinations.md#mapping) 會傳送至預設的Target工作區。
><br>
>此行為將在未來的更新中變更。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [啟用對象以邊緣個人化目的地](../../ui/activate-edge-personalization-destinations.md) 以取得啟用此目的地對象的指示。

## 匯出的資料 {#exported-data}

Adobe Target *讀取* 來自Adobe Experience Platform Edge Network的設定檔資料，因此不會匯出任何資料。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).
