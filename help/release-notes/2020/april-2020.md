---
title: Adobe Experience Platform 發行說明
description: Experience Platform發行說明2020年4月8日
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: c3166bea873572fe6ee2e63dfd13bc64d81e252b

---


# Adobe Experience Platform 發行說明

## 發行日期: 2020 年 4 月 8 日

## 隱私權服務

新的法律和組織法規讓使用者有權應要求從資料存放區存取或刪除其個人資料。 Adobe Experience Platform Privacy Service提供REST風格的API和使用者介面，可協助您管理客戶的這些資料要求。 透過隱私權服務，您可以提交從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料的要求，以利自動符合法律和組織的隱私權法規。

**新功能**

| 功能 | 說明 |
| --- | --- |
| PDPA支援 | 現在，您可以根據泰國的個人資料保護法(PDPA)來建立和追蹤隱私權要求。 在API中提出隱私權要求時， `regulation` 陣列接受&quot;pdpa_tha&quot;值。 |
| UI中的名稱空間類型 | 您現在可以在「隱私服務」UI的「請求產生器」中指定不同的命名空間類型。 如需詳細 [資訊，請參閱](../../privacy-service/ui/user-guide.md) 「使用指南」。 |
| 淘汰舊端點 | 舊API端點(`data/privacy/gdpr`)已過時。 |

已知問題

* 無

如需隱私權服務的詳細資訊，請先閱讀隱私權服務 [概觀](../../privacy-service/home.md)。

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->