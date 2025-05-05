---
title: 根據LiveRamp識別碼將受眾啟用至已組織的目的地
type: Tutorial
description: 瞭解如何使用LiveRamp RampID從Adobe Experience Platform啟用對象至連線的電視和音訊目的地，以及其他整合。
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# 根據LiveRamp識別碼將受眾啟用至已組織的目的地

使用Adobe Real-Time CDP與[!DNL LiveRamp]的整合，將對象啟用至使用[[!DNL [LiveRamp RampID]]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html)啟用的精選目的地清單，包括連線電視和音訊目的地，例如下列目的地。

>[!IMPORTANT]
>
>您不需要在Experience Platform介面中擷取或以任何方式使用LiveRamp RampID。
>
> 如官方[LiveRamp檔案](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers)所述，您可以從Real-Time CDP匯出身分識別，例如PII型識別碼、已知識別碼和自訂ID。 然後，這些身分會在啟動程式中與下游的[!DNL LiveRamp RampIDs]相符。


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

本文會說明直接從Real-Time CDP UI將受眾從Real-Time CDP啟動至上述目的地所需的工作流程。

## 啟用工作流程 {#workflow}

您透過兩步驟程式，並使用[LiveRamp — 上線](../catalog/advertising/liveramp-onboarding.md)和[LiveRamp — 發佈](../catalog/advertising/liveramp-distribution.md)目的地，將對象啟用至連線的電視和音訊目的地，如下圖所示。

![圖表顯示透過LiveRamp將對象從Real-Time CDP啟用至已組織目的地的工作流程。](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

首先，您將對象從Real-Time CDP匯出至[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)目的地，格式為CSV檔案。

匯出對象後，請使用[[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md)目的地啟用對象。

>[!TIP]
>
>此程式可讓您直接從Real-Time CDP UI啟用您的對象到目的地，例如[[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku)、[[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)等，而不需要登入您的[!DNL LiveRamp]帳戶以進行啟用。

### 教學課程影片 {#video}

觀看以下影片，瞭解本頁面所述工作流程的端對端說明。

>[!VIDEO](https://video.tv.adobe.com/v/3452669?captions=chi_hant)

### 步驟1：透過[!DNL LiveRamp - Onboarding]目的地，將您的對象從Experience Platform傳送至LiveRamp {#onboarding}

若要將您的對象啟用至根據LiveRamp RampID策劃的目的地，您必須先將對象從Experience Platform匯出至&#x200B;**。[!DNL LiveRamp]**

您可以使用&#x200B;**[!DNL LiveRamp - Onboarding]**&#x200B;目的地來執行此動作。

![顯示LiveRamp — 上線目的地卡片的Experience Platform UI影像](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

若要瞭解如何設定[!DNL LiveRamp - Onboarding]目的地並從Experience Platform匯出您的對象，請閱讀[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)目的地檔案。

>[!IMPORTANT]
>
>將檔案匯出至[!DNL LiveRamp - Onboarding]目的地時，Experience Platform會為每個[合併原則ID](../../profile/merge-policies/overview.md)產生一個CSV檔案。 如需如何驗證資料匯出至LiveRamp的詳細資訊，請參閱[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)目的地檔案。


成功將對象匯出至LiveRamp後，請繼續[步驟2](#distribution)。

>[!TIP]
>
>在移至[步驟2](#distribution)之前，[驗證](../catalog/advertising/liveramp-onboarding.md#exported-data)您的對象已成功匯出至LiveRamp。 請參閱有關[監視目的地資料流](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)的檔案，並閱讀[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data)的特定監視詳細資料。

### 步驟2：透過[!DNL LiveRamp - Distribution]目的地，將已上線的對象啟用至連線的電視和音訊目的地 {#distribution}

在您[驗證](../catalog/advertising/liveramp-onboarding.md#exported-data)您的對象已成功匯出至LiveRamp後，您就可以開始啟用對象至您偏好的目的地，例如[[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku)、[[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)等。

您使用&#x200B;**[!DNL LiveRamp - Distribution]**&#x200B;目的地來啟用對象（已在[步驟1](#onboarding)中匯出）。

![顯示LiveRamp — 散發目的地卡片的Experience Platform UI影像](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

若要瞭解如何設定&#x200B;**[!DNL LiveRamp - Distribution]**&#x200B;目的地並啟用您在[步驟1](#onboarding)中匯出的對象，請閱讀[[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md)目的地檔案。

>[!IMPORTANT]
>
>在&#x200B;**[!DNL LiveRamp - Distribution]**&#x200B;目的地的&#x200B;**對象選取**&#x200B;步驟中，您必須選取您已匯出至[步驟1](#onboarding)中的[LiveRamp — 上線](../catalog/advertising/liveramp-onboarding.md)目的地的&#x200B;*完全相同的對象*。

設定&#x200B;**[!DNL LiveRamp - Distribution]**&#x200B;目的地時，您必須針對要使用的每個下游目的地（Roku、Disney等）建立專用連線。

>[!TIP]
>
>為目的地命名時，Adobe建議遵循此格式： `LiveRamp - Downstream Destination Name`。 此命名模式可協助您在目的地工作區的[瀏覽](../ui/destinations-workspace.md#browse)索引標籤中快速識別您的目的地。
><br>
>範例：`LiveRamp - Roku`。

![Experience Platform UI熒幕擷圖顯示多個LiveRamp目的地。](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

若要驗證將您的對象成功匯出至[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)目的地，請參閱[監視目的地資料流](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)的檔案，並閱讀[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data)的特定監視詳細資料。

若要驗證您的對象是否成功啟用至您選擇的廣告平台（例如Roku、Disney及其他），請登入您的目的地平台帳戶並檢查啟用量度。
