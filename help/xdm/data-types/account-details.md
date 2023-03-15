---
title: 帳戶詳細資訊資料類型
description: 本檔案概述「帳戶詳細資料體驗資料模型」(XDM)資料類型。
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 5%

---

# [!UICONTROL 帳戶詳細資訊] 資料類型

[!UICONTROL 帳戶詳細資訊] 是標準的Experience Data Model(XDM)資料類型，可說明與業務組織相關的詳細資訊。

![資料類型結構](../images/data-types/account-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL 貨幣]](./currency.md) | 本組織的年收入估計數。 |
| `DUNSNumber` | 字串 | 該組織的Dun &amp; Bradstreet D-U-N-S號。 這是一個非指示性的九位數數字，分配給Dun &amp; Bradstreet資料庫中的每個業務位置，具有獨特、獨立和獨特的操作，僅由Dun &amp; Bradstreet維護。 |
| `NAICSCode` | 字串 | 組織在北美行業分類系統內的分類。 |
| `NAICSDescription` | 字串 | 根據組織的NAICS代碼，對組織業務線的簡短說明。 |
| `SICCode` | 字串 | 組織的標準工業分類(SIC)代碼。 這是一個四位數的代碼，根據公司的業務活動對公司所屬的行業進行分類。 |
| `SICDescription` | 字串 | 根據組織的SIC代碼，對組織的業務線的簡要描述。 |
| `companyProductAndServices` | 字串 | 組織正在處理或從事業務的產品和服務。 |
| `facebookPageUrl` | 字串 | 連結至組織之Facebook帳戶的網站。 |
| `industry` | 字串 | 此組織所屬的行業。 這是自由格式欄位，建議對查詢使用結構化值，或使用 `xdm:classifier` 屬性。 |
| `jigsaw` | 字串 | 組織的Data.com金鑰。 |
| `linkedinPageUrl` | 字串 | 連結至組織之LinkedIn帳戶的網站。 |
| `logoUrl` | 字串 | 要與Salesforce例項的URL結合的路徑(例如， `https://yourInstance.salesforce.com/`)產生URL，以要求與組織相關聯的社交網路設定檔影像。 產生的URL會傳回HTTP重新導向（程式碼302）至組織的社交網路設定檔影像。 |
| `marketSegment` | 字串 | 組織參與的已命名市場區段。 這是自由格式欄位，建議對查詢使用結構化值，或使用 `xdm:identifier` 屬性。 |
| `numberOfEmployees` | 整數 | 組織的員工人數。 |
| `organizationType` | 字串 | 說明組織類型的標籤。 |
| `primaryEmailDomain` | 字串 | 組織人員使用的主要電子郵件網域。 |
| `rating` | 雙倍 | 此組織的計算分數或星級。 `1` 指出最大可能的評等，以及 `0` 是最低的評等。 |
| `tickerSymbol` | 字串 | 此帳戶的股市符號。 最多20個字元。 |
| `twitterHandleUrl` | 字串 | 連結至組織之twitter控制代碼的網站連結。 |
| `website` | 字串 | 組織網站的URL。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
