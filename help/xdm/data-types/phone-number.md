---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構描述；電話號碼；xdm：phoneNumber；資料型別；資料型別；
solution: Experience Platform
title: 電話號碼資料型別
description: 瞭解電話號碼XDM資料型別。
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 16%

---

# [!UICONTROL 電話號碼]資料型別

[!UICONTROL 電話號碼]是描述電話號碼詳細資訊的標準XDM資料型別。

![](../images/data-types/phone-number.png){width=600}

| 屬性 | 說明 |
| --- | --- |
| `extension` | 用於從自備交換機、接線生或總機打電話的內部撥接號碼。 |
| `number` | 電話號碼。 請注意，電話號碼為字串，並可能包含有意義的字元，例如括弧`()`、連字型大小`-`或表示次撥接識別碼的字元，例如分機號碼`x`，例如`1-353(0)18391111`或`+613 9403600x1234`。 |
| `primary` | 表示這是否為個人主要電話號碼的布林值。 不像地址或電子郵件地址，主要電話號碼可能會有好幾個；每個通訊通道一個。 通訊通道是由型別定義（由父屬性的名稱表示）： `textMessaging`、`mobile`、`phone`、`home`、`work`、`unknown`和`fax`。 |
| `status` | 指出目前是否可以使用電話號碼。 |
| `statusReason` | 目前狀態的描述。 |
| `validity` | 電話號碼的技術正確性等級。 |

{style="table-layout:auto"}

如需電話號碼資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
