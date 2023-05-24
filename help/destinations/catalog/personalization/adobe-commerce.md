---
title: Adobe Commerce目的地連接器
description: 瞭解Adobe Commerce和Real-Time CDP商戶如何通過提供高度相關的網站內容和促銷來個性化購物體驗，這些內容和促銷針對Real-Time CDP內部構建和管理的客戶群進行了定制。
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 813a564eb02a5366945468ee689b2744e31baaa8
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 3%

---

# Adobe Commerce {#adobe-commerce}

## 總覽 {#overview}

的 [!DNL Adobe Commerce] 目標連接器允許您選擇一個或多個Real-Time CDP受眾以激活到您 [!DNL Adobe Commerce] 為購物者提供動態個性化體驗。 在 [!DNL Adobe Commerce]，然後您可以選擇這些Real-Time CDP受眾，以個性化購物車中的獨特優惠，如「購買2獲取1免費」。 您還可以顯示英雄橫幅，並通過促銷優惠修改產品定價，所有優惠都針對Adobe Real-Time CDP觀眾定制。

## 先決條件 {#prerequisites}

此連接器可在目的地目錄中為購買了Real-Time CDPPrime或旗艦版和Adobe Commerce的客戶提供。

要使用此目標連接，請確保您有權訪問：

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). 通過訪問開發人員控制台，您可以查看服務帳戶和所需的憑據資訊 [完成配置](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) 延長期的Adobe Commerce。
- [Adobe Commerce Cloud2.4.4版或更高版本](https://business.adobe.com/products/magento/magento-commerce.html)

在Experience Platform中，建立以下內容：

- [方案](../../../xdm/schema/composition.md). 您建立的架構表示您計畫從Adobe Commerce接收的資料。 [瞭解更多資訊](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) 關於如何建立包含特定於Commerce的欄位組的架構。
- [資料集](../../../catalog/datasets/user-guide.md#create). 資料集是用於資料集合的儲存和管理構造。 您可以從上面建立的架構建立此資料集。
- [資料流](../../../edge/datastreams/overview.md#create)。 允許資料從Adobe Experience Platform流到其他AdobeDX產品的ID。 此ID必須與您特定Adobe Commerce實例中的特定網站關聯。 建立此資料流時，請指定上面建立的XDM架構。

完成先決條件後，請連接到 [!DNL Commerce] 目標。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

連接到 [!DNL Adobe Commerce] 目標：

1. 在 [平台介面](https://experience.adobe.com/platform/)，轉到 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]**。
1. 選擇 **[!UICONTROL 個性化]**。
1. 選擇要突出顯示的Adobe Commerce目標，然後選擇 **[!UICONTROL 設定]**。
1. 按照中介紹的步驟操作 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

- **[!UICONTROL 名稱]**:填寫此目標的首選名稱。
- **[!UICONTROL 說明]**:輸入目標的說明。 例如，您可以提及您為此目標使用的市場活動。 此欄位為可選欄位。
- **[!UICONTROL 整合別名]**:此值將作為JSON對象名發送到Experience PlatformWeb SDK。
- **[!UICONTROL 資料流ID]**:這將確定哪些資料收集資料流包含響應頁面中包含的訪問群體。 下拉式選單僅顯示已啟用目的地設定的資料流。請參閱 [配置資料流](../../../edge/datastreams/overview.md) 的子菜單。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將觀眾激活到 [!DNL Commerce] 目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以配置請求目標](../../ui/activate-profile-request-destinations.md) 有關激活觀眾的說明 [!DNL Commerce] 目標。

## 後續步驟 [!DNL Adobe Commerce]

現在您已配置 [!DNL Commerce] 目標Experience Platform中，您需要安裝 [!DNL Audience Activation] 擴展 [!DNL Commerce] 並配置 [!DNL Commerce Admin] 導入您建立的Real-Time CDP觀眾。 查看 [[!DNL Commerce] 文檔](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) 來瞭解更多資訊。

## 驗證Commerce中的受眾激活 {#exported-data}

激活Real-Time CDP觀眾後 [!DNL Adobe Commerce] 帳戶，當您轉到 _管理_ 邊欄，然後轉到 **[!UICONTROL 客戶]** > **[!UICONTROL 即時CDP受眾]**。

![Real-Time CDP觀眾儀表板](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](/help/data-governance/home.md)。
