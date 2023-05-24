---
keywords: IP地址、IP範圍、允許清單目標、允許清單
title: 雲儲存目標的IP地址允許清單
type: Documentation
description: 此頁提供了IP範圍，您可以將這些範圍添加到允許清單中，以便安全地將資料從Experience Platform導出到SFTP伺服器、AmazonS3或Azure Blob儲存。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 雲儲存目標的IP地址允許清單 {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建議您將此頁面加入書籤，然後每三個月重新訪問一次，以檢查最新的IP地址。 Adobe不提供新IP範圍的通知。
> * 雖然Adobe支援向SFTP伺服器導出資料，但建議的用於導出資料的雲儲存位置 [!DNL Amazon S3] 和 [!DNL Azure Blob]。


## 總覽 {#overview}

本頁提供了IP範圍，您可以將這些範圍添加到允許清單中，以安全地將資料從Experience Platform導出到 [SFTP伺服器](./sftp.md)。

您可以通過網路防火牆定義網路訪問控制。 通過指定適當的IP範圍，您可以允許資料傳輸服務的通信。

Adobe建議在使用雲儲存目標連接之前，將以下IP範圍添加到允許清單。 如果無法將特定於區域的IP範圍添加到允許清單，則在使用雲儲存目標連接時可能會導致錯誤或效能不佳。

## 所有客戶都需要

* `52.247.108.70`

## 美國客戶

* `52.252.71.64/29`

## EMEA客戶

* `51.137.8.208/29`

## APAC客戶

* `20.53.201.168/29`
