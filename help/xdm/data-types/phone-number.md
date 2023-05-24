---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；欄位；模式；方案；電話號碼；xdm：電話號碼；資料類型；資料類型；
solution: Experience Platform
title: 電話號碼資料類型
description: 此文檔概述電話號碼XDM資料類型。
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# [!UICONTROL 電話號碼] 資料類型

[!UICONTROL 電話號碼] 是描述電話號碼詳細資訊的標準XDM資料類型。

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 屬性 | 說明 |
| --- | --- |
| `extension` | 用於從專用交換機、操作員或交換機進行呼叫的內部撥號號碼。 |
| `number` | 電話號碼。 請注意，電話號碼是字串，可能包含有意義的字元，如括弧 `()`，連字元 `-`，或用於指示子撥號標識符（如副檔名）的字元 `x` 比如說， `1-353(0)18391111` 或 `+613 9403600x1234`。 |
| `primary` | 一個布爾值，它指示這是否是個人的主要電話號碼。 與地址或電子郵件地址不同，主電話號碼可以多個；每個通信通道1個。 通信通道由類型（由父屬性的名稱指示）定義： `textMessaging`。 `mobile`。 `phone`。 `home`。 `work`。 `unknown`, `fax`。 |
| `status` | 指示當前是否可以使用電話號碼。 |
| `statusReason` | 當前狀態的說明。 |
| `validity` | 電話號碼的技術正確性級別。 |

{style="table-layout:auto"}

有關電話號碼資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
