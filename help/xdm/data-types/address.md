---
title: 郵寄地址資料型別
description: 瞭解郵寄地址體驗資料模型(XDM)資料型別。
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 41%

---

# [!UICONTROL 郵寄地址]資料型別

[!UICONTROL 郵寄地址]是提供地址詳細資訊的標準Experience Data Model (XDM)資料型別。

![ [!UICONTROL 郵寄地址]資料型別的圖表。](../images/data-types/postal-address.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL 主要] | `primary` | 布林值 | 主要地址指標。 設定檔在特定時間只能有一個`primary`位址。 |
| [!UICONTROL 標籤] | `label` | 字串 | 地址的自由形式名稱。 |
| [!UICONTROL 街道1] | `street1` | 字串 | 主要的街道層級資訊: 公寓號碼、門牌號碼和街道名稱。 |
| [!UICONTROL 街道2] | `street2` | 字串 | 選用的街道資訊第二行。 |
| [!UICONTROL 街道3] | `street3` | 字串 | 選用的街道資訊第三行。 |
| [!UICONTROL 街道4] | `street4` | 字串 | 選用的街道資訊第四行。 |
| [!UICONTROL 地區] | `region` | 字串 | 地址的地區、國家或區域部分。 |
| [!UICONTROL Post Office Box] | `postOfficeBox` | 字串 | 地址的郵政信箱。 |
| [!UICONTROL 國家/地區] | `country` | 字串 | 政府管理的領土的名稱。 除了``countryCode``，這是自由格式的欄位，可以有任何語言的國家名稱。 |
| [!UICONTROL 狀態] | `state` | 字串 | 州名。此為自由格式的欄位。 |
| [!UICONTROL 狀態] | `status` | 字串 | 使用地址能力的指示。 |
| [!UICONTROL 狀態原因] | `statusReason` | 字串 | 目前狀態的描述。 |
| [!UICONTROL 上次驗證日期] | `lastVerifiedDate` | 字串 | 最後一次驗證地址仍與個人相關聯的日期。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫上的[完整結構描述](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json)：
