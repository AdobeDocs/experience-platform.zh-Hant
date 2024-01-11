---
title: IP位址允許清單SFTP目的地
type: Documentation
description: 此頁面提供您可新增至允許清單的IP範圍，以便安全地從Experience Platform將資料匯出至SFTP伺服器。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 52186e03ba2a9d8b105d01ebfcd9be7666bfb6ff
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# SFTP目的地的IP位址允許清單 {#ip-address-allow-list-sftp}

>[!IMPORTANT]
>
> * Adobe建議您將此頁面加入書籤，每三個月重新造訪一次，以檢查最新IP位址。 Adobe不提供新IP範圍的通知。
> * 雖然Adobe支援將資料匯出至SFTP伺服器，但建議匯出資料的雲端儲存位置為 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 概觀 {#overview}

此頁面提供您可新增至允許清單的IP範圍，以便安全地從Experience Platform匯出資料至您的 [SFTP伺服器](./sftp.md).

您可以透過網路防火牆定義網路存取控制。 透過指定適當的IP範圍，您可以允許資料傳輸服務的流量。

Adobe建議在使用雲端儲存空間目的地連線之前，將下列IP範圍新增至允許清單。 使用雲端儲存空間目的地連線時，如果無法將您區域專屬的IP範圍新增至允許清單，可能會導致錯誤或效能不佳。

## 所有客戶均需要

* `52.247.108.70`

## 美國客戶

* `52.252.71.64/29`

## 加拿大客戶

* `20.220.135.16/29`

## EMEA客戶

* `51.137.8.208/29`

## 英國客戶

* `20.26.133.96/29`

## APAC客戶

* `20.53.201.168/29`
