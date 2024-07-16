---
keywords: 檢視設定檔rtcdp；rtcdp設定檔檢視；rtcdp設定檔
title: 在Real-time Customer Data Platform中瀏覽設定檔
description: Adobe Real-time Customer Data Platform可讓您使用Adobe Experience Platform使用者介面瀏覽即時客戶個人檔案資料。
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: ea785ffa1dfa0f7c684fe536796a4b7409882159
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# 在Real-time Customer Data Platform中瀏覽設定檔

即時客戶設定檔可為個別客戶建立整體檢視，並結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 當個別設定檔是根據從各種來源帶入系統的資料進行彙總時，每個設定檔都會變成可操作、附有時間戳記的帳戶，說明客戶與您品牌每次互動。

在Adobe Experience Platform使用者介面中，您可以檢視這些唯讀設定檔，並檢視有關每個個別客戶的重要資訊，包括其偏好設定、過去事件、互動和個人所屬的對象。

Adobe Real-time Customer Data Platform是以Adobe Experience Platform為建置基礎，因此能夠利用Experience Platform UI中的設定檔檢視功能。 如需在Platform使用者介面中檢視客戶設定檔的詳細指南，請參閱[即時客戶設定檔使用者指南](../../profile/ui/user-guide.md)。

## Real-Time CDP B2B版本的設定檔增強功能

除了Adobe Experience Platform、Real-Time CDP、B2B Edition支援的設定檔瀏覽功能之外，使用者還可以分別在[!UICONTROL 屬性]和[!UICONTROL 事件]標籤上存取客戶設定檔中的B2B屬性和事件。 B2B資料也可用來執行分段，這些對象會出現在客戶的[!UICONTROL 對象成員資格]標籤下，以及非B2B對象。

Real-Time CDP， B2B Edition也可讓您從與個別客戶相關聯的企業來源瀏覽[!UICONTROL 帳戶]、[!UICONTROL 機會]和[!UICONTROL Source記錄]。

若要探索這些增強功能，請依照在[即時客戶設定檔使用手冊](../../profile/ui/user-guide.md)中概述的步驟，依合併原則或身分名稱空間瀏覽設定檔。

![](images/b2b-browse-profile.png)

除了客戶設定檔中提供的標準資訊之外，設定檔詳細資料還包含對[!UICONTROL 帳戶]、[!UICONTROL 商機]和[!UICONTROL Source記錄]標籤的存取權，這些資訊已透過B2B事件和屬性增強。

![](images/b2b-profile-detail.png)

若要進一步瞭解Platform UI中提供的設定檔詳細資料，請參閱設定檔儀表板檔案](../../dashboards/guides/profiles.md#browse-profiles)的[詳細資訊區段。

### 帳戶標籤

選取&#x200B;**[!UICONTROL 帳戶]**&#x200B;以檢視與設定檔相關的帳戶清單。 此清單包含帳戶設定檔的基本資訊，例如帳戶的名稱、網站和產業，以及帳戶設定檔的連結。

如需檢視和探索帳戶設定檔的詳細資訊，請先閱讀[帳戶設定檔總覽](../accounts/account-profile-overview.md)。

![](images/b2b-profile-accounts.png)

### 機會標籤

**[!UICONTROL 商機]**&#x200B;索引標籤提供與帳戶相關的未結與已結商機的詳細資料。 這些機會可能會從多個來源引入Experience Platform，但Real-Time CDP B2B版本讓行銷人員輕鬆地在一個位置一起看到所有這些機會。

每個商機都包含商機的名稱、數量、階段，以及商機是否開啟、關閉、成功或失敗等資訊。

![](images/b2b-profile-opportunities.png)

### Source記錄索引標籤

**[!UICONTROL Source記錄]**&#x200B;索引標籤可讓您輕鬆檢視來自企業來源的多筆來源記錄，這些記錄對單一客戶設定檔有貢獻。 除了[!UICONTROL 人員來源金鑰]和電子郵件地址之外，每個來源記錄也提供記錄型別（例如，「連絡人」或「潛在客戶」記錄）以及來源。

![](images/b2b-profile-source-records.png)
