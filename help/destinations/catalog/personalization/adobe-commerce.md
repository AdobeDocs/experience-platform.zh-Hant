---
title: (Beta)Adobe Commerce Destination Connector
description: 了解Adobe Commerce和Real-Time CDP商家如何透過提供高度相關的網站內容和促銷活動(根據Real-Time CDP中建立和管理的客戶區段加以自訂)來個人化購物體驗。
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 638a778d1d999ab6a1726333f9cde0a0b4fad57b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 1%

---

# （測試版）Adobe Commerce連線 {#adobe-commerce}

## 總覽 {#overview}

>[!IMPORTANT]
> 
>此 **[!UICONTROL Adobe Commerce]** 連接器為測試版，僅適用於特定數量的客戶。

此 [!DNL Adobe Commerce] 目的地連接器可讓您選取一或多個要啟用的Real-Time CDP區段 [!DNL Adobe Commerce] 帳戶，為購物者提供動態的個人化體驗。 內 [!DNL Adobe Commerce]，您就可以選取這些Real-Time CDP區段，以個人化購物車中的獨特選件，例如「購買2即可免費獲得1」。 您也可以顯示主圖橫幅廣告，並透過促銷優惠方案修改產品定價，所有優惠方案皆自訂為Adobe Real-Time CDP區段。

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## 先決條件 {#prerequisites}

目的地目錄中提供此擴充功能，供已購買Real-Time CDP Prime或Ultimate及Adobe Commerce的精選測試版客戶使用。

測試版客戶應可存取：

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud 2.4.4版或更新版本](https://business.adobe.com/products/magento/magento-commerce.html)

在Experience Platform中，建立下列項目：

- [方案](../../../xdm/schema/composition.md). 您建立的結構代表您計畫從Adobe Commerce擷取的資料。 [深入了解](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) 關於如何建立包含商務專用欄位群組的結構。
- [資料集](../../../catalog/datasets/user-guide.md#create). 資料集是資料集合的儲存和管理結構。 您必須從上方建立的結構中建立此資料集。
- [資料流](../../../edge/datastreams/overview.md#create). 允許資料從Adobe Experience Platform流向其他AdobeDX產品的ID。 此ID必須與您特定Adobe Commerce例項內的特定網站相關聯。 建立此資料流時，請指定您在上方建立的XDM架構。

完成必要條件後，請連線至 [!DNL Commerce] 目的地。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

連線至 [!DNL Adobe Commerce] 目的地：

1. 在 [平台介面](https://experience.adobe.com/platform/)，前往 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**.
1. 選擇 **[!UICONTROL 個人化]**.
1. 選取要反白標示的Adobe Commerce目的地，然後選取 **[!UICONTROL 設定]**.
1. 請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

- **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
- **[!UICONTROL 說明]**:輸入目的地的說明。 例如，您可以提及您使用此目的地的促銷活動。 此欄位為選填欄位。
- **[!UICONTROL 整合別名]**:此值會以JSON物件名稱的形式傳送至Experience PlatformWeb SDK。
- **[!UICONTROL 資料流ID]**:這會決定要將區段納入頁面回應中的資料收集資料流。 下拉式功能表只會顯示已啟用目的地設定的資料流。 請參閱 [設定資料流](../../../edge/datastreams/overview.md) 以取得更多詳細資訊。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 將區段啟用至 [!DNL Commerce] 目的地 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至設定檔請求目的地](../../ui/activate-profile-request-destinations.md) 關於在 [!DNL Commerce] 目的地。

## 下一步 [!DNL Adobe Commerce]

現在您已設定 [!DNL Commerce] Experience Platform內的目的地，您必須設定 [!DNL Commerce Admin] 匯入您建立的Real-Time CDP區段。 請參閱 [[!DNL Commerce] 檔案](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/customer-segment-rtcdp.html) 了解更多。

## 驗證Commerce中的受眾啟動 {#exported-data}

在您將Real-Time CDP區段啟用至 [!DNL Adobe Commerce] 帳戶，您會在 [!DNL Admin] 建立購物車價格規則時：

![Adobe Commerce管理員](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](/help/data-governance/home.md).
