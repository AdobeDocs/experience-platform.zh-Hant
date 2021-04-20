---
keywords: IP位址、IP範圍、允許清單目的地、允許清單
title: 'IP位址允許雲端儲存目標清單 '
type: Documentation
description: 此頁提供可添加到允許清單的IP範圍，以安全地將資料從Experience Platform導出到SFTP伺服器、AmazonS3或Azure Blob儲存。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
translation-type: tm+mt
source-git-commit: ac62ebcc7b00a96f718a3c39725bcf21ce3d56cf
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# IP位址允許雲端儲存空間目標清單{#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建議您將此頁面設為書籤，每三個月重新造訪一次，以檢查最新的IP位址。 Adobe不提供新IP範圍的通知。
> * 雖然Adobe支援將資料匯出至SFTP伺服器，但建議的雲端儲存位置會是[!DNL Amazon S3]和[!DNL Azure Blob]。


## 概述 {#overview}

本頁提供可添加到允許清單的IP範圍，以安全地將資料從Experience Platform導出到[SFTP伺服器](./sftp.md)、[AmazonS3](./amazon-s3.md)或[Azure Blob](./azure-blob.md)儲存。

您可以通過網路防火牆定義網路訪問控制。 通過指定適當的IP範圍，您可以允許資料傳輸服務的通信。

Adobe建議您在使用雲端儲存空間目標連線之前，先將下列IP範圍新增至允許清單。 若無法將您地區專屬的IP範圍新增至您的允許清單，在使用雲端儲存區目的地連線時，可能會導致錯誤或效能不佳。

## 所有客戶都需要

* `52.247.108.70`

## 美國客戶

* `52.252.71.64/29`

## EMEA客戶

* `51.137.8.208/29`

## 亞太地區客戶

* `20.53.201.168/29`
