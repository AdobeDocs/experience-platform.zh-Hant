---
title: 啟用受眾以串流設定檔匯出目的地
type: Tutorial
description: 瞭解如何透過將受眾傳送至串流設定檔型目的地，以啟用您在Adobe Experience Platform中的受眾資料。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 3e2dc51e768d6bcfeedbc26e04997dc46c852e4d
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---


# 啟用受眾以串流設定檔匯出目的地

>[!IMPORTANT]
> 
> * 若要啟用資料並啟用 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> * 若要在不透過 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用區段而不進行對應]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> 
> 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

## 概觀 {#overview}

本文說明在Adobe Experience Platform中啟用受眾資料至串流設定檔目的地所需的工作流程(也稱為 [企業目的地](/help/destinations/destination-types.md#streaming-profile-export))。

本文適用於下列三個目的地：

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Azure事件中樞](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [HTTP API目的地](/help/destinations/catalog/streaming/http-destination.md).

## 先決條件 {#prerequisites}

若要啟用目的地的資料，您必須已成功 [已連線至目的地](./connect-destination.md). 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。

## 選取您的目的地 {#select-destination}

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![顯示目的地目錄索引標籤的影像。](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 選取 **[!UICONTROL 啟用對象]** 位於您要啟用對象之目的地的對應卡片上，如下圖所示。

   ![在目的地目錄標籤中反白啟用對象控制項的影像。](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. 選取您要用來啟用對象的目的地連線，然後選取「 」 **[!UICONTROL 下一個]**.

   ![此影像顯示您可以連線到的兩個目的地的選取範圍。](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移至下一個區段至 [選取您的對象](#select-audiences).

## 選取您的對象 {#select-audiences}

若要選取您要啟用至目的地的對象，請使用對象名稱左邊的核取方塊，然後選取「 」 **[!UICONTROL 下一個]**.

您可以根據對象的來源，從多種對象型別中進行選取：

* **[!UICONTROL 分段服務]**：細分服務在Experience Platform中產生的對象。 請參閱 [細分檔案](../../segmentation/ui/overview.md) 以取得更多詳細資料。
* **[!UICONTROL 自訂上傳]**：在Experience Platform外部產生的對象，並以CSV檔案的形式上傳至Platform。 若要深入瞭解外部對象，請參閱以下檔案： [匯入對象](../../segmentation/ui/overview.md#import-audience).
* 其他型別的對象，源自其他Adobe解決方案，例如 [!DNL Audience Manager].

![在啟動工作流程的「選取對象」步驟中，反白核取方塊選取範圍的影像。](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## 選取設定檔屬性 {#select-attributes}

在 **[!UICONTROL 對應]** 步驟，選取您要傳送至目標目的地的設定檔屬性。

1. 在 **[!UICONTROL 選取屬性]** 頁面，選取 **[!UICONTROL 新增欄位]**.

   ![在對應步驟中反白新增欄位控制項的影像。](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 選取右側的箭頭 **[!UICONTROL 結構描述欄位]** 登入點。

   ![在對應步驟中反白如何選取來源欄位的影像。](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在 **[!UICONTROL 選取欄位]** 頁面上，選取您要傳送至目的地的XDM屬性，然後選擇 **[!UICONTROL 選取]**.

   ![顯示可選取作為來源欄位的一系列XDM欄位的影像。](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. 若要新增更多欄位，請重複步驟1至3，然後選取「 」 **[!UICONTROL 下一個]**.

## 請檢閱 {#review}

在 **[!UICONTROL 檢閱]** 頁面中，您可以看到選取範圍的摘要。 選取 **[!UICONTROL 取消]** 若要分解流量， **[!UICONTROL 返回]** 以修改您的設定，或 **[!UICONTROL 完成]** 以確認您的選取範圍並開始傳送資料至目的地。

![稽核步驟中的選取範圍摘要。](../assets/ui/activate-streaming-profile-destinations/review.png)

### 同意原則評估 {#consent-policy-evaluation}

[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 目前不支援匯出至三個企業目的地：Amazon Kinesis、Azure事件中樞和HTTP API。

這表示未同意成為目標的設定檔 *包含* 匯出至這三個目的地的資料中。

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### 資料使用原則檢查 {#data-usage-policy-checks}

在 **[!UICONTROL 檢閱]** 步驟，Experience Platform也會檢查是否有任何資料使用原則違規。 以下是違反原則的範例。 在解決違規之前，您無法完成對象啟用工作流程。 如需有關如何解決原則違規的資訊，請參閱 [資料使用原則違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) 資料控管檔案區段中的。

![資料原則違規](../assets/common/data-policy-violation.png)

### 篩選對象 {#filter-audiences}

此外，在此步驟中，您可以使用頁面上的可用篩選器，只顯示其排程或對應已隨著此工作流程而更新的對象。

![熒幕錄製，顯示稽核步驟中可用的對象篩選器。](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

如果您對您的選取感到滿意，並且未偵測到任何原則違規，請選取 **[!UICONTROL 完成]** 以確認您的選取範圍並開始傳送資料至目的地。

## 驗證受眾啟用 {#verify}

您的匯出 [!DNL Experience Platform] 資料會以JSON格式登陸至您的目標目的地。 例如，下列事件包含符合特定對象資格並退出其他對象之設定檔的電子郵件地址屬性。 此潛在客戶的身分是 `ECID` 和 `email_lc_sha256`.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
