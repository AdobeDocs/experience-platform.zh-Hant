---
title: 對目的地啟用帳戶對象
type: Tutorial
description: 瞭解如何對目的地啟用帳戶對象
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 1c31dd978298191dd10500b60eb446d2ca37139c
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# 啟用帳戶對象

>[!AVAILABILITY]
>
>購買[企業對企業](/help/rtcdp/overview.md#rtcdp-b2b)和[企業對個人](/help/rtcdp/overview.md#rtcdp-b2p)版Real-time Customer Data Platform的公司可以使用啟用帳戶對象到目的地的功能。

本文說明從Adobe Experience Platform將[帳戶對象](/help/segmentation/ui/account-audiences.md)匯出至您偏好的目的地所需的工作流程。

## 支援的目的地 {#supported-destinations}

移至&#x200B;**[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。 使用&#x200B;**[!UICONTROL 資料型別]**&#x200B;篩選器並選取&#x200B;**[!UICONTROL 帳戶]**，檢視支援啟用帳戶對象的目的地。 目前，匯出帳戶對象僅適用於特定雲端儲存空間目的地([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)、[ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md)、[Azure Blob儲存空間](/help/destinations/catalog/cloud-storage/azure-blob.md)、[資料登陸區域](/help/destinations/catalog/cloud-storage/data-landing-zone.md)和[SFTP](/help/destinations/catalog/cloud-storage/sftp.md))以及[Demandbase](/help/destinations/catalog/advertising/demandbase.md)和[（公司） LinkedIn相符的對象](/help/destinations/catalog/social/linkedin-b2b.md)串流目的地。

![支援帳戶對象的目的地。](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## 影片概觀

請觀看下方的影片，概略瞭解如何建立和啟用帳戶對象，以及啟用帳戶對象時支援的使用案例。

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## 先決條件 {#prerequisites}

* 您必須先內嵌[帳戶設定檔](/help/rtcdp/accounts/account-profile-overview.md)並建立[帳戶對象](/help/segmentation/ui/account-audiences.md)，才能將其啟動至下游目的地。
* 若要將帳戶對象啟用至目的地，您必須已成功連線至目的地。 如果您尚未這麼做，請前往[目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。 如需詳細資訊，請參閱[連線到目的地](./connect-destination.md)的UI教學課程。

### 必要權限 {#permissions}

若要啟用帳戶對象，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 啟用目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

為確保您擁有啟動帳戶對象的必要許可權，請瀏覽目的地目錄。 如果目的地有&#x200B;**[!UICONTROL 啟用]**&#x200B;控制項，則表示您擁有適當的許可權。

## 選取您的目的地 {#select-destination}

依照指示選取可匯出資料集的目的地：

1. 移至&#x200B;**[!UICONTROL 連線>目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   ![目錄控制項反白顯示的目的地目錄標籤。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 在對應您要匯出資料集之目的地的卡片上，選取&#x200B;**[!UICONTROL 啟動]**。

>[!TIP]
>
>可匯出帳戶對象的目的地會在卡片的右上角標示圖示，類似於下面醒目提示的目的地，或者，您可以使用資料型別篩選器來只顯示可匯出帳戶對象的目的地，如頁面上較高的[所示](#supported-destinations)。

![可匯出醒目提示之設定檔對象的Demandbase目的地頁面。](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. 選取&#x200B;**[!UICONTROL 資料型別帳戶]**，接著選取您要匯出資料集的目的地連線，然後選取&#x200B;**[!UICONTROL 下一步]**。

>[!TIP]
> 
>如果您想要設定新的目的地以啟用帳戶對象，請選取&#x200B;**[!UICONTROL 設定新的目的地]**&#x200B;以觸發[連線到目的地](/help/destinations/ui/connect-destination.md)工作流程，並[選取帳戶作為資料型別](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports)。

![帳戶控制項反白顯示的目的地啟用工作流程。](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. 繼續下一節至[選取要匯出的帳戶對象](#select-profile-audiences)。

## 選取您的帳戶對象 {#select-account-audiences}

使用帳戶對象名稱左側的核取方塊來選取您要匯出至目的地的對象，然後選取&#x200B;**[!UICONTROL 下一步]**。 請注意，此檢視中只會顯示&#x200B;*帳戶對象*，不會顯示其他對象型別。

![資料集匯出工作流程顯示「選取對象」步驟，您可以在此選取要匯出的帳戶對象。](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## 排程和後續步驟

若要進行其餘的啟動工作流程以匯出帳戶對象，請閱讀有關將資料啟動至檔案型目的地的教學課程。 從[排程對象匯出步驟](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)繼續。 如果您要啟用帳戶對象至&#x200B;**[!UICONTROL （公司） LinkedIn相符對象]**&#x200B;目的地，請閱讀啟用串流目的地的教學課程。 從[對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)繼續。

>[!NOTE]
>
>請注意，將帳戶對象匯出至雲端儲存空間目的地時，在排程步驟中，啟用帳戶對象的工作流程僅允許您依每日排程&#x200B;_匯出[完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)_。 不支援每小時匯出。 另請注意，**[!UICONTROL 對象評估之後]**&#x200B;是唯一支援的評估型別。

## 重要圖說文字和已知限制 {#important-callouts-known-limitations}

請注意下列重要圖說和已知限制，瞭解啟用帳戶對象功能的一般可用性版本。

### 將帳戶對象啟用至&#x200B;**[!UICONTROL （公司） LinkedIn相符對象]**&#x200B;目的地時，在對應步驟中需要對應的配對 {#required-mappings}

將帳戶對象啟用至&#x200B;**[!UICONTROL （公司） LinkedIn Matched Audiences]**&#x200B;目的地時，請注意，若要成功匯出資料，必須有下列兩個對應配對：

![LinkedIn對應必要欄位。](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 來源欄位 | 目標欄位 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` （選取&#x200B;**[!UICONTROL 目標欄位]**&#x200B;時，在&#x200B;**[!UICONTROL 選取身分識別名稱空間]**&#x200B;檢視中選取此欄位）。<br> ![選取工作流程中反白的身分名稱空間，以啟用帳戶的對象到目的地。](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的帳戶對象。"){width="100" zoomable="yes"} |

### 資料治理實施 {#data-governance-enforcement}

*客戶和潛在客戶對象*&#x200B;的同意是在人員或設定檔層級強制執行。 因此，在啟用帳戶對象到目的地時，目前不支援[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。 在啟用工作流程的檢閱步驟中，您可以看到&#x200B;**[!UICONTROL 檢視適用的同意原則]**&#x200B;的控制項顯示為灰色。

![啟用帳戶對象工作流程的稽核步驟，同意執行控制項顯示為灰色。](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

支援Real-Time CDP中的其他資料治理機制，例如[資料使用原則檢查](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)和[屬性型存取控制](/help/destinations/home.md#attribute-based-access)。
