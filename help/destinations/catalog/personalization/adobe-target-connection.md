---
keywords: target個人化；目的地；experience platform target目的地；adobe target目的地；
title: Adobe Target連線
description: Adobe Target應用程式可在跨網站、行動應用程式等處的所有傳入客戶互動中提供即時的AI支援個人化和實驗功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 9%

---

# Adobe Target連線 {#adobe-target-connection}

## 目的地變更記錄檔 {#changelog}

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2024 年 4 月 | 功能和檔案更新 | 當連線到Target目的地並使用資料串流ID時，您現在不需要&#x200B;*即可啟用邊緣區段的資料串流。*&#x200B;這表示Target目的地將會搭配批次和串流對象運作，不過您可以完成的使用案例會有所不同。 檢視[連線引數](#parameters)區段中的資料表以取得詳細資訊。 |
| 2024 年 1 月 | 功能和檔案更新 | 您現在可以為預設的生產沙箱和其他非預設沙箱將受眾和設定檔屬性共用到Adobe Target連線。 |
| 2023 年 6 月 | 功能和檔案更新 | 自2023年6月起，當您設定新的Adobe Target目的地連線時，可以選取您要共用對象的Adobe Target工作區。 如需詳細資訊，請參閱「[連線參數](#parameters)」一節。另外，如需有關工作區的詳細資訊，請參閱 Adobe Target 中有關[設定工作區](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html)的教學課程。 |
| 2023 年 5 月 | 功能和檔案更新 | 自2023年5月起，**[!UICONTROL Adobe Target]**&#x200B;連線支援[屬性式個人化](../../ui/activate-edge-personalization-destinations.md#map-attributes)，通常可供所有客戶使用。 |

{style="table-layout:auto"}

## 概觀 {#overview}

Adobe Target應用程式可在跨網站、行動應用程式等處的所有傳入客戶互動中提供即時的AI支援個人化和實驗功能。

Adobe Target是Adobe Experience Platform目標目錄中的個人化連線。

## 影片概觀 {#video-overview}

如需如何在Experience Platform中設定Adobe Target連線的簡短概觀，請觀看下方的影片。

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## 根據實施型別的支援使用案例 {#supported-use-cases}

下表根據您的實作型別，顯示支援的Adobe Target目的地使用案例，包含或不包含[網頁SDK](/help/web-sdk/home.md)，以及是否啟用[邊緣細分](/help/segmentation/home.md#edge)。

| Adobe Target實作&#x200B;*不含* Web SDK | Adobe Target實作&#x200B;*搭配*&#x200B;網頁SDK | Adobe Target實作&#x200B;*已關閉*&#x200B;網頁SDK *和*&#x200B;邊緣區段 |
|---|---|---|
| <ul><li>資料流不是必要專案。 可透過[at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html)、[伺服器端](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation)或[混合式](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation)實作方法來部署Adobe Target。</li><li>不支援[Edge分段](../../../segmentation/methods/edge-segmentation.md)。</li><li>不支援[相同頁面和下一頁個人化](../../ui/activate-edge-personalization-destinations.md)。</li><li>您可以針對&#x200B;*預設生產沙箱*&#x200B;和非預設沙箱，將對象和設定檔屬性共用至Adobe Target連線。</li><li>若要在不使用資料串流ID的情況下設定下一個工作階段個人化，請使用[at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html)。</li></ul> | <ul><li>需要設定為服務的Adobe Target和Experience Platform資料流。</li><li>Edge區段如預期運作。</li><li>[支援相同頁面和下一頁個人化](../../ui/activate-edge-personalization-destinations.md#use-cases)。</li><li>支援從其他沙箱共用對象和設定檔屬性。</li></ul> | <ul><li>需要設定為服務的Adobe Target和Experience Platform資料流。</li><li>當[設定資料流](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)時，請勿選取&#x200B;**Edge分段**&#x200B;核取方塊。</li><li>支援[下一個工作階段個人化](../../ui/activate-edge-personalization-destinations.md#next-session)。</li><li>支援從其他沙箱共用對象和設定檔屬性。</li></ul> |


## 先決條件 {#prerequisites}

### 資料串流 ID {#datastream-id}

設定[的Adobe Target連線時，必須使用資料串流ID](#parameters)，您必須實作[Adobe Experience Platform Web SDK](/help/web-sdk/home.md)。

設定Adobe Target連線而不使用資料串流ID，不需要您實作網頁SDK。

>[!IMPORTANT]
>
>在建立[!DNL Adobe Target]連線之前，請先閱讀如何[為相同頁面和下一頁個人化](../../ui/activate-edge-personalization-destinations.md)設定個人化目的地的指南。 本指南會針對跨多個Experience Platform元件的相同頁面和下一頁個人化使用案例，引導您進行所需設定步驟。 若要實現相同頁面和下一頁個人化使用案例，在設定Adobe Target連線時，您必須使用資料串流ID。

### Adobe Target的必要條件 {#prerequisites-in-adobe-target}

在Adobe Target中，確定您的使用者具有：

* 存取[預設工作區](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace)；
* **核准者** [角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions)。

深入瞭解授與[Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80)和[Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions)的許可權。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

>[!IMPORTANT]
>
>針對相同頁面和下一頁個人化使用案例&#x200B;*啟用*&#x200B;邊緣對象時，對象&#x200B;*必須*&#x200B;使用[active-on-edge合併原則](../../../segmentation/ui/segment-builder.md#merge-policies)。 [!DNL active-on-edge]合併原則可確保持續評估邊緣](../../../segmentation/methods/edge-segmentation.md)上的對象[，並可用於即時和下一頁個人化使用案例。  根據實作型別，閱讀關於[所有可用使用案例](#parameter)。
>如果您將使用不同合併原則的邊緣受眾對應至Adobe Target目的地，這些受眾將不會針對即時和下一頁使用案例進行評估。
>依照[建立合併原則](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy)上的指示進行，並確定啟用&#x200B;**[!UICONTROL Edge上主動式合併原則]**&#x200B;切換按鈕。


| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | X | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!DNL Profile request]** | 您正在請求已對應至Adobe Target目的地的所有受眾，以獲得單一設定檔。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="關於資料流 ID"
>abstract="此選項會確定哪個資料集合資料流中將包含對象。下拉選單僅顯示已啟用目標設定的資料流。若要使用邊緣分段，您必須選取一個資料流 ID。選取不停用所有使用邊緣分段的使用案例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="了解有關選取資料流的詳細資訊"

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

Adobe Experience Platform會自動連線至貴公司的Adobe Target執行個體。 不需要驗證。

### 連線參數 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="關於 Adobe Target 工作區"
>abstract="選取將共用對象的 Adobe Target 工作區。您可以為每個 Adobe Target 連線選取一個工作區。啟動後，對象將被導向到選取的工作區，同時依循適用的 Experience Platform 資料使用標籤。"
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html" text="進一步了解 Adobe Target 工作區"

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **名稱**：填寫此目的地的偏好名稱。
* **描述**：輸入目的地的描述。 例如，您可以提及要將此目的地用於哪個行銷活動。 此欄位為選用。
* **資料串流識別碼**：這會決定要將對象包含在哪個資料收集資料串流中。 下拉式功能表只會顯示已啟用Target和Adobe Experience Platform服務的資料串流。 請參閱[設定資料串流](../../../datastreams/configure.md#aep)，以取得如何設定Adobe Experience Platform和Adobe Target的資料串流的詳細資訊。

  >[!IMPORTANT]
  >
  >每個Adobe Target目的地連線的資料串流ID都是唯一的。 您無法在多個Adobe Target目的地連線中使用相同的資料串流ID。
  >如果您需要將相同的對象對應到多個資料流，您必須為每個資料流ID [建立新的目的地連線](../../ui/connect-destination.md)，並完成[對象啟動流程](#activate)。

   * **[!UICONTROL 無]**：如果您需要設定Adobe Target個人化，但無法實作[Experience Platform Web SDK](/help/web-sdk/home.md)，請選取此選項。 使用此選項時，從Experience Platform匯出至Target的受眾僅支援下一次工作階段個人化，且會停用邊緣細分。 請參考[支援的使用案例](#supported-use-cases)區段中的資料表，以比較每個實作型別的可用使用案例。

  | Adobe Target實作&#x200B;*不含* Web SDK | Adobe Target實作&#x200B;*搭配*&#x200B;網頁SDK | Adobe Target實作&#x200B;*已關閉*&#x200B;網頁SDK *和*&#x200B;邊緣區段 |
  |---|---|---|
  | <ul><li>資料流不是必要專案。 可透過[at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html)、[伺服器端](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation)或[混合式](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation)實作方法來部署Adobe Target。</li><li>不支援[Edge分段](../../../segmentation/methods/edge-segmentation.md)。</li><li>不支援[相同頁面和下一頁個人化](../../ui/activate-edge-personalization-destinations.md)。</li><li>您可以針對&#x200B;*預設生產沙箱*&#x200B;和非預設沙箱，將對象和設定檔屬性共用至Adobe Target連線。</li><li>若要在不使用資料串流ID的情況下設定下一個工作階段個人化，請使用[at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html)。</li></ul> | <ul><li>需要設定為服務的Adobe Target和Experience Platform資料流。</li><li>Edge區段如預期運作。</li><li>[支援相同頁面和下一頁個人化](../../ui/activate-edge-personalization-destinations.md#use-cases)。</li><li>支援從其他沙箱共用對象和設定檔屬性。</li></ul> | <ul><li>需要設定為服務的Adobe Target和Experience Platform資料流。</li><li>當[設定資料流](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)時，請勿選取&#x200B;**Edge分段**&#x200B;核取方塊。</li><li>支援[下一個工作階段個人化](../../ui/activate-edge-personalization-destinations.md#next-session)。</li><li>支援從其他沙箱共用對象和設定檔屬性。</li></ul> |

* **Workspace**：選取將與其共用對象的Adobe Target [工作區](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html)。 您可以為每個 Adobe Target 連線選取一個工作區。啟用後，在遵循適用的[Experience Platform資料使用標籤](../../../data-governance/labels/overview.md)時，會將對象路由到選取的工作區。

>[!NOTE]
>
>使用具有屬性](../../ui/activate-edge-personalization-destinations.md)的[相同頁面和下一頁個人化的自訂Target工作區時，只有[選取的對象](../../ui/activate-edge-personalization-destinations.md#select-audiences)會傳送到選取的Target工作區。 [對應的屬性](../../ui/activate-edge-personalization-destinations.md#mapping)會傳送到預設的Target工作區。
><br>
>此行為將在未來的更新中變更。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

閱讀[啟用邊緣個人化目的地的對象](../../ui/activate-edge-personalization-destinations.md)，以取得啟用此目的地對象的指示。

## 從Target目的地移除對象 {#remove}

當受眾已用於Adobe Target [活動](https://experienceleague.adobe.com/en/docs/target/using/activities/activities)時，需要執行額外的步驟，才能從現有Adobe Target連線中移除該受眾。 嘗試從Adobe Target連線中移除對象時，如果Adobe Target活動使用對象，則會導致錯誤。

![Experience Platform UI影像顯示嘗試移除Target活動使用的對象所導致的錯誤。](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

若要在活動中使用對象時，從Target目的地移除對象，您必須先從使用對象的Target活動中移除對象，或完全刪除活動。 然後，您就可以從Target連線中移除對象。

如果活動未使用對象，請移至&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** > **[!UICONTROL 選取目的地資料流]** > **[!UICONTROL 啟用資料]**，選取您要移除的對象，然後選取&#x200B;**[!UICONTROL 移除對象]**。

## 匯出的資料 {#exported-data}

Adobe Target *會從Adobe Experience Platform Edge Network讀取*&#x200B;設定檔資料，因此不會匯出任何資料。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。
