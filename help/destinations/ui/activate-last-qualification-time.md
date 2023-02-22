---
title: 在新的測試版雲端儲存目的地中，使用上次限定時間XDM屬性
description: 了解如何在新的測試版雲端儲存目的地中使用上次資格鑑定時間XDM屬性
hidefromtoc: y
hide: y
source-git-commit: 7dd525d8c71cdfb9fb2393181faa3270ad1dc4cc
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 在新的測試版雲端儲存目的地中，使用上次限定時間XDM屬性 {#last-qualification-time}

>[!IMPORTANT]
> 
>本頁面說明測試版的功能。 功能和檔案可能會有所變更。 如果您想要存取此測試版計畫，請連絡您的Adobe代表或客戶服務。

## 先決條件 {#prerequisites}

使用上次資格時間(`lastQualificationTime`)XDM屬性，您必須已註冊 [測試版方案](/help/release-notes/2022/october-2022.md#destinations) 若要使用改良的檔案匯出功能，並將資料匯出至以下六項其中之一： [beta雲端儲存目的地](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md))。 如果您在目錄中看到雲端儲存目的地的新測試版卡，即會註冊，如下所示 [!DNL Amazon S3].

![顯示新Amazon S3測試版卡的影像](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## 如何使用上次限定時間XDM屬性 {#how-to-use}

如果您使用6個新雲端儲存測試版連接器之一，可在 [對應步驟](//help/destinations/ui/activate-batch-profile-destinations.md#mapping) 啟用工作流程中建立欄，且最新時間戳記為符合區段的設定檔時。 這可協助您處理特定測量或分析使用案例，也可讓您更清楚了解何時啟用特定對象。

請注意，若要新增 `lastQualificationTime` 您目前需要手動插入值，才能匯出檔案 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 填入來源欄位，如下所示。 您也可以將目標欄位編輯為 `lastQualificationTime` 或您想要為此欄命名的任何其他值。 請注意，由於這是測試版功能，因此 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 值可能會在未來變更。

![螢幕記錄，顯示上次將XDM屬性貼入對應步驟的資格時間](/help/destinations/ui/last-qualification-time.gif)

## 詳細資訊 {#more-information}

如需將資料啟用至檔案式目的地的詳細資訊，包括工作流程中的所有步驟和必要權限，請參閱 [啟用檔案式目的地教學課程](/help/destinations/ui/activate-batch-profile-destinations.md).