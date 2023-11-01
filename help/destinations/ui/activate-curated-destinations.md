---
title: 根據LiveRamp識別碼將受眾啟用至已組織的目的地
type: Tutorial
description: 瞭解如何使用LiveRamp RampID從Adobe Experience Platform啟用對象至連線的電視和音訊目的地，以及其他整合。
source-git-commit: 25cda72508860b57bfa9ad0a729d0329d0f6bd1f
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---


# 根據LiveRamp識別碼將受眾啟用至已組織的目的地

將Adobe Real-Time CDP整合用於 [!DNL LiveRamp] 若要啟用受眾至使用的精選目的地清單 [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) 進行啟用，包括連線電視和音訊目的地，例如下列目的地。

>[!IMPORTANT]
>
>您不需要在Experience Platform介面中擷取或以任何方式使用LiveRamp RampID。
>
> 如官方檔案所述，您可以從Real-Time CDP匯出身分識別，例如PII型識別碼、已知識別碼和自訂ID [LiveRamp檔案](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). 然後，這些身分將和 [!DNL LiveRamp RampIDs] 啟動流程的下游。


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

透過進行兩個步驟的程式並使用 [LiveRamp — 入門](../catalog/advertising/liveramp-onboarding.md) 和 [LiveRamp — 分佈](../catalog/advertising/liveramp-distribution.md) 目的地，如下圖所示。

![此圖表顯示透過LiveRamp將受眾從Real-Time CDP啟用至已組織目的地的工作流程。](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

首先，您將對象從Real-Time CDP匯出至 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 目的地（以CSV檔案形式）。

匯出對象後，您可使用 [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) 目的地。

>[!TIP]
>
>此程式可讓您對目的地（例如）啟用對象。 [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku)， [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)，以及更多功能，直接從Real-Time CDP UI存取，而不需登入 [!DNL LiveRamp] 啟用帳戶。

### 步驟1：透過，將您的對象從Experience Platform傳送至LiveRamp。 [!DNL LiveRamp - Onboarding] 目的地 {#onboarding}

為了將您的對象啟用至根據LiveRamp RampIDs的已組織目的地，您必須先執行下列動作： **將您的對象從Experience Platform匯出至[!DNL LiveRamp]**.

若要這麼做，請使用 **[!DNL LiveRamp - Onboarding]** 目的地。

![顯示LiveRamp — 入門目的地卡片的Experience PlatformUI影像](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

若要瞭解如何設定 [!DNL LiveRamp - Onboarding] 目的地並從Experience Platform匯出您的對象，請閱讀 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 目的地檔案。

>[!IMPORTANT]
>
>將檔案匯出至 [!DNL LiveRamp - Onboarding] 目的地，Platform會為每個目的地產生一個CSV檔案 [合併原則ID](../../profile/merge-policies/overview.md). 請參閱 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 目的地檔案，以取得有關如何驗證資料匯出至LiveRamp的詳細資訊。


成功將對象匯出至LiveRamp後，請繼續 [步驟2](#distribution).

>[!TIP]
>
>移至之前 [步驟2](#distribution)， [驗證](../catalog/advertising/liveramp-onboarding.md#exported-data) 您的對象已成功匯出至LiveRamp。 請參閱以下檔案： [監視目的地資料流](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 並閱讀的特定監視詳細資訊 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### 步驟2：透過「 」，將已上線的對象啟動至已連線的電視和音訊目的地。 [!DNL LiveRamp - Distribution] 目的地 {#distribution}

在您擁有 [已驗證](../catalog/advertising/liveramp-onboarding.md#exported-data) 您的對象已成功匯出至LiveRamp，是時候將對象啟動至您偏好的目的地，例如 [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku)， [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)、等等。

您啟動對象(匯出於 [步驟1](#onboarding))藉由使用 **[!DNL LiveRamp - Distribution]** 目的地。

![顯示LiveRamp — 發佈目的地卡片的Experience PlatformUI影像](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

若要瞭解如何設定 **[!DNL LiveRamp - Distribution]** 目的地並啟用您匯出的對象 [步驟1](#onboarding)，閱讀 [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) 目的地檔案。

>[!IMPORTANT]
>
>在 **對象選擇** 的步驟 **[!DNL LiveRamp - Distribution]** 目的地，您必須選取 *完全相同的對象* 您已匯出至 [LiveRamp — 入門](../catalog/advertising/liveramp-onboarding.md) 目的地位於 [步驟1](#onboarding).

當您設定 **[!DNL LiveRamp - Distribution]** 目的地，您必須針對要使用的每個下游目的地（Roku、Disney等）建立專用連線。

>[!TIP]
>
>為目的地命名時，Adobe建議遵循以下格式： `LiveRamp - Downstream Destination Name`. 此命名模式可協助您快速識別 [瀏覽](../ui/destinations-workspace.md#browse) 目的地工作區的索引標籤。
><br>
>範例：`LiveRamp - Roku`。

![顯示多個LiveRamp目的地的平台UI熒幕擷圖。](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

驗證將對象成功匯出至 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 目的地，請參閱以下檔案： [監視目的地資料流](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 並閱讀的特定監視詳細資訊 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

若要驗證您的對象是否成功啟用至您選擇的廣告平台（例如Roku、Disney及其他），請登入您的目的地平台帳戶並檢查啟用量度。
