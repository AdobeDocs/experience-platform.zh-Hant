---
keywords: Experience Platform；主題；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；架構；架構設計；欄位組；欄位組；人員；人員詳細資訊；人員詳細資訊；個人；
solution: Experience Platform
title: 人口結構詳細資訊方案欄位組
description: 此文檔提供「人口結構詳細資訊」架構欄位組的概覽。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 3%

---


# [!UICONTROL 人口結構詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 人口結構詳細資訊] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md)。 欄位組提供根級別 `person` 對象，其子欄位描述有關個人的資訊。

![](../../images/field-groups/demographic-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `person.name` | [人員姓名](../../data-types/person-name.md) | 子欄位描述人員姓名的各種元素的對象。 |
| `person.birthDate` | 日期 | 人生的完整日期，以ISO 8601時間戳的形式。 |
| `person.birthDayAndMonth` | 字串 | 出生日期和月份，格式為MM-DD。 在已知某人出生的日月時，應使用此欄位，但不應使用年份。 |
| `person.birthYear` | 整數 | 一個人出生的年份，包括世紀（如1989年）。 當僅知道該人的年齡，而不是完整的出生日期時，應使用此欄位。 |
| `person.gender` | 字串 | 該人的性別身份。 |
| `person.martialStatus` | 字串 | 描述一個人與重要他人的關係。 |
| `person.nationality` | 字串 | 使用ISO 3166-1 Alpha-2代碼表示的個人與其國家之間的法律關係。 |
| `person.taxId` | 字串 | 人員的稅/會計標識，如美國的TIN或西班牙的CIF/NIF。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)