---
keywords: 檢視設定檔rtcdp;rtcdp設定檔檢視；rtcdp設定檔
title: 在Real-time Customer Data Platform中瀏覽設定檔
description: Adobe Real-time Customer Data Platform可讓您使用Adobe Experience Platform使用者介面來瀏覽即時客戶設定檔資料。
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# 在Real-time Customer Data Platform中瀏覽設定檔

「即時客戶設定檔」可建立個別客戶的全方位檢視，結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 當個別設定檔會根據從各種來源匯入系統的資料進行匯總時，每個設定檔都會成為客戶與您品牌每次互動的可操作時間戳記帳戶。

在Adobe Experience Platform使用者介面中，您可以檢視這些唯讀設定檔，並查看有關每個個別客戶的重要資訊，包括其偏好設定、過去事件、互動，以及個人所屬的區段。

Adobe Real-time Customer Data Platform建置在Adobe Experience Platform上，因此可以使用Experience PlatformUI中的設定檔檢視功能。 如需在Platform使用者介面中檢視客戶設定檔的詳細指南，請參閱 [即時客戶個人檔案使用手冊](../../profile/ui/user-guide.md).

## Real-Time CDP B2B版的設定檔增強功能

除了Adobe Experience Platform、Real-Time CDP支援的設定檔瀏覽功能外，B2B Edition使用者還可以在 [!UICONTROL 屬性] 和 [!UICONTROL 事件] 頁簽。 B2B資料也可用來執行分段，這些區段會顯示在客戶的 [!UICONTROL 區段成員資格] 標籤並搭配非B2B區段。

Real-Time CDP B2B Edition還允許您瀏覽 [!UICONTROL 帳戶], [!UICONTROL 機會]，和 [!UICONTROL 源記錄] 從與個別客戶關聯的企業來源取得。

若要探索這些增強功能，請先依照 [即時客戶個人檔案使用手冊](../../profile/ui/user-guide.md) 要通過合併策略或標識命名空間來瀏覽配置檔案。

![](images/b2b-browse-profile.png)

設定檔詳細資料包括 [!UICONTROL 帳戶], [!UICONTROL 機會]，和 [!UICONTROL 源記錄] 索引標籤，以及客戶設定檔中提供的標準資訊，此資訊也已透過B2B事件和屬性進行增強。

![](images/b2b-profile-detail.png)

### 帳戶索引標籤

選擇 **[!UICONTROL 帳戶]** 查看與配置檔案相關的帳戶清單。 此清單包含帳戶設定檔的基本資訊，例如帳戶的名稱、網站和產業，以及帳戶設定檔的連結。

如需檢視和探索帳戶設定檔的詳細資訊，請先閱讀 [帳戶設定檔概觀](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### 「機會」頁簽

此 **[!UICONTROL 機會]** 索引標籤提供與帳戶相關的未結和已結業務機會的詳細資訊。 這些機會可能會從多個來源擷取到Experience Platform中，但Real-Time CDP B2B版可讓行銷人員輕鬆在單一位置一併看到所有這些機會。

每個機會都包括以下資訊：機會的名稱、其金額、階段，以及該機會是開啟、關閉、成功還是丟失。

![](images/b2b-profile-opportunities.png)

### 源記錄頁簽

此 **[!UICONTROL 源記錄]** 標籤可讓您輕鬆查看來自企業來源的多個來源記錄，這些記錄對單一客戶設定檔有貢獻。 除了 [!UICONTROL 人員源密鑰] 和電子郵件地址，每個來源記錄也提供記錄類型（例如「聯絡人」或「銷售機會」記錄）以及來源。

![](images/b2b-profile-source-records.png)
