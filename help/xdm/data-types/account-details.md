---
title: 帳戶詳細資訊資料類型
description: 此文檔概述了「帳戶詳細資訊體驗資料模型」(XDM)資料類型。
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# [!UICONTROL 帳戶詳細資訊] 資料類型

[!UICONTROL 帳戶詳細資訊] 是標準的體驗資料模型(XDM)資料類型，它描述與業務組織相關的詳細資訊。

![資料類型結構](../images/data-types/account-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL 貨幣]](./currency.md) | 組織的年收入估計數。 |
| `DUNSNumber` | 字串 | 該組織的Dun &amp; Bradstreet D-U-N-S號。 這是一個非指示性的九位數數字，分配給Dun &amp; Bradstreet資料庫中每個業務位置，具有獨特、獨立和獨特的操作，僅由Dun &amp; Bradstreet維護。 |
| `NAICSCode` | 字串 | 該組織在北美行業分類系統內的分類。 |
| `NAICSDescription` | 字串 | 根據組織的NAICS代碼對組織的業務線進行簡短描述。 |
| `SICCode` | 字串 | 組織的標準行業分類(SIC)代碼。 這是一個四位數的代碼，根據公司的業務活動對公司所屬行業進行分類。 |
| `SICDescription` | 字串 | 根據組織的SIC代碼對其業務線進行簡要描述。 |
| `companyProductAndServices` | 字串 | 組織正在處理或在其中開展業務的產品和服務。 |
| `facebookPageUrl` | 字串 | 一個指向該組織Facebook帳戶的網站連結。 |
| `industry` | 字串 | 此組織所屬的行業。 這是自由格式欄位，建議使用結構化值進行查詢或 `xdm:classifier` 屬性。 |
| `jigsaw` | 字串 | 組織的Data.com鍵。 |
| `linkedinPageUrl` | 字串 | 一個指向該組織LinkedIn帳戶的網站連結。 |
| `logoUrl` | 字串 | 要與Salesforce實例的URL組合的路徑(例如， `https://yourInstance.salesforce.com/`)以生成URL以請求與組織關聯的社交網路配置檔案映像。 所生成的URL將HTTP重定向（代碼302）返回到組織的社交網路配置檔案影像。 |
| `marketSegment` | 字串 | 組織參與的指定市場細分。 這是自由格式欄位，建議使用結構化值進行查詢或 `xdm:identifier` 屬性。 |
| `numberOfEmployees` | 整數 | 組織中的員工數。 |
| `organizationType` | 字串 | 描述組織類型的標籤。 |
| `primaryEmailDomain` | 字串 | 組織為其人員使用的主要電子郵件域。 |
| `rating` | 雙倍 | 此組織的計算得分或星級。 `1` 指示最大可能的評級， `0` 是最小可能的評級。 |
| `tickerSymbol` | 字串 | 此帳戶的股市符號。 最多20個字元。 |
| `twitterHandleUrl` | 字串 | 指向組織twitter句柄的網站連結。 |
| `website` | 字串 | 組織網站的URL。 |

{style=&quot;table-layout:auto&quot;}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
