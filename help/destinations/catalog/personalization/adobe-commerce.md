---
title: Adobe Commerce目的地聯結器
description: 瞭解Adobe Commerce和Real-Time CDP商家如何提供高度相關的網站內容和促銷活動，並根據Real-Time CDP中建立和管理之客戶對象進行自訂，進而個人化購物體驗。
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 3%

---

# Adobe Commerce連線 {#adobe-commerce}

## 概觀 {#overview}

[!DNL Adobe Commerce]目的地聯結器可讓您選取一或多個Real-Time CDP對象，以啟用至您的[!DNL Adobe Commerce]帳戶，為購物者提供動態的個人化體驗。 在[!DNL Adobe Commerce]內，您可以選取那些Real-Time CDP對象，以個人化購物車中的獨特選件，例如「購買2 get 1免費」。 您也可以顯示主圖橫幅，並透過促銷優惠修改產品定價，所有優惠都根據Adobe Real-Time CDP受眾自訂。

## 先決條件 {#prerequisites}

已購買Real-Time CDP Prime或Ultimate和Adobe Commerce的客戶可在目標目錄中取得此聯結器。

若要使用此目的地連線，請確定您有以下存取權：

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)。 您可以存取開發人員主控台，檢視在Adobe Commerce中[完成擴充功能組態](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=zh-Hant#configure-the-extension)所需的服務帳戶和認證資訊。
- [Adobe Commerce Cloud 2.4.4版或更新版本](https://business.adobe.com/products/magento/magento-commerce.html)

在Experience Platform中建立下列專案：

- [結構描述](../../../xdm/schema/composition.md)。 您建立的結構描述代表您計畫從Adobe Commerce擷取的資料。 [深入瞭解](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=zh-Hant)如何建立包含Commerce特定欄位群組的結構描述。
- [資料集](../../../catalog/datasets/user-guide.md#create)。 資料集是資料集合的儲存和管理結構。 您會使用先前建立的結構描述建立此資料集。
- [資料流](../../../datastreams/overview.md#create)。 可讓資料從Adobe Experience Platform流向其他Adobe DX產品的ID。 此ID必須與您特定Adobe Commerce執行個體中的特定網站相關聯。 當您建立此資料流時，請指定您在上面建立的XDM結構描述。

完成先決條件後，請連線至[!DNL Commerce]目的地。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到[!DNL Adobe Commerce]目的地：

1. 在[Experience Platform介面](https://experience.adobe.com/platform/)中，前往&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**。
1. 選取&#x200B;**[!UICONTROL Personalization]**。
1. 選取Adobe Commerce目的地以反白顯示，然後選取&#x200B;**[!UICONTROL 設定]**。
1. 請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

- **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
- **[!UICONTROL 描述]**：輸入目的地的描述。 例如，您可以提及要將此目的地用於哪個行銷活動。 此欄位為選用。
- **[!UICONTROL 整合別名]**：此值會作為JSON物件名稱傳送到Experience Platform Web SDK。
- **[!UICONTROL 資料串流識別碼]**：這會判斷哪個資料收集資料串流包含頁面回應中所包含的對象。 下拉選單僅顯示已啟用目的地設定的資料流。如需詳細資訊，請參閱[設定資料串流](../../../datastreams/overview.md)。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 將對象啟用至[!DNL Commerce]目的地 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

閱讀[啟用設定檔和受眾以設定檔要求目的地](../../ui/activate-edge-personalization-destinations.md)，以取得啟用受眾至[!DNL Commerce]目的地的指示。

## [!DNL Adobe Commerce]中的後續步驟

現在您已在Experience Platform中設定[!DNL Commerce]目的地，您必須在[!DNL Commerce]中安裝[!DNL Audience Activation]擴充功能，並設定[!DNL Commerce Admin]以匯入您建立的Real-Time CDP對象。 請參閱[[!DNL Commerce] 檔案](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=zh-Hant)以瞭解更多資訊。

## 驗證Commerce中的對象啟用 {#exported-data}

在您的[!DNL Adobe Commerce]帳戶啟用Real-Time CDP對象後，您將看到這些對象在您前往&#x200B;_管理員_&#x200B;側邊欄，然後前往&#x200B;**[!UICONTROL 客戶]** > **[!UICONTROL Real-Time CDP對象]**&#x200B;時可用。

![Real-Time CDP受眾控制面板](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
