---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；結構；忠誠度詳細資訊；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: 忠誠度詳細資訊結構欄位組
topic-legacy: overview
description: 本檔案提供「忠誠度詳細資料」結構欄位群組的概觀。
source-git-commit: fe49560a69c4c02835f00e4ebc0a5b9dc88eae90
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 3%

---


# [!UICONTROL 忠誠度詳] 細資訊結構欄位群組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL 忠誠] 度詳細資訊類別的標準結構欄 [[!DNL XDM Individual Profile] 位群組](../../classes/individual-profile.md)。欄位群組提供單一物件類型欄位`loyalty`，可擷取客戶忠誠度計畫中與人員成員資格相關的資訊。

![](../../images/field-groups/loyalty-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `pointsExpiration` | 物件陣列 | 列出任何即將到期的忠誠點數（或忠誠點數群組），以及到期日。 每個陣列項目都必須是包含下列兩個屬性的物件： <ul><li>`pointsExpirationDate`:點將過期的ISO 8601日期時間。</li><li>`pointsExpiring`:截至相關到期日的到期點餘額。</li></ul> |
| `joinDate` | DateTime | 人員加入忠誠計畫的ISO 8601日期時間。 |
| `loyaltyID` | 字串陣列 | 代表與忠誠計畫成員相關聯的忠誠計畫ID。 |
| `points` | 雙倍 | 忠誠會員的目前忠誠點數或獎勵平衡。 |
| `pointsRedeemed` | 雙倍 | 忠誠會員已套用至購買或已換回的點數。 |
| `program` | 字串 | 已註冊人員的忠誠計畫的名稱。 |
| `status` | 字串 | 人員的忠誠會籍的目前狀態，例如`active`、`disabled`或`suspended`。 |
| `tier` | 字串 | 擷取已註冊人員的忠誠計畫層級。 |
| `upgradeDate` | 字串 | 將忠誠會員升級至其最新層級的日期。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-loyalty-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-loyalty-details.schema.json)
