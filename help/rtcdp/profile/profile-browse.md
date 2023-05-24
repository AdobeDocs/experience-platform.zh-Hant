---
keywords: 視圖配置檔案rtcdp;rtcdp配置檔案視圖；rtcdp配置檔案
title: 瀏覽Real-time Customer Data Platform的配置檔案
description: Adobe Real-time Customer Data Platform使您能夠使用Adobe Experience Platform用戶介面瀏覽即時客戶配置檔案資料。
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# 瀏覽Real-time Customer Data Platform的配置檔案

即時客戶配置檔案可建立您每個客戶的整體視圖，將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 由於單個配置檔案是根據從各種來源引入系統的資料進行聚合的，因此每個配置檔案都會成為一個可操作且時間戳記的帳戶，用於記錄您的客戶與您的品牌進行的每次交互。

在Adobe Experience Platform用戶介面中，您可以查看這些只讀配置檔案，並查看有關每個客戶的重要資訊，包括其首選項、過去事件、交互以及個人所屬的段。

Adobe Real-time Customer Data Platform建在Adobe Experience Platform之上，因此能夠利用Experience PlatformUI中的配置檔案查看功能。 有關在平台用戶介面中查看客戶配置檔案的詳細指南，請參閱 [即時客戶概要檔案使用手冊](../../profile/ui/user-guide.md)。

## Real-Time CDPB2B版配置檔案增強功能

除了Adobe Experience Platform、Real-Time CDP和B2B版支援的配置檔案瀏覽功能外，B2B版用戶可以訪問客戶配置檔案中的B2B屬性和事件 [!UICONTROL 屬性] 和 [!UICONTROL 事件] 頁籤。 B2B資料也可用於執行分割，這些段出現在客戶的下面 [!UICONTROL 段成員資格] 頁籤

Real-Time CDPB2B版還允許您瀏覽 [!UICONTROL 帳戶]。 [!UICONTROL 機會], [!UICONTROL 源記錄] 與單個客戶關聯的企業源。

要瞭解這些增強功能，請首先執行中概述的步驟 [即時客戶概要檔案使用手冊](../../profile/ui/user-guide.md) 通過合併策略或標識命名空間瀏覽配置檔案。

![](images/b2b-browse-profile.png)

配置檔案詳細資訊包括訪問 [!UICONTROL 帳戶]。 [!UICONTROL 機會], [!UICONTROL 源記錄] 頁籤，此外，客戶配置檔案中提供的標準資訊也已通過B2B事件和屬性得到增強。

![](images/b2b-profile-detail.png)

### 「帳戶」頁籤

選擇 **[!UICONTROL 帳戶]** 查看與配置檔案相關的帳戶清單。 此清單包括帳戶配置檔案的基本資訊，以及指向帳戶配置檔案的連結。

有關查看和瀏覽帳戶配置檔案的詳細資訊，請從閱讀 [帳戶概要資訊](../accounts/account-profile-overview.md)。

![](images/b2b-profile-accounts.png)

### 機會頁籤

的 **[!UICONTROL 機會]** 頁籤提供與與帳戶相關的未結和已結業務機會相關的詳細資訊。 這些機會可能會從多個來源被Experience Platform，但是，Real-Time CDPB2B版使營銷人員能夠輕鬆地在一個地方看到所有這些機會。

每個機會都包括諸如機會名稱、其金額、階段以及該機會是開啟、關閉、贏得還是丟失等資訊。

![](images/b2b-profile-opportunities.png)

### 「源記錄」頁籤

的 **[!UICONTROL 源記錄]** 頁籤使您能夠輕鬆查看來自企業來源的多個來源記錄，這些來源記錄對單個客戶配置檔案有幫助。 除 [!UICONTROL 人員源鍵] 和電子郵件地址，每個來源記錄還提供記錄類型（例如，「聯繫人」或「線索」記錄），以及來源。

![](images/b2b-profile-source-records.png)
