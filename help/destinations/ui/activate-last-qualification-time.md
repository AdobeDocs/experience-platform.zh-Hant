---
title: 使用新Beta版雲端儲存空間目的地中的上次資格取得時間XDM屬性
description: 瞭解如何在新的Beta版雲端儲存目的地使用上次資格取得時間XDM屬性
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 7130ac46a7768ea6e71bf73eb970bf2890323d0f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 使用新Beta版雲端儲存空間目的地中的上次資格取得時間XDM屬性 {#last-qualification-time}

>[!IMPORTANT]
> 
>本頁說明測試版的功能。 功能和檔案可能會有所變更。 如果您想要存取此測試版計畫，請聯絡您的Adobe代表或客戶服務。

## 先決條件 {#prerequisites}

使用上次資格取得時間(`lastQualificationTime`) XDM屬性，您必須將資料匯出至下列六個雲端儲存空間目的地之一：

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]è](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## 如何使用最後合格時間XDM屬性 {#how-to-use}

如果您使用以上列出的六個雲端儲存聯結器之一，則可以在中使用最後限定時間XDM屬性 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 啟動工作流程的一部分，以在匯出的檔案中建立欄，且最新時間戳記為設定檔符合區段資格的時間。 這可協助您處理某些測量或分析使用案例，且可讓您更清楚瞭解何時啟用某些對象。

請注意，若要新增 `lastQualificationTime` 在檔案匯出中，您目前需要手動插入值 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 放入來源欄位中，如下所示。 您也可以編輯目標欄位至 `lastQualificationTime` 或您想要為此欄命名的任何其他值。 請注意，由於這是測試版功能，因此的 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 值未來可能會變更。

![熒幕錄製，顯示上次將XDM屬性貼入對應步驟的資格時間](/help/destinations/ui/last-qualification-time.gif)

## 詳細資訊 {#more-information}

如需將資料啟用至檔案型目的地的詳細資訊，包括工作流程中的所有步驟和必要許可權，請參閱 [啟用檔案型目的地教學課程](/help/destinations/ui/activate-batch-profile-destinations.md).
