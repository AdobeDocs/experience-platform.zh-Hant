---
title: 附注資料型別
description: 瞭解註釋體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# [!UICONTROL 註解]資料型別

[!UICONTROL Annotation]是標準的體驗資料模型(XDM)資料型別，其中包含可歸因至作者的文位元組點。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![註解資料型別結構](../../../images/healthcare/data-types/annotation.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 作者參考] | `authorReference` | [[!UICONTROL 參考]](../data-types/reference.md) | 對作者的引用。 |
| [!UICONTROL 作者] | `authorString` | 字串 | 負責註解的個人。 |
| [!UICONTROL 文字] | `text` | 字串 | 註解的內容。 |
| [!UICONTROL 時間] | `time` | 日期時間 | 建立註解的時間。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
