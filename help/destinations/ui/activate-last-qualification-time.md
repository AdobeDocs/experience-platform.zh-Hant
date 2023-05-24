---
title: 在新的測試版雲儲存目標中使用上次鑑定時間XDM屬性
description: 瞭解如何在新的測試版雲儲存目標中使用上次鑑定時間XDM屬性
hidefromtoc: y
hide: y
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 在新的測試版雲儲存目標中使用上次鑑定時間XDM屬性 {#last-qualification-time}

>[!IMPORTANT]
> 
>本頁介紹測試版中的功能。 功能和文檔可能會更改。 如果您想訪問此試用版計畫，請與Adobe代表或客戶服務人員聯繫。

## 先決條件 {#prerequisites}

使用上次資格時間(`lastQualificationTime`)XDM屬性，您必須在 [beta程式](/help/release-notes/2022/october-2022.md#destinations) 使用改進的檔案導出功能並將資料導出到六個 [beta雲儲存](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)。 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)。 [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)。 [[!DNL Data Landing Zon]如](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。 [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)。 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md))。 如果在目錄中看到雲儲存目標的新測試卡，則您將被註冊，如下所示 [!DNL Amazon S3]。

![顯示新AmazonS3測試卡的圖片](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## 如何使用上次限定時間XDM屬性 {#how-to-use}

如果您使用六個新的雲儲存測試連接器之一，則可以使用 [映射步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 激活工作流中建立列的時間戳，該時間戳的最新時間戳為限定段的配置檔案。 這可以幫助您瞭解某些度量或分析使用案例，並讓您更瞭解何時激活某些受眾。

請注意，要添加 `lastQualificationTime` 要導出檔案，當前需要手動插入值 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 到源欄位，如下所示。 也可以編輯目標欄位以 `lastQualificationTime` 或您要為此列命名的任何其他值。 請注意，由於這是測試版功能，因此 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 值在將來可能會改變。

![顯示上次限定時間XDM屬性貼上到映射步驟的螢幕錄制](/help/destinations/ui/last-qualification-time.gif)

## 詳細資訊 {#more-information}

有關將資料激活到基於檔案的目標（包括工作流中的所有步驟和必要的權限）的詳細資訊，請閱讀 [激活基於檔案的目標教程](/help/destinations/ui/activate-batch-profile-destinations.md)。
