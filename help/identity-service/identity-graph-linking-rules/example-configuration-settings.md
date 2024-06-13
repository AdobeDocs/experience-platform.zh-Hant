---
title: 設定範例
description: 瞭解使用圖表模擬工具時的設定範例。
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 22%

---

# 圖表設定範例

>[!NOTE]
>
>「CRM ID」是自訂名稱空間。 因此，下列範例需要您建立具有「CRM ID」顯示名稱和身分符號的自訂名稱空間。

下節是您在圖形模擬中可能遇到的圖形案例範例。

## 僅限CRM ID

事件：

* CRM ID：Tom，ECID：111

演演算法設定：

| 優先等級 | 顯示名稱 | 身分符號 | 身分類型 | 在每個圖表中唯一 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | 跨裝置 | 是 |
| 2 | ECID | ECID | COOKIE | 否 |

+++選取以檢視模擬圖形

+++

## 使用雜湊電子郵件的CRM ID

此情境中，CRM ID會內嵌並代表線上（體驗事件）和離線（設定檔記錄）資料。 此案例也涉及雜湊電子郵件的擷取，其代表CRM記錄資料集中傳送的另一個名稱空間以及CRM ID。

事件：

* CRM識別碼：Tom， Email_LC_SHA256： tom<span>@acme.com
* CRM ID：Tom，ECID：111
* CRM ID：Summer， Email_LC_SHA256： summer<span>@acme.com
* CRM ID：Summer，ECID：222

演演算法設定：

| 優先等級 | 顯示名稱 | 身分符號 | 身分類型 | 在每個圖表中唯一 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | 跨裝置 | 是 |
| 2 | 電子郵件 (SHA256，小寫) | Email_LC_SHA256 | 電子郵件 | 否 |
| 3 | ECID | ECID | COOKIE | 否 |

+++選取以檢視模擬圖形

+++

## 使用雜湊電子郵件、雜湊電話、GAID及IDFA的CRM ID

事件：

* CRM識別碼：Tom， Email_LC_SHA256：aabbcc， Phone_SHA256:123-4567
* CRM ID：Tom，ECID：111
* crm ID：Tom，ECID：222，IDFA：A-A-A
* CRM識別碼：Summer， Email_LC_SHA256： deeff， Phone_SHA256： 765-4321
* CRM ID：Summer，ECID：333
* CRM ID：Summer，ECID：444，GAID：B-B-B

演演算法設定：

| 優先等級 | 顯示名稱 | 身分符號 | 身分類型 | 在每個圖表中唯一 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | 跨裝置 | 是 |
| 2 | 電子郵件 (SHA256，小寫) | Email_LC_SHA256 | 電子郵件 | 否 |
| 3 | 電話 (SHA256) | Phone_SHA256 | 電話 | 否 |
| 4 | Google廣告ID (GAID) | GAID | 裝置 | 否 |
| 5 | Apple IDFA (Apple的ID) | IDFA | 裝置 | 否 |
| 6 | ECID | ECID | COOKIE | 否 |

+++選取以檢視模擬圖形

+++