---
title: 對目的地啟用帳戶對象
type: Tutorial
description: 瞭解如何對目的地啟用帳戶對象
badgeLimitedAvailability: label="可用性限制" type="Caution"
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: bf4a34a0fbf59571eaea3ccbc619f9fe17d5c218
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 啟用帳戶對象

>[!AVAILABILITY]
>
>對目的地啟用帳戶對象的功能僅適用於 [Real-time Customer Data Platform的B2B版本](../../rtcdp/b2b-overview.md). 此外，帳戶對象功能目前正在 **可用性限制**. 請聯絡Adobe客戶服務或您的Adobe代表，以要求存取此功能。

本文會說明匯出所需的工作流程 [帳戶對象](/help/segmentation/ui/account-audiences.md) 從Adobe Experience Platform前往您偏好的目的地。

## 支援的目的地 {#supported-destinations}

前往 **[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。 使用 **[!UICONTROL 資料型別]** 篩選並選取 **[!UICONTROL 帳戶]** 檢視支援啟用帳戶對象的目的地。 目前，匯出帳戶對象僅適用於特定雲端儲存空間目的地([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)， [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md)， [Azure Blob儲存體](/help/destinations/catalog/cloud-storage/azure-blob.md)， [資料登陸區域](/help/destinations/catalog/cloud-storage/data-landing-zone.md)、和 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md))和 [（公司） LinkedIn相符的受眾](/help/destinations/catalog/social/linkedin.md) 目的地。

![支援帳戶對象的目的地。](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## 先決條件 {#prerequisites}

* 您必須先內嵌 [帳戶設定檔](/help/rtcdp/accounts/account-profile-overview.md) 和建立 [帳戶對象](/help/segmentation/ui/account-audiences.md) 才能啟用至下游目的地。
* 若要將帳戶對象啟用至目的地，您必須已成功連線至目的地。 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。 閱讀UI教學課程，位於 [連線到目的地](./connect-destination.md) 以取得詳細資訊。

### 必要權限 {#permissions}

若要啟用帳戶對象，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

為確保您擁有啟動帳戶對象的必要許可權，請瀏覽目的地目錄。 如果目的地有 **[!UICONTROL 啟動]** 控制項，則表示您擁有適當的許可權。

## 選取您的目的地 {#select-destination}

依照指示選取可匯出資料集的目的地：

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![反白顯示目錄控制項的目的地目錄標籤。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 選取 **[!UICONTROL 啟動]** 位於對應您要匯出資料集之目的地的卡片上。

>[!TIP]
>
>可匯出帳戶對象的目的地會在卡片的右上角顯示圖示，類似於下方醒目提示的目的地，或者，您可以使用資料型別篩選器來僅顯示可匯出帳戶對象的目的地，如下所示 [顯示在頁面較高的位置](#supported-destinations).

![可匯出醒目提示之設定檔對象的Amazon S3目標頁面。](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. 選取 **[!UICONTROL 資料型別帳戶]**，然後選取您要匯出資料集的目的地連線 **[!UICONTROL 下一個]**.

>[!TIP]
> 
>如果您想要設定新的目的地以啟用帳戶對象，請選取「 」 **[!UICONTROL 設定新目的地]** 以觸發 [連線到目的地](/help/destinations/ui/connect-destination.md) 工作流程和 [選取帳戶作為資料型別](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![標示帳戶控制項的目的地啟用工作流程。](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. 繼續下一節至 [選取您的帳戶對象](#select-profile-audiences) 以匯出。

## 選取您的帳戶對象 {#select-account-audiences}

使用帳戶對象名稱左側的核取方塊來選取您要匯出至目的地的對象，然後選取「 」 **[!UICONTROL 下一個]**. 請注意，僅 *帳戶對象* 會顯示在此檢視中，不會顯示其他對象型別。

![資料集匯出工作流程顯示「選取對象」步驟，您可在此選取要匯出的帳戶對象。](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## 排程和後續步驟

若要進行其餘的啟動工作流程以匯出帳戶對象，請閱讀有關將資料啟動至檔案型目的地的教學課程。 繼續從 [排程對象匯出步驟](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). 如果您要將帳戶對象啟用至 **[!UICONTROL （公司） LinkedIn相符的受眾]** 目的地，請閱讀啟用串流目的地的教學課程。 繼續從 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>請注意，在排程步驟中，將帳戶對象匯出至雲端儲存空間目的地時，啟用帳戶對象的工作流程僅允許您匯出 [完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _依每日排程_. 不支援每小時匯出。 另請注意 **[!UICONTROL 對象評估後]** 是唯一支援的評估型別。

## 重要圖說文字和已知限制 {#important-callouts-known-limitations}

請注意下列重要圖說和已知限制，瞭解啟用帳戶對象功能的有限可用性版本。

### 將帳戶對象啟用至時，需在對映步驟中選取對映 **[!UICONTROL （公司） LinkedIn相符的受眾]** 目的地 {#required-mappings}

將帳戶對象啟用至 **[!UICONTROL （公司） LinkedIn相符的受眾]** 目的地，請注意，若要成功匯出資料，下列兩個對應配對為必要專案：

![linkedIn對應必要欄位。](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 來源欄位 | 目標欄位 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (在「 」中選取此欄位 **[!UICONTROL 選取身分名稱空間]** 檢視) |

### 資料治理實施 {#data-governance-enforcement}

[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 目前不支援將帳戶對象啟用到目的地。 在啟動工作流程的稽核步驟中，您可以看到控制項呈現灰色 **[!UICONTROL 檢視適用的同意政策]**.

![啟用帳戶對象工作流程的稽核步驟，同意執行控制項顯示為灰色。](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Real-Time CDP中的其他資料治理機制，例如 [資料使用原則檢查](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 和 [基於屬性的存取控制](/help/destinations/home.md#attribute-based-access) 支援。
