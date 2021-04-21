---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas；地址；xdm:address;datatype；資料類型；
solution: Experience Platform
title: 郵遞區號資料類型
topic-legacy: overview
description: 本檔案提供「郵遞區號XDM」資料類型的概述。
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# [!UICONTROL Postal address] 資料類型

[!UICONTROL Postal address] 是一種標準的XDM資料類型，它描述了郵件地址的詳細資訊。

<img src="../images/data-types/postal-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `city` | 城市名稱。 |
| `country` | 政府管理領土的名稱。 這是自由格式欄位，可以使用任何語言來命名國家／地區名稱。 |
| `countryCode` | 國家／地區的雙字元<a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a>程式碼。 |
| `createdByBatchID` | 建立地址記錄的收錄批處理檔案的ID。 |
| `dmaID` | 尼爾森媒體研究指定了市場區域。 |
| `label` | 地址的自由格式名稱。 |
| `lastVerifiedDate` | 上次驗證地址為與人員仍然關聯的日期。 |
| `modifiedByBatchID` | 上次修改記錄的收錄批次檔案ID。 |
| `msaID` | 觀察發生地的美國都市統計區。 |
| `postOfficeBox` | 地址的郵局信箱。 |
| `postalCode` | 位置的郵遞區號。 郵遞區號並非所有國家／地區皆可使用。 在某些國家，這只會包含部分郵遞區號。 |
| `primary` | 一個布爾值，它指示這是否為個人的主地址。 配置式在給定時間點只能有一個`primary`地址。 |
| `region` | 地址的地區、縣或區部分。 |
| `repositoryCreatedBy` | 建立記錄的用戶的ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶的ID。 |
| `stateProvince` | 觀察的州或省部分。 格式遵循[ISO 3166-2（國家／地區和細分）](http://www.unece.org/cefact/locode/subdivisions.html)標準。 |
| `status` | 指出目前是否可使用此位址。 |
| `statusReason` | 當前`status`的說明。 |
| `street1` - `street4` | 這四個欄位應包含主要街道等級資訊、公寓編號、街號和街道名稱。 `street2` 選項 `street4` 卡。 |

有關郵遞區號資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)
