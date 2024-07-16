---
title: 外部來源系統稽核詳細資料
description: 瞭解外部Source系統稽核詳細資料體驗資料模型(XDM)欄位群組。
source-git-commit: 656070cf69e3713c7889f53d51937e0e70085d96
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 6%

---

# [!UICONTROL 外部Source系統稽核詳細資料]欄位群組

[!UICONTROL 外部Source系統稽核詳細資料]是標準的體驗資料模型(XDM)欄位群組，可參考核心「外部Source系統稽核屬性」的屬性並新增內容中繼資料，以擴充其資料型別。 如此可讓您進行詳細的稽核追蹤，並彈性整合來自外部來源的資料。

![外部Source系統稽核詳細資料欄位群組的結構描述圖。](../../images/field-groups/shared/external-source-system-audit-details.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL 外部Source系統稽核詳細資料] | `external-source-system-audit-details` | [[!UICONTROL 外部Source系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | &#39;[!UICONTROL 外部Source系統稽核詳細資料]&#39;欄位群組藉由參考其屬性並新增內容中繼資料，來擴充核心「外部Source系統稽核屬性」資料型別。 這有助於詳細稽核追蹤，以及外部來源的彈性資料整合，適應設定檔擷取的非同步性質。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [完整結構描述](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)