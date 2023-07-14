---
title: 啟用對象以邊緣個人化目的地
description: 瞭解如何針對相同頁面和下一頁個人化使用案例，從Adobe Experience Platform啟用對象至邊緣個人化目的地。
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 37819b5a6480923686d327e30b1111ea29ae71da
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 2%

---


# 啟用對象以邊緣個人化目的地

## 概觀 {#overview}

Adobe Experience Platform使用 [邊緣細分](../../segmentation/ui/edge-segmentation.md) 搭配edge目的地，讓客戶可即時大規模建立及鎖定對象。 此功能可協助您設定相同頁面和下一頁個人化使用案例。

邊緣目的地的範例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化](../../destinations/catalog/personalization/custom-personalization.md) 連線。

>[!NOTE]
>
>時間 [設定Adobe Target連線](../catalog/personalization/adobe-target-connection.md) 若不使用資料串流ID，即不支援本文所述的使用案例。 在沒有資料流的情況下，僅支援下一次工作階段個人化使用案例。

>[!IMPORTANT]
> 
> * 若要啟用資料並啟用 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> * 若要在不透過 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用區段而不進行對應]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> 
> 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

本文說明在Adobe Experience Platform Edge目的地啟用對象所需的工作流程。 搭配使用時 [邊緣細分](../../segmentation/ui/edge-segmentation.md) 和選填 [設定檔屬性對應](#mapping)，這些目的地會在您的網頁和行動屬性上啟用相同頁面和下一頁個人化使用案例。

如需如何設定Adobe Target連線以進行Edge個人化的簡短概觀，請觀看以下影片。

>[!NOTE]
>
>Experience Platform使用者介面經常更新，自從錄製此影片後，可能有所變更。 如需最新資訊，請參閱以下章節中所述的設定步驟。

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

如需如何將對象和設定檔屬性共用至Adobe Target和自訂個人化目的地的簡短概觀，請觀看以下影片。

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## 使用案例 {#use-cases}

邊緣個人化目的地可讓您使用Adobe個人化解決方案(例如Adobe Target)或您自己的個人化合作夥伴平台(例如 [!DNL Optimizely]， [!DNL Pega])，以及專屬系統（例如內部CMS），透過提供更深入的客戶個人化體驗 [自訂個人化](../catalog/personalization/custom-personalization.md) 目的地。 同時運用Experience Platform Edge Network的資料收集與細分功能。

以下說明的使用案例包含網站個人化和目標網站上的廣告。

若要啟用這些使用案例，客戶需要一種快速且簡化的方式，從Experience Platform中擷取對象和設定檔屬性資訊，並將此資訊傳送至以下任一項： [Adobe Target](../catalog/personalization/adobe-target-connection.md) 或 [自訂個人化](../catalog/personalization/custom-personalization.md) Experience PlatformUI中的連線。

### 同一頁面的個人化 {#same-page}

使用者造訪您網站的某個頁面。 客戶可使用目前的頁面瀏覽資訊（例如反向連結URL、瀏覽器語言、內嵌的產品資訊）來選取下一個動作/決定（例如個人化），方法為 [自訂個人化](../catalog/personalization/custom-personalization.md) 非Adobe平台的連線(例如， [!DNL Pega]， [!DNL Optimizely]、等)。

### 下一頁個人化 {#next-page}

使用者造訪您網站上的頁面A。 根據此互動，使用者已符合一組對象的資格。 然後，使用者按一下連結，該連結會將使用者從頁面A帶往頁面B。使用者在頁面A上先前互動期間符合資格的對象，加上目前網站造訪決定的設定檔更新，將用於支援下一個動作/決定（例如，要向訪客顯示哪個廣告橫幅，或在A/B測試的情況下，要顯示哪個頁面版本）。

### 下一個工作階段的個人化 {#next-session}

使用者造訪您網站上的數個頁面。 根據這些互動，使用者已符合一組對象的資格。 然後，使用者會終止目前的瀏覽工作階段。

第二天，使用者返回相同的客戶網站。 他們之前與所有造訪的網站頁面互動期間符合資格的受眾，加上目前網站造訪決定的設定檔更新，將用於選取下一個動作/決定（例如，要向訪客顯示哪個廣告橫幅，或在A/B測試的情況下，要顯示哪個頁面版本）。

### 個人化首頁橫幅 {#home-page-banner}

一家家用租賃和銷售公司想要根據Adobe Experience Platform中的受眾資格，以橫幅來個人化他們的首頁。 公司可以選取應該讓哪些對象獲得個人化體驗，並將這些對象傳送到Adobe Target，作為其Target選件的鎖定目標條件。

## 先決條件 {#prerequisites}

### 在資料收集UI中設定資料串流 {#configure-datastream}

設定個人化目的地的第一個步驟，是為Experience PlatformWeb SDK設定資料流。 這可在資料收集UI中完成。

設定資料串流時，在 **[!UICONTROL Adobe Experience Platform]** 請確定兩者 **[!UICONTROL 邊緣細分]** 和 **[!UICONTROL 個人化目的地]** 已選取。

![資料流設定](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

如需如何設定資料串流的詳細資訊，請依照 [Platform Web SDK檔案](../../edge/datastreams/configure.md#aep).

### 建立 [!DNL Active-On-Edge] 合併原則 {#create-merge-policy}

建立目的地連線後，您必須建立 [!DNL Active-On-Edge] 合併原則。 此 [!DNL Active-On-Edge] 合併原則可確保持續評估對象 [在邊緣](../../segmentation/ui/edge-segmentation.md) 和適用於即時和下一頁個人化使用案例。

>[!IMPORTANT]
>
>目前，邊緣目的地僅支援啟用使用 [主動邊緣合併原則](../../segmentation/ui/segment-builder.md#merge-policies) 設定為預設值。 如果您將使用不同合併原則的對象對應至邊緣目的地，則不會評估這些對象。

請依照以下說明操作： [建立合併原則](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)，並確保啟用 **[!UICONTROL Active-On-Edge合併原則]** 切換。

### 在Platform中建立新對象 {#create-audience}

在您建立 [!DNL Active-On-Edge] 合併原則，您必須在Platform中建立新的對象。

請遵循 [對象產生器](../../segmentation/ui/segment-builder.md) 指南來建立您的新對象，並確保 [指派它](../../segmentation/ui/segment-builder.md#merge-policies) 此 [!DNL Active-On-Edge] 您在步驟3建立的合併原則。

### 建立目的地連線 {#connect-destination}

設定資料串流後，您就可以開始設定個人化目的地。

請遵循 [目的地連線建立教學課程](../ui/connect-destination.md) 以取得有關如何建立新目的地連線的詳細說明。

根據您設定的目的地，請參閱下列文章以取得目的地特定先決條件及相關資訊：

* [Adobe Target連線](../catalog/personalization/adobe-target-connection.md#parameters)
* [自訂個人化連線](../catalog/personalization/custom-personalization.md##parameters)

## 選取您的目的地 {#select-destination}

完成必要條件後，您現在可以選取邊緣個人化目的地，以用於相同頁面和下一頁個人化。

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![目的地目錄標籤](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. 選取 **[!UICONTROL 啟用對象]** 在您想要啟用對象之個人化目的地的對應卡片上，如下圖所示。

   ![啟動按鈕](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. 選取您要用來啟用對象的目的地連線，然後選取 **[!UICONTROL 下一個]**.

   ![選取目的地](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. 移至下一區段至 [選取您的對象](#select-audiences).

## 選取您的對象 {#select-audiences}

使用對象名稱左側的核取方塊來選取您要啟用至目的地的對象，然後選取「 」 **[!UICONTROL 下一個]**.

若要選取您想要啟用至目的地的對象，請使用對象名稱左邊的核取方塊，然後選取 **[!UICONTROL 下一個]**.

您可以根據對象的來源，從多種對象型別中進行選取：

* **[!UICONTROL 細分服務]**：細分服務在Experience Platform中產生的對象。 請參閱 [細分檔案](../../segmentation/ui/overview.md) 以取得更多詳細資料。
* **[!UICONTROL 自訂上傳]**：在Experience Platform外部產生的對象，並以CSV檔案的形式上傳至Platform。 若要進一步瞭解外部對象，請參閱以下檔案： [匯入對象](../../segmentation/ui/overview.md#import-audience).
* 其他型別的對象，源自其他Adobe解決方案，例如 [!DNL Audience Manager].

![選取對象](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## 對應屬性 {#mapping}

>[!IMPORTANT]
>
>設定檔屬性可能包含敏感資料。 為了保護此資料， **[!UICONTROL 自訂個人化]** 目的地要求您使用 [Edge Network Server API](../../server-api/overview.md) 設定屬性型個人化的目的地時。 所有伺服器API呼叫都必須在 [已驗證的內容](../../server-api/authentication.md).
>
><br>如果您已在使用Web SDK或Mobile SDK進行整合，您可以透過新增伺服器端整合來透過伺服器API擷取屬性。
>
><br>如果您未遵循上述要求，個人化將僅以對象成員資格為基礎。

選取您想要根據為使用者啟用個人化使用案例的屬性。 這表示如果屬性的值變更或將屬性新增至設定檔，則該設定檔將成為對象的成員，並將啟動至個人化目的地。

新增屬性為選用，您仍可繼續進行下一個步驟，並在不選取屬性的情況下啟用相同頁面和下一頁個人化。 如果您未在此步驟中新增任何屬性，仍會根據設定檔的對象成員資格和身分對應資格進行個人化。

![顯示已選取屬性之對應步驟的影像](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### 選取來源屬性 {#select-source-attributes}

若要新增來源屬性，請選取 **[!UICONTROL 新增欄位]** 控制 **[!UICONTROL 來源欄位]** 欄並搜尋或導覽至您所需的XDM屬性欄位，如下所示。

![顯示如何在對應步驟中選取目標屬性的熒幕錄製](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### 選取目標屬性 {#select-target-attributes}

若要新增目標屬性，請選取 **[!UICONTROL 新增欄位]** 控制 **[!UICONTROL 目標欄位]** 欄並輸入您要對應來源屬性的自訂屬性名稱。

>[!NOTE]
>
>目標屬性的選取範圍僅適用於 [自訂個人化](../catalog/personalization/custom-personalization.md) 啟用工作流程，以便在目的地平台中支援易記名稱欄位對應。

![熒幕錄製，顯示如何在對應步驟中選取XDM屬性](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## 排程對象匯出 {#scheduling}

根據預設， [!UICONTROL 對象排程] 頁面僅顯示您在目前啟用流程中選擇的新選取對象。

若要檢視所有正在啟用至您的目的地的對象，請使用篩選選項並停用 **[!UICONTROL 僅顯示新對象]** 篩選。

![所有對象](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

於 **[!UICONTROL 對象排程]** 頁面，選取每個對象，然後使用 **[!UICONTROL 開始日期]** 和 **[!UICONTROL 結束日期]** 選取器，設定傳送資料至目的地的時間間隔。

![對象排程](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

選取 **[!UICONTROL 下一個]** 前往 [!UICONTROL 檢閱] 頁面。

## 請檢閱 {#review}

於 **[!UICONTROL 檢閱]** 頁面中，您可以看到選取範圍的摘要。 選取 **[!UICONTROL 取消]** 若要分解流量， **[!UICONTROL 返回]** 修改您的設定，或 **[!UICONTROL 完成]** 以確認您的選擇並開始傳送資料至目的地。

![稽核步驟中的選取專案摘要。](../assets/ui/activate-edge-personalization-destinations/review.png)

### 同意原則評估 {#consent-policy-evaluation}

如果您的組織購買了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，請選取&#x200B;**[!UICONTROL 檢視適用的同意原則]**，以查看套用了哪些同意原則以及由於這些原則啟動中包含了多少個設定檔。閱讀關於 [同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 以取得詳細資訊。

### 資料使用原則檢查 {#data-usage-policy-checks}

在 **[!UICONTROL 檢閱]** 步驟，Experience Platform也會檢查是否有任何資料使用原則違規。 以下是違反原則的範例。 在解決違規之前，您無法完成對象啟用工作流程。 如需有關如何解決原則違規的資訊，請閱讀關於 [資料使用原則違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) （位於資料控管檔案區段）。

![資料原則違規](../assets/common/data-policy-violation.png)

### 篩選對象 {#filter-audiences}

在此步驟中，您可以使用頁面上的可用篩選器來僅顯示其排程或對應已隨著此工作流程而更新的對象。 您也可以切換要檢視的表格欄。

![熒幕錄製，顯示稽核步驟中可用的對象篩選器。](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

如果您對您的選擇感到滿意，並且未偵測到任何原則違規，請選取 **[!UICONTROL 完成]** 以確認您的選擇並開始傳送資料至目的地。

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
