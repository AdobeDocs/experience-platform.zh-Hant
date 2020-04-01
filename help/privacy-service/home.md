---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform隱私權服務
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364

---


# Adobe Experience Platform隱私權服務概觀

為了提供更好的客戶體驗，您需要收集和儲存客戶的個人資料。 使用這些資料時，請務必瞭解並尊重客戶的隱私權。 新的法律和組織法規讓使用者有權應要求從資料存放區存取或刪除其個人資料。

Adobe Experience Platform Privacy Service提供REST風格的API和使用者介面，可協助您管理客戶的這些資料要求。 透過隱私權服務，您可以提交從Adobe Experience Cloud應用程式存取和刪除私人或個人客戶資料的要求，以利自動符合法律和組織的隱私權法規。

## 為何選擇隱私權服務？

隱私權服務是因應企業管理客戶個人資料的方式發生根本轉變而開發。 隱私權服務的主要目的是自動遵守資料隱私權規定，一旦違反該規定，可能會導致貴公司遭受重大罰款並中斷資料營運。

### 隱私權服務與GDPR

通用 [資料保護規則](https://eugdpr.org/) (GDPR)為歐盟成員國引進了數項新的資料隱私權，包括存取權 **和** 被遺忘權 ****。 這表示，您的企業已收集個人資料的任何歐盟公民，都可隨時要求存取或刪除其資料。 若未能在30天內遵守這些要求，您的組織將面臨數百萬美元的罰款。

隱私權服務支援存取和刪除GDPR要求，並與CCPA規則下的要求分開追蹤。 請參閱 [GDPR常見問答](gdpr/faq.md)[和術語文](gdpr/terminology.md) 件，以取得詳細資訊。

### 隱私權服務與CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. CCPA為加州居民提供新的資料隱私權，包括存取和刪除其個人資料的權利，以得知其個人資料是賣給或披露（以及向誰），以及選擇不將其資料賣給第三方的權利。

隱私權服務支援存取和刪除CCPA規則的要求，並與GDPR要求分開追蹤。 隱私權服務也支援傳送支援Experience Cloud應用程式的退出銷售要求。 請參閱 [CCPA常見問答](ccpa/faq.md) ，以取得詳細資訊。

## 如何使用隱私權服務管理隱私權工作要求

隱私權服務提供REST風格的API和使用者介面，讓您管理客戶存取／刪除其私人資料或選擇退出銷售的要求(也稱為隱 **私工作**)。 此服務也提供集中稽核與記錄機制，讓您檢視與Experience Cloud應用程式有關的隱私權工作狀態與結果。

>[!NOTE] 退出要求目前僅受隱私權服務API支援。

### 使用API

隱 [私權服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) 可讓您使用REST風格的API呼叫來建立和管理隱私權工作，讓您以程式設計方式處理Experience Cloud應用程式的隱私權法規遵循。 如需如何使用API的詳細步驟，請參閱「隱私 [服務API開發人員指南」](api/getting-started.md)。

### 使用UI

「隱私服務」UI允許您使用圖形介面建立和監視隱私作業。 UI包含狀態報 **告介面工具集** ，可以視覺化呈現所有作用中請求的狀態，並可讓您使用內建的 **Request Builder** 或上傳JSON檔案來建立新請求。 如需使用UI的詳細資訊，請參閱「隱私 [服務」使用指南](ui/overview.md)。