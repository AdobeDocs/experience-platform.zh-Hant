---
title: Algolia使用者設定檔Source概觀
description: 瞭解Adobe Experience Platform中的Algolia使用者設定檔來源
hide: true
hidefromtoc: true
source-git-commit: 1bde4b831f1b79de1a8292ad5f221f522e871d08
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!DNL Algolia User Profiles]

[[!DNL Algolia]](https://www.algolia.com/)是功能強大的搜尋和探索API平台，可讓企業提供快速、相關且可自訂的搜尋體驗。 它提供即時搜尋功能，具備拼寫錯誤容許度、篩選、多面向和AI支援的相關性調整等功能。 [!DNL Algolia]藉由為網站、電子商務平台和應用程式提供高效能搜尋解決方案，協助公司改善使用者參與度、轉換率和整體客戶體驗。

[!DNL Algolia]的一些主要優點包括：

* 快速搜尋，立即產生結果。
* 由AI提供支援的高度相關建議。
* 可自訂的排名，可排定業務需求的優先順序。
* 可輕鬆處理高流量負載的擴充性。

如需詳細資訊，請瀏覽[[!DNL Algolia] 產品檔案](https://resources.algolia.com/)。

## 架構

自助來源(批次SDK)提供所有必要的功能，例如驗證、分頁或完整和部分資料提取。 [!DNL Algolia User Profiles]來源使用這些功能來完成整合。

![Algoria與Experience Platform整合的架構](../../images/tutorials/create/algolia/user-profiles/algolia-aep-user-profiles-arch.png)

## 先決條件 {#prerequisites}

您必須先完成下列先決條件步驟，才能將您的[!DNL Algolia]帳戶連線至Experience Platform。

1. 使用[[!DNL Algolia] 儀表板](https://dashboard.algolia.com/users/sign_up)登入您的[!DNL Algolia]帳戶或建立新帳戶。
2. [準備您的索引](https://www.algolia.com/doc/guides/sending-and-managing-data/prepare-your-data/in-depth/prepare-data-in-depth/)。
3. [設定您的多面向](https://www.algolia.com/doc/guides/managing-results/refine-results/faceting/)。
4. [傳送使用者事件](https://www.algolia.com/doc/guides/sending-events/getting-started/)。
5. [個人化您的索引](https://www.algolia.com/doc/guides/personalization/advanced-personalization/configure/setup/indices/)。

### 在Experience Platform上設定許可權

您必須同時為您的帳戶啟用&#x200B;**[!UICONTROL 檢視來源]**&#x200B;和&#x200B;**[!UICONTROL 管理來源]**&#x200B;許可權，才能將您的[!DNL Algolia]帳戶連線至Experience Platform。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/abac/ui/permissions.md)。

### IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 將您的[!DNL Algolia]帳戶連線至Experience Platform

完成先決條件後，您就可以繼續進行下一個步驟，並[將您的 [!DNL Algolia] 帳戶連線至Experience Platform](../../tutorials/ui/create/data-partners/algolia-user-profiles.md)。
