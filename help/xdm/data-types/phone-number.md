---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；phoneNumber;xdm:phoneNumber；資料類型；資料類型；
solution: Experience Platform
title: 電話號碼資料類型
description: 本檔案概述電話號碼XDM資料類型。
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 2%

---

# [!UICONTROL 電話號碼] 資料類型

[!UICONTROL 電話號碼] 是標準的XDM資料類型，可說明電話號碼的詳細資訊。

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 屬性 | 說明 |
| --- | --- |
| `extension` | 用於從私人交換機、操作員或交換機呼叫的內部撥號號碼。 |
| `number` | 電話號碼。 請注意，電話號碼是字串，可能包含有意義的字元，例如括弧 `()`，連字型大小 `-`，或用於指示子撥號標識符（如副檔名）的字元 `x` 例如， `1-353(0)18391111` 或 `+613 9403600x1234`. |
| `primary` | 一個布林值，指示這是否是個人的主要電話號碼。 與地址或電子郵件地址不同，可以有多個主要電話號碼；每個通信通道一個。 通訊通道由類型（以父屬性的名稱指示）定義： `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`，和 `fax`. |
| `status` | 指示當前是否可以使用電話號碼。 |
| `statusReason` | 目前狀態的說明。 |
| `validity` | 電話號碼的技術正確性。 |

{style=&quot;table-layout:auto&quot;}

如需電話號碼資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
