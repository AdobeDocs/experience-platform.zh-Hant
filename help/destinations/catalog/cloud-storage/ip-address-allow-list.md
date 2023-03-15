---
keywords: IP位址、IP範圍、允許清單目的地、允許清單
title: 雲端儲存目的地的IP位址允許清單
type: Documentation
description: 此頁面提供可新增至允許清單的IP範圍，以安全地將資料從Experience Platform匯出至SFTP伺服器、Amazon S3或Azure Blob儲存。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 雲端儲存目的地的IP位址允許清單 {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建議您將此頁面加入書籤，並每三個月重新造訪一次，以檢查最新的IP位址。 Adobe不提供新IP範圍的通知。
> * 雖然Adobe支援將資料匯出至SFTP伺服器，但建議的雲端儲存空間位置會匯出資料 [!DNL Amazon S3] 和 [!DNL Azure Blob].


## 總覽 {#overview}

此頁面提供可新增至允許清單的IP範圍，以安全地將資料從Experience Platform匯出至 [SFTP伺服器](./sftp.md).

您可以通過網路防火牆定義網路訪問控制。 通過指定適當的IP範圍，可以允許資料傳輸服務的通信。

Adobe建議您在處理雲端儲存目標連線之前，先將下列IP範圍新增至允許清單。 若未將您地區專屬的IP範圍新增至允許清單，在使用雲端儲存目的地連線時，可能會導致錯誤或效能不佳。

## 所有客戶都需要

* `52.247.108.70`

## 美國客戶

* `52.252.71.64/29`

## EMEA客戶

* `51.137.8.208/29`

## APAC客戶

* `20.53.201.168/29`
