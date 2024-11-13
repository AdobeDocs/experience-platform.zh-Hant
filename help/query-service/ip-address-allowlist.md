---
keywords: IP位址， IP範圍，允許清單，允許清單，查詢服務，網路存取
title: 查詢服務的IP位址允許清單
description: 此頁面提供更新的IP範圍，您可將其新增至允許清單，以安全地存取查詢服務。
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: e6c148b943c68bff5330c7ff021ffa88ba131639
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# IP位址允許清單 {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建議您將此頁面加入書籤，每三個月重新造訪一次，以檢查最新IP位址。 Adobe不提供新IP範圍的通知。
> * 自2024年10月15日起，只有新的IP範圍才對查詢服務存取有效。 過時的IP位址已無法運作。 確保您的允許清單僅包含新IP，以避免服務中斷。

## 概觀 {#overview}

您可以透過網路防火牆定義網路存取控制。 透過指定適當的IP範圍，您可以允許查詢服務存取的流量。

作為持續改善的一部分，Adobe已更新網路存取查詢服務的IP範圍。 先前的IP位址現已棄用，只有新的IP位址有效。 請務必更新您的允許清單，以包含下列新IP範圍，以保持服務不中斷。

Adobe建議您根據所在的地區，將下列地區專屬的IP範圍新增至允許清單。 若未新增這些區域專屬的IP範圍，可能會導致錯誤或服務中斷。

## VA7：美國和美國的客戶 {#us-americas}

**新IP：** 4.152.211.251

## NLD2：EMEA客戶 {#emea}

**新IP：** 108.141.12.47

## AUS5：APAC客戶 {#apac}

**新IP：** 40.82.220.111

## CAN2：加拿大客戶 {#can2}

**新IP：** 4.172.28.20

## GBR9：英國客戶 {#gbr9}

**新IP：** 20.254.80.141

## 設定IP型限制 {#set-ip-restrictions}

使用[查詢服務授權API指南](./auth-api/overview.md)設定IP限制。 這些IP型限制可確保只有經過核准的網路和使用者端電腦才能透過Adobe Experience Platform中的SQL存取資料。 瞭解如何設定、強制執行及監控IP限制，以維護高安全性標準，並具備即時存取追蹤和警報功能。

* [快速入門手冊](./auth-api/getting-started.md)
* [IP存取端點指南](./auth-api/ip-access.md)
* [IP驗證端點指南](./auth-api/validate.md)
