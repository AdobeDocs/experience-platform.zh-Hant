---
keywords: Experience Platform；主題；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；架構；架構設計；混合；工作詳細資訊；配置檔案；
solution: Experience Platform
title: 工作聯繫人詳細資訊方案欄位組
description: 此文檔提供「工作聯繫人詳細資訊」架構欄位組的概覽。
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---


# [!UICONTROL 工作聯繫人詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 工作聯繫人詳細資訊] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md)。 該欄位組提供了幾個欄位，用於捕獲有關個人的職業資訊，如工作地址、工作電子郵件、工作電話號碼和此人所屬的組織。

![](../../images/field-groups/work-contact-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `workAddress` | [郵政地址](../../data-types/postal-address.md) | 描述人員的工作地址。 |
| `workEmail` | [電子郵件地址](../../data-types/email-address.md) | 描述人員的工作電子郵件地址。 |
| `workPhone` | [電話號碼](../../data-types/phone-number.md) | 描述人員的工作電話號碼。 |
| `organizations` | 字串（陣列） | 自由格式字串的陣列，它表示人員所屬的組織。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
