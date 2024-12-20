---
title: 帳戶詳細資料資料型別
description: 瞭解帳戶詳細資料體驗資料模型(XDM)資料型別。
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 11%

---

# [!UICONTROL 帳戶詳細資料]資料型別

[!UICONTROL 帳戶詳細資料]是標準的體驗資料模型(XDM)資料型別，可描述與業務組織相關的詳細資料。

![資料型別結構](../images/data-types/account-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL 貨幣]](./currency.md) | 預估的組織年收入金額。 |
| `DUNSNumber` | 字串 | 組織的Dun &amp; Bradstreet D-U-N-S編號。 這是指派給Dun &amp; Bradstreet資料庫中每個商業地點的非指示性九位數編號，具有唯一、單獨和相異的操作，並完全由Dun &amp; Bradstreet維護。 |
| `NAICSCode` | 字串 | 該組織在北美產業分類系統中的分類。 |
| `NAICSDescription` | 字串 | 組織的企業營運的簡短說明（根據其NAICS代碼）。 |
| `SICCode` | 字串 | 組織的標準產業分類(SIC)代碼。 這是四位數的代碼，會根據公司的業務活動來分類其所屬的產業。 |
| `SICDescription` | 字串 | 組織的企業營運的簡短說明（根據其SIC代碼）。 |
| `companyProductAndServices` | 字串 | 組織正在交易或做生意的產品和服務。 |
| `facebookPageUrl` | 字串 | 組織的指向Facebook帳戶的網站連結。 |
| `industry` | 字串 | 這個組織所屬的產業。 這是自由格式的欄位，建議使用結構化的查詢值或使用`xdm:classifier`屬性。 |
| `jigsaw` | 字串 | 組織的Data.com金鑰。 |
| `linkedinPageUrl` | 字串 | 組織的指向LinkedIn帳戶的網站連結。 |
| `logoUrl` | 字串 | 路徑將與Salesforce執行個體的URL （例如`https://yourInstance.salesforce.com/`）結合，以產生URL來請求與組織相關聯的社交網路設定檔影像。 產生的URL會傳回HTTP重新導向（代碼302）至組織的社交網路設定檔影像。 |
| `marketSegment` | 字串 | 組織參與的已命名市場對象。 這是自由格式的欄位，建議使用結構化的查詢值或使用`xdm:identifier`屬性。 |
| `numberOfEmployees` | 整數 | 組織的員工人數。 |
| `organizationType` | 字串 | 說明組織型別的標籤。 |
| `primaryEmailDomain` | 字串 | 組織用於其人員的主要電子郵件網域。 |
| `rating` | 雙精度 | 此組織的計算分數或星級評等。 `1`表示最高評分，`0`表示最低評分。 |
| `tickerSymbol` | 字串 | 此帳戶的股票代碼。最多 20 個字元。 |
| `twitterHandleUrl` | 字串 | 指向組織twitter控制代碼的網站連結。 |
| `website` | 字串 | 組織網站的 URL。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
