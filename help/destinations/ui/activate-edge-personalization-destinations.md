---
title: 啟用對象以邊緣個人化目的地
description: 瞭解如何針對相同頁面和下一頁個人化使用案例，從Adobe Experience Platform啟用對象至邊緣個人化目的地。
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 25697d341b2970eeb20d9f2507ee701ade8046d3
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 2%

---


# 啟用對象以邊緣個人化目的地

## 概觀 {#overview}

Adobe Experience Platform使用[edge segmentation](../../segmentation/methods/edge-segmentation.md)搭配[edge destinations](/help/destinations/destination-types.md#edge-personalization-destinations)讓客戶能夠即時建立並鎖定大規模對象。 此功能可協助您設定相同頁面和下一頁個人化使用案例。

邊緣目的地的範例是[Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)和[自訂個人化](../../destinations/catalog/personalization/custom-personalization.md)連線。

>[!NOTE]
>
>當[使用資料流ID設定Adobe Target連線](../catalog/personalization/adobe-target-connection.md) *而非*&#x200B;時，不支援本文中所述的使用案例。 在沒有資料流的情況下，僅支援下一次工作階段個人化使用案例。

>[!IMPORTANT]
> 
> * 若要啟用資料並啟用工作流程的[對應步驟](#mapping)，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;以及&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。
> * 若要在不進行工作流程的[對應步驟](#mapping)的情況下啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用沒有對應的區段]**、**[!UICONTROL 檢視設定檔]**&#x200B;以及&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}
> 
> 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

本文說明在Adobe Experience Platform邊緣目的地啟用對象所需的工作流程。 在搭配[邊緣區段](../../segmentation/methods/edge-segmentation.md)和選用的[設定檔屬性對應](#mapping)一起使用時，這些目的地會在您的網頁和行動屬性上啟用相同頁面和下一頁個人化使用案例。

如需如何設定Adobe Target連線以進行Edge Personalization的簡短概覽，請觀看下方的影片。

>[!NOTE]
>
>Experience Platform使用者介面經常更新，自從錄製此影片後，可能已經變更。 如需最新資訊，請參閱以下章節所述的設定步驟。

>[!VIDEO](https://video.tv.adobe.com/v/3449804/?quality=12&learn=on&captions=chi_hant)

如需如何將對象和設定檔屬性共用至Adobe Target和自訂個人化目的地的簡短概觀，請觀看以下影片。

>[!VIDEO](https://video.tv.adobe.com/v/3447366/?quality=12&learn=on&captions=chi_hant)

## 使用案例 {#use-cases}

使用Adobe個人化解決方案(例如Adobe Target)或您自己的個人化合作夥伴平台（例如，[!DNL Optimizely]、[!DNL Pega]），以及專屬系統(例如內部CMS)，透過[自訂Personalization](../catalog/personalization/custom-personalization.md)目的地提供更深入的客戶個人化體驗。 同時利用Experience Platform Edge Network資料收集和細分功能。

下述使用案例包含網站個人化及鎖定網站上的目標廣告。

若要啟用這些使用案例，客戶需要以快速、簡化的方式從Experience Platform擷取對象和設定檔屬性資訊，並將此資訊傳送至Experience Platform UI中的[Adobe Target](../catalog/personalization/adobe-target-connection.md)或[自訂Personalization](../catalog/personalization/custom-personalization.md)連線。

### 相同頁面個人化 {#same-page}

使用者造訪您網站的頁面。 您可以使用目前的頁面瀏覽資訊（例如反向連結URL、瀏覽器語言、內嵌的產品資訊），針對非Adobe平台（例如，[!DNL Pega]、[!DNL Optimizely]或其他）使用[自訂個人化](../catalog/personalization/custom-personalization.md)連線，來選取下一個動作或決定（例如個人化）。

### 下一頁個人化 {#next-page}

使用者造訪您網站上的頁面A。 根據此互動，使用者已符合一組對象的資格。 接著，使用者按一下連結，系統就會將使用者從頁面A帶往頁面B。使用者在頁面A上先前互動期間符合資格的對象，以及目前網站造訪決定的設定檔更新，將用於支援下一個動作或決定（例如，要向訪客顯示的廣告橫幅，或在A/B測試的情況下，要顯示的頁面版本）。

### 下一次工作階段個人化 {#next-session}

使用者造訪您網站上的數個頁面。 根據這些互動，使用者已符合一組對象的資格。 然後，使用者會終止目前的瀏覽工作階段。

次日，使用者回到相同的客戶網站。 他們之前與所有造訪的網站頁面互動期間符合資格的對象，以及目前網站造訪決定的設定檔更新，將用於選取下一個動作/決定（例如，要向訪客顯示哪個廣告橫幅，或者，在A/B測試的情況下，要顯示哪個頁面版本）。

### 個人化首頁橫幅 {#home-page-banner}

一家住家租賃和銷售公司想要根據Adobe Experience Platform中的對象資格，以橫幅來個人化他們的首頁。 公司可以選取應該獲得個人化體驗的對象，並將這些對象傳送至Adobe Target，作為其Target選件的鎖定目標條件。

## 先決條件 {#prerequisites}

### 在資料收集UI中設定資料串流 {#configure-datastream}

設定個人化目的地的第一個步驟，是為Experience Platform Web SDK設定資料流。 這是在資料收集UI中完成。

設定資料串流時，在&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;底下，確定已選取&#x200B;**[!UICONTROL Edge分段]**&#x200B;和&#x200B;**[!UICONTROL Personalization目的地]**。

>[!TIP]
>
>從2024年4月發行版本開始，在[設定與Edge的連線](/help/destinations/catalog/personalization/adobe-target-connection.md)時，您不需要選取「Adobe Target分段」核取方塊。 在這種情況下，[下一個工作階段個人化](#next-session)是唯一可用的個人化使用案例。

![Edge細分和Personalization目的地醒目提示的資料流設定！](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

如需如何設定資料串流的詳細資訊，請依照[Experience Platform Web SDK檔案](../../datastreams/configure.md#aep)中所述的指示操作。

### 建立[!DNL Active-On-Edge]合併原則 {#create-merge-policy}

建立目的地連線之後，您必須建立[!DNL Active-On-Edge]合併原則。 [!DNL Active-On-Edge]合併原則可確保在Edge[&#128279;](../../segmentation/methods/edge-segmentation.md)上持續評估對象，並可用於即時和下一頁個人化使用案例。

>[!IMPORTANT]
>
>目前，邊緣目的地僅支援啟用使用[Edge上主動合併原則](../../segmentation/ui/segment-builder.md#merge-policies)設定為預設的受眾。 如果您將使用不同合併原則的對象對應至邊緣目的地，則不會評估這些對象。

依照[建立合併原則](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)上的指示進行，並確定啟用&#x200B;**[!UICONTROL Edge上主動式合併原則]**&#x200B;切換按鈕。

### 在Experience Platform中建立新受眾 {#create-audience}

建立[!DNL Active-On-Edge]合併原則後，您必須在Experience Platform中建立新的對象。

依照[對象產生器](../../segmentation/ui/segment-builder.md)指南建立新對象，並確定[將您在上一步建立的[!DNL Active-On-Edge]合併原則指派給它](../../segmentation/ui/segment-builder.md#merge-policies)。

### 建立目的地連線 {#connect-destination}

設定資料流後，您就可以開始設定個人化目的地。

請依照[目的地連線建立教學課程](../ui/connect-destination.md)中的指示進行，以取得有關如何建立新目的地連線的詳細說明。

根據您設定的目的地，請參閱下列文章以取得目的地特定先決條件及相關資訊：

* [Adobe Target連線](../catalog/personalization/adobe-target-connection.md#parameters)
* [自訂個人化連線](../catalog/personalization/custom-personalization.md#parameters)

## 選取您的目的地 {#select-destination}

完成必要條件後，您現在可以選取要用於相同頁面和下一頁個人化的邊緣個人化目的地。

1. 移至&#x200B;**[!UICONTROL 連線>目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   在Experience Platform UI中反白顯示![目的地目錄索引標籤。](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. 在您想要啟用對象的個人化目的地對應卡片上，選取「**[!UICONTROL 啟用對象]**」，如下圖所示。

   ![在目錄中的目的地卡上反白顯示啟用對象控制項。](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. 選取您想要用來啟用對象的目的地連線，然後選取[下一步] **&#x200B;**。

   ![在啟動工作流程中選取目的地步驟。](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. 移至下一個區段以[選取您的對象](#select-audiences)。

## 選取您的對象 {#select-audiences}

使用對象名稱左邊的核取方塊來選取您要啟用至目的地的對象，然後選取&#x200B;**[!UICONTROL 下一步]**。

若要選取您要啟用至目的地的對象，請使用對象名稱左邊的核取方塊，然後選取&#x200B;**[!UICONTROL 下一步]**。

您可以根據對象的來源，從多種對象型別中進行選取：

* **[!UICONTROL 細分服務]**：細分服務在Experience Platform中產生的對象。 如需詳細資訊，請參閱[分段檔案](../../segmentation/ui/overview.md)。
* **[!UICONTROL 自訂上傳]**：對象是在Experience Platform外部產生，並以CSV檔案形式上傳至Experience Platform。 若要深入瞭解外部對象，請參閱有關[匯入對象](../../segmentation/ui/audience-portal.md#import-audience)的檔案。
* 其他型別的對象，源自其他Adobe解決方案，例如[!DNL Audience Manager]。

![選取啟用工作流程的對象步驟，並反白數個對象。](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## 對應屬性 {#mapping}

>[!IMPORTANT]
>
>設定檔屬性可能包含敏感資料。 為了保護此資料，**[!UICONTROL 自訂Personalization]**&#x200B;目的地在設定以屬性為基礎的個人化目的地時，需要您使用[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)。 所有Edge Network API呼叫都必須在[已驗證的內容](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/)中進行。
>
><br>如果您已使用Web SDK或Mobile SDK進行整合，您可以新增伺服器端整合，透過Edge Network API擷取屬性。
>
><br>如果您未遵循上述要求，個人化將僅以對象成員資格為基礎。

選取您想要根據其為使用者啟用個人化使用案例的屬性。 這表示，如果屬性的值變更或已將屬性新增至設定檔，則該設定檔將成為對象的成員，並將啟動至個人化目的地。

新增屬性為選用，您仍可繼續進行下一個步驟，並在不選取屬性的情況下啟用相同頁面和下一頁個人化。 如果您未在此步驟中新增任何屬性，仍會根據設定檔的對象成員資格和身分對應資格進行個人化。

![影像顯示已選取屬性的對應步驟。](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### 選取來源屬性 {#select-source-attributes}

若要新增來源屬性，請在&#x200B;**[!UICONTROL Source欄位]**&#x200B;欄位上選取&#x200B;**[!UICONTROL 新增欄位]**&#x200B;控制項，然後搜尋或導覽至您想要的XDM屬性欄位，如下所示。

![熒幕錄製，顯示如何在對應步驟中選取目標屬性。](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### 選取目標屬性 {#select-target-attributes}

若要新增目標屬性，請選取&#x200B;**[!UICONTROL 目標欄位]**&#x200B;欄位上的&#x200B;**[!UICONTROL 新增欄位]**&#x200B;控制項，並輸入您要對應來源屬性的自訂屬性名稱。

>[!NOTE]
>
>目標屬性的選取僅適用於[自訂Personalization](../catalog/personalization/custom-personalization.md)啟動工作流程，以支援目的地平台中的好記名稱欄位對應。

![顯示如何在對應步驟](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)中選取XDM屬性的熒幕錄製

## 排程對象匯出 {#scheduling}

依預設，[!UICONTROL 對象排程]頁面僅顯示您目前啟用流程中選擇的新選取對象。

若要檢視所有啟用至您目的地的對象，請使用篩選選項並停用&#x200B;**[!UICONTROL 僅顯示新對象]**&#x200B;篩選器。

![所有對象篩選器皆強調顯示。](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

在&#x200B;**[!UICONTROL 對象排程]**&#x200B;頁面上，選取每個對象，然後使用&#x200B;**[!UICONTROL 開始日期]**&#x200B;和&#x200B;**[!UICONTROL 結束日期]**&#x200B;選取器來設定傳送資料至目的地的時間間隔。

![啟動工作流程中強調開始和結束日期的對象排程步驟。](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以移至[!UICONTROL 檢閱]頁面。

## 審核 {#review}

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;頁面上，您可以看到選取專案的摘要。 選取&#x200B;**[!UICONTROL 取消]**&#x200B;以中斷流程，**[!UICONTROL 上一步]**&#x200B;以修改您的設定，或選取&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始傳送資料到目的地。

![檢閱步驟中的選擇摘要。](../assets/ui/activate-edge-personalization-destinations/review.png)

### 同意原則評估 {#consent-policy-evaluation}

如果您的組織購買了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，請選取&#x200B;**[!UICONTROL 檢視適用的同意原則]**，以查看套用了哪些同意原則以及由於這些原則啟動中包含了多少個設定檔。如需詳細資訊，請參閱[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。

### 資料使用原則檢查 {#data-usage-policy-checks}

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;步驟中，Experience Platform也會檢查是否有任何資料使用原則違規。 以下是違反原則的範例。 在解決違規之前，您無法完成對象啟用工作流程。 如需有關如何解決原則違規的資訊，請參閱資料治理檔案一節中的關於[資料使用原則違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation)。

![資料原則違規的範例。](../assets/common/data-policy-violation.png)

### 篩選對象 {#filter-audiences}

在此步驟中，您可以使用頁面上的可用篩選器來僅顯示其排程或對應已隨著此工作流程而更新的對象。 您也可以切換要檢視的表格欄。

![熒幕錄製，顯示稽核步驟中可用的對象篩選器。](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

如果您對您的選擇感到滿意，並且未偵測到任何原則違規，請選取[完成] **[!UICONTROL 以確認您的選擇，並開始將資料傳送到目的地。]**

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
