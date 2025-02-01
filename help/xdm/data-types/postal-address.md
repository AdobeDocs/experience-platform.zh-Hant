---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；欄位；綱要；綱要；位址；xdm：位址；資料型別；資料型別；
solution: Experience Platform
title: 郵寄地址資料型別
description: 瞭解郵寄地址XDM資料型別。
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 23%

---

# [!UICONTROL 郵寄地址]資料型別

[!UICONTROL 郵寄地址]是描述郵寄地址詳細資訊的標準XDM資料型別。

![](../images/data-types/postal-address.png){width=450}

| 屬性 | 說明 |
| --- | --- |
| `city` | 城市的名稱。 |
| `country` | 政府管理的領土的名稱。 這是自由格式的欄位，可以有任何語言的國家名稱。 |
| `countryCode` | 國家/地區的雙字元<a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a>代碼。 |
| `createdByBatchID` | 建立地址記錄之擷取批次檔案的ID。 |
| `dmaID` | Nielsen 媒體研究指定的市場區域。 |
| `label` | 此地址的任意格式名稱。 |
| `lastVerifiedDate` | 此地址最後驗證仍與個人相關聯的日期。 |
| `modifiedByBatchID` | 上次修改記錄之擷取批次檔的ID。 |
| `msaID` | 進行觀察的美國大都會統計區域。 |
| `postOfficeBox` | 地址的郵政信箱。 |
| `postalCode` | 地點的郵遞區號。無法提供所有國家/地區的郵遞區號。在部分國家/地區，這僅包含部分的郵遞區號。 |
| `primary` | 表示這是否為個人主要地址的布林值。 設定檔在特定時間只能有一個`primary`位址。 |
| `region` | 地址的地區、國家或區域部分。 |
| `repositoryCreatedBy` | 建立紀錄的使用者ID。 |
| `repositoryLastModifiedBy` | 上次修改紀錄的使用者ID。 |
| `stateProvince` | 觀察的州或省的部分。 格式遵循[ISO 3166-2 （國家/地區和次分割）](https://www.unece.org/cefact/locode/subdivisions.html)標準。 |
| `status` | 指出目前是否可以使用地址。 |
| `statusReason` | 目前`status`的說明。 |
| `street1` - `street4` | 這四個欄位的用途是包含主要街道層級資訊、公寓號碼、街道號碼和街道名稱。 `street2`至`street4`是選用專案。 |

{style="table-layout:auto"}

如需郵寄地址資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
