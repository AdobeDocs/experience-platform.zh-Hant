---
keywords: Experience Platform;home；常用主題；模式；模式；XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype；資料類型；
solution: Experience Platform
title: 電話號碼資料類型
topic: overview
description: 本文檔概述電話號碼XDM資料類型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# [!UICONTROL 電話] 號碼資料類型

[!UICONTROL 電] 話號碼是標準XDM資料類型，用於描述電話號碼的詳細資訊。

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 屬性 | 說明 |
| --- | --- |
| `extension` | 用於從私人交換機、操作員或交換機呼叫的內部撥號號碼。 |
| `number` | 電話號碼。 請注意，電話號碼是字串，可能包含有意義的字元，如括弧`()`、連字型大小`-`或字元，以指示副撥號標識符，如`x`，例如`1-353(0)18391111`或`+613 9403600x1234`。 |
| `primary` | 一個布爾值，它指示這是否是個人的主要電話號碼。 與地址或電子郵件地址不同，主要電話號碼可能有多個；每個通信通道一個。 通信通道由類型定義（由父屬性的名稱指示）:`textMessaging`、`mobile`、`phone`、`home`、`work`、`unknown`和`fax`。 |
| `status` | 指示當前是否可以使用電話號碼。 |
| `statusReason` | 當前狀態的說明。 |
| `validity` | 電話號碼的技術正確性。 |

有關電話號碼資料類型的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)