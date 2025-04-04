---
title: 啟用受眾以串流設定檔匯出目的地
type: Tutorial
description: 瞭解如何透過將受眾傳送至串流設定檔型目的地，以啟用您在Adobe Experience Platform中的受眾資料。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 1%

---


# 啟用受眾以串流設定檔匯出目的地

>[!IMPORTANT]
> 
> * 若要啟用資料並啟用工作流程的[對應步驟](#mapping)，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;以及&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。
> * 若要在不進行工作流程的[對應步驟](#mapping)的情況下啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用沒有對應的區段]**、**[!UICONTROL 檢視設定檔]**&#x200B;以及&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。
> 
> 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

## 概觀 {#overview}

本文說明在Adobe Experience Platform中啟用受眾資料至串流設定檔型目的地（也稱為[企業目的地](/help/destinations/destination-types.md#advanced-enterprise-destinations)）所需的工作流程。

本文適用於下列三個目的地：

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Azure 事件中樞](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [HTTP API目的地](/help/destinations/catalog/streaming/http-destination.md)。

## 先決條件 {#prerequisites}

若要啟用目的地的資料，您必須已成功[連線到目的地](./connect-destination.md)。 如果您尚未這麼做，請前往[目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。

## 選取您的目的地 {#select-destination}

1. 移至&#x200B;**[!UICONTROL 連線>目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   ![顯示目的地目錄索引標籤的影像。](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 在您要啟用對象之目的地的對應卡片上，選取&#x200B;**[!UICONTROL 啟用對象]**，如下圖所示。

   ![在目的地目錄標籤中反白啟用對象控制項的影像。](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. 選取您想要用來啟用對象的目的地連線，然後選取[下一步] ****。

   ![影像顯示您可以連線到之兩個目的地的選取範圍。](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移至下一個區段以[選取您的對象](#select-audiences)。

## 選取您的對象 {#select-audiences}

若要選取您要啟用至目的地的對象，請使用對象名稱左邊的核取方塊，然後選取&#x200B;**[!UICONTROL 下一步]**。

您可以根據對象的來源，從多種對象型別中進行選取：

* **[!UICONTROL 細分服務]**：細分服務在Experience Platform中產生的對象。 如需詳細資訊，請參閱[Audience Portal檔案](../../segmentation/ui/audience-portal.md)。
* **[!UICONTROL 自訂上傳]**：對象是在Experience Platform外部產生，並以CSV檔案形式上傳至Experience Platform。 若要深入瞭解外部對象，請參閱有關[匯入對象](../../segmentation/ui/audience-portal.md#import-audience)的檔案。
* 其他型別的對象，源自其他Adobe解決方案，例如[!DNL Audience Manager]。

![啟用工作流程的「選取對象」步驟中，反白核取方塊選取專案的影像。](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## 選取設定檔屬性 {#select-attributes}

在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，選取您要傳送至目標目的地的設定檔屬性。

1. 在&#x200B;**[!UICONTROL 選取屬性]**&#x200B;頁面中，選取&#x200B;**[!UICONTROL 新增欄位]**。

   ![影像在對應步驟中醒目提示[新增欄位控制項]。](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 選取&#x200B;**[!UICONTROL 結構描述欄位]**&#x200B;專案右側的箭頭。

   ![在對應步驟中反白顯示如何選取來源欄位的影像。](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在&#x200B;**[!UICONTROL 選取欄位]**&#x200B;頁面中，選取您要傳送至目的地的XDM屬性，然後選擇&#x200B;**[!UICONTROL 選取]**。

   ![影像顯示您可以選取做為來源欄位的一系列XDM欄位。](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. 若要新增更多欄位，請重複步驟1到3，然後選取&#x200B;**[!UICONTROL 下一步]**。

## 審核 {#review}

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;頁面上，您可以看到選取專案的摘要。 選取&#x200B;**[!UICONTROL 取消]**&#x200B;以中斷流程，**[!UICONTROL 上一步]**&#x200B;以修改您的設定，或選取&#x200B;**[!UICONTROL 完成]**&#x200B;以確認您的選擇並開始傳送資料到目的地。

![檢閱步驟中的選擇摘要。](../assets/ui/activate-streaming-profile-destinations/review.png)

### 同意原則評估 {#consent-policy-evaluation}

匯出至三個企業目的地(Amazon Kinesis、Azure事件中樞和HTTP API)時，目前不支援[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。

這表示未同意成為目標&#x200B;*的設定檔會包含在匯出到這三個目的地的內容中*。

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### 資料使用原則檢查 {#data-usage-policy-checks}

在&#x200B;**[!UICONTROL 檢閱]**&#x200B;步驟中，Experience Platform也會檢查是否有任何資料使用原則違規。 以下是違反原則的範例。 在解決違規之前，您無法完成對象啟用工作流程。 如需有關如何解決原則違規的資訊，請參閱資料治理檔案一節中的關於[資料使用原則違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation)。

![資料原則違規](../assets/common/data-policy-violation.png)

### 篩選對象 {#filter-audiences}

此外，在此步驟中，您可以使用頁面上的可用篩選器，只顯示其排程或對應已隨著此工作流程而更新的對象。

![熒幕錄製，顯示稽核步驟中可用的對象篩選器。](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

如果您對您的選擇感到滿意，並且未偵測到任何原則違規，請選取[完成] **[!UICONTROL 以確認您的選擇，並開始將資料傳送到目的地。]**

## 驗證受眾啟用 {#verify}

您匯出的[!DNL Experience Platform]資料以JSON格式登陸至您的目標目的地。 例如，下列事件包含符合特定對象資格並退出其他對象之設定檔的電子郵件地址屬性。 此潛在客戶的身分是`ECID`和`email_lc_sha256`。

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
