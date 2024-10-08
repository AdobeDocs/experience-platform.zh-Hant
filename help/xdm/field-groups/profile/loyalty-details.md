---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個人設定檔；欄位；結構；結構；忠誠度詳細資料；結構描述設計；欄位群組；欄位群組；
solution: Experience Platform
title: 熟客方案詳細資料結構欄位群組
description: 瞭解熟客方案詳細資料結構欄位群組。
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# [!UICONTROL 熟客方案詳細資料]結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱更新](../name-updates.md)的檔案。

[!UICONTROL 熟客方案詳細資料]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組。 欄位群組提供單一物件型別欄位`loyalty`，可擷取有關客戶忠誠計畫中的個人會員資格資訊。

![](../../images/field-groups/loyalty-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `pointsExpiration` | 物件陣列 | 列出任何即將過期的熟客點數（或熟客點群組），以及到期日期。 每個陣列專案都必須是包含下列兩個屬性的物件： <ul><li>`pointsExpirationDate`：點到期的ISO 8601日期時間。</li><li>`pointsExpiring`：截至相關到期日的點數餘額。</li></ul> |
| `joinDate` | 日期時間 | 個人加入忠誠計畫的ISO 8601日期時間。 |
| `loyaltyID` | 字串陣列 | 代表與熟客方案會員相關聯的熟客方案ID。 |
| `points` | 雙精度 | 目前忠誠會員的忠誠度積分或獎勵餘額。 |
| `pointsRedeemed` | 雙精度 | 忠誠會員已套用於購買或以其他方式兌換的點數金額。 |
| `program` | 字串 | 個人註冊的熟客方案名稱。 |
| `status` | 字串 | 人員的熟客方案會員資格目前的狀態，例如`active`、`disabled`或`suspended`。 |
| `tier` | 字串 | 擷取人員註冊的熟客方案層級。 |
| `upgradeDate` | 字串 | 熟客方案會員升級至其最近層級的日期。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
