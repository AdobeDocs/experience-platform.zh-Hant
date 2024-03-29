---
keywords: IP位址， IP範圍，允許清單，允許清單
title: 查詢服務的IP位址允許清單
description: 此頁面提供可新增至允許清單的IP範圍。
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: 3a00f98b7463f7fb35aa53f703d67193f18400cf
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# IP位址允許清單 {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建議您將此頁面加入書籤，每三個月重新造訪一次，以檢查最新IP位址。 Adobe不提供新IP範圍的通知。
> * 雖然Adobe支援將資料匯出至SFTP伺服器，但建議匯出資料的雲端儲存位置為 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 概觀 {#overview}

此頁面提供您可新增至允許清單的IP位址，以便安全地從Experience Platform匯出資料至您的 [SFTP伺服器](../destinations/catalog/cloud-storage/sftp.md).

您可以透過網路防火牆定義網路存取控制。 透過指定適當的IP範圍，您可以允許資料傳輸服務的流量。

Adobe建議您將下列IP範圍新增至允許清單，實際取決於您的地區。 未能將您區域專屬的IP範圍新增到允許清單可能會導致錯誤或效能不佳。

## VA7：美國和美洲客戶 {#us-americas}

* 20.14.241.153

## NLD2：EMEA客戶 {#emea}

* 20.101.233.128

## AUS5：APAC客戶 {#apac}

* 20.248.220.69

## CAN2：加拿大客戶 {#can2}

* 4.172.1.139

## GBR9：英國客戶 {#gbr9}

* 20.108.200.9

