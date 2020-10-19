---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;data-type;data type;
solution: Experience Platform
title: 電話號碼資料類型
topic: overview
description: 本文檔概述電話號碼XDM資料類型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---


# [!UICONTROL 電話號碼] ，資料類型

[!UICONTROL 電話號碼] (Phone number)是一種標準的XDM資料類型，用於描述電話號碼的詳細資訊。

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 屬性 | 說明 |
| --- | --- |
| `extension` | 用於從私人交換機、操作員或交換機呼叫的內部撥號號碼。 |
| `number` | 電話號碼。 請注意，電話號碼是字串，可能包含有意義的字元，例如括弧、連字型大小或字元 `()`, `-`以指出子撥號識別碼(例如，或 `x` 延伸模組) `1-353(0)18391111``+613 9403600x1234`。 |
| `primary` | 一個布爾值，它指示這是否是個人的主要電話號碼。 與地址或電子郵件地址不同，主要電話號碼可能有多個；每個通信通道一個。 通信通道由類型定義（由父屬性的名稱指示）: `textMessaging`、 `mobile`、 `phone`、 `home`、 `work`、和 `unknown``fax`。 |
| `status` | 指示當前是否可以使用電話號碼。 |
| `statusReason` | 當前狀態的說明。 |
| `validity` | 電話號碼的技術正確性。 |

有關電話號碼資料類型的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)