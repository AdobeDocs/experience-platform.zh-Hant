---
title: 中繼轉換API擴充功能概觀
description: 了解Adobe Experience Platform中用於事件轉送的中繼轉換API擴充功能。
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 擴充功能概觀

此 [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) 可讓您將伺服器端行銷資料連結至 [!DNL Meta] 技術，以最佳化您的廣告鎖定目標、降低每個動作的成本並衡量結果。 事件會連結至 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID和的處理方式與用戶端事件類似。

使用 [!DNL Meta Conversions API] 擴充功能，您可以在 [事件轉送](../../../ui/event-forwarding/overview.md) 將資料傳送至的規則 [!DNL Meta] 來自Adobe Experience Platform Edge Network。 本檔案說明如何安裝擴充功能，以及在事件轉送中使用其功能 [規則](../../../ui/managing-resources/rules.md).

## 先決條件

強烈建議使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 分別從用戶端和伺服器端共用和傳送相同事件，因為這可能有助於復原未擷取的事件 [!DNL Meta Pixel]. 安裝之前 [!DNL Conversions API] 擴充功能，請參閱 [[!DNL Meta Pixel] 擴充功能](../../client/meta/overview.md) 以了解如何將其整合至用戶端標籤實施的步驟。

>[!NOTE]
>
>的 [事件去重複化](#deduplication) 本檔案稍後將說明確保不會使用相同事件兩次的步驟，因為同一事件可能會從瀏覽器和伺服器接收。

若要使用 [!DNL Conversions API] 擴充功能，您必須擁有事件轉送的存取權，且具備有效 [!DNL Meta] 有權存取的帳戶 [!DNL Ad Manager] 和 [!DNL Event Manager]. 具體來說，您必須複製現有 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (或 [建立新 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) )，以便將擴充功能設定至您的帳戶。

## 安裝擴充功能

若要安裝 [!DNL Meta Conversions API] 擴充功能，請導覽至資料收集UI或Experience PlatformUI，然後選取 **[!UICONTROL 事件轉送]** 從左側導覽。 從此處，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需屬性後，請選取 **[!UICONTROL 擴充功能]** 在左側導覽器中，選取 **[!UICONTROL 目錄]** 標籤。 搜尋 [!UICONTROL 中繼轉換API] 卡片，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL 安裝] 按鈕 [!UICONTROL 中繼轉換API] 擴充功能。](../../../images/extensions/server/meta/install.png)

在顯示的設定檢視中，您必須提供 [!DNL Pixel] 您先前複製的ID，將擴充功能連結至您的帳戶。 您可以直接將ID貼入輸入，或改用資料元素。

您也需要提供存取權杖，才能使用 [!DNL Conversions API] 具體來說。 請參閱 [!DNL Conversions API] 檔案 [產生存取權杖](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 以取得此值的步驟。

完成後，請選取 **[!UICONTROL 儲存]**

![此 [!DNL Pixel] 在擴充功能組態檢視中以資料元素形式提供的ID。](../../../images/extensions/server/meta/configure.png)

擴充功能已安裝，您現在可以在事件轉送規則中運用其功能。

## 設定事件轉送規則 {#rule}

本節說明如何使用 [!DNL Conversions API] 一般事件轉送規則中的擴充功能。 實際上，您應設定數個規則，以傳送所有已接受的 [標準事件](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] 和 [!DNL Conversions API].

>[!NOTE]
>
>事件應為 [即時傳送](https://www.facebook.com/business/help/379226453470947?id=818859032317965) 或盡可能接近即時，以更佳的廣告促銷活動最佳化。

開始建立新的事件轉送規則，並視需要設定其條件。 選取規則的動作時，請選取 **[!UICONTROL 中繼轉換API擴充功能]** 對於擴充功能，請選取 **[!UICONTROL 傳送轉換API事件]** （針對動作類型）。

![此 [!UICONTROL 傳送頁面檢視] 在資料收集UI中為規則選取的動作類型。](../../../images/extensions/server/meta/select-action.png)

控制項可讓您設定要傳送至的事件資料 [!DNL Meta] 透過 [!DNL Conversions API]. 這些選項可直接輸入到提供的輸入中，或者您可以選取現有資料元素來代表值。 設定選項分為四個主要部分，如下所述。

| 設定區段 | 說明 |
| --- | --- |
| [!UICONTROL 伺服器事件參數] | 事件的一般資訊，包括發生時間和觸發事件的來源動作。 請參閱 [!DNL Meta] 開發人員檔案，以取得 [標準事件參數](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) 接受 [!DNL Conversions API].<br><br>如果您同時使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 若要傳送事件，請務必同時包含 **[!UICONTROL 事件名稱]** (`event_name`)和 **[!UICONTROL 事件ID]** (`event_id`)，因為這些值會用於 [事件去重複化](#deduplication).<br><br>您也可以選擇 **[!UICONTROL 啟用有限的資料使用]** 以協助遵守客戶選擇退出。 請參閱 [!DNL Conversions API] 檔案 [資料處理選項](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 以取得此功能的詳細資訊。 |
| [!UICONTROL 客戶資訊參數] | 用於將事件歸因給客戶的使用者身分資料。 其中有些值必須先經過雜湊處理，才能傳送至API。<br><br>為確保良好的通用API連線和高事件符合品質(EMQ)，建議您全部傳送 [接受的客戶資訊參數](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) 與伺服器事件一起使用。 這些參數也應為 [根據其重要性和對EMQ的影響來排定優先順序](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL 自訂資料] | 要用於廣告傳送最佳化的其他資料，以JSON物件的形式提供。 請參閱 [[!DNL Conversions API] 檔案](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) ，以了解此對象的接受屬性。<br><br>如果您要傳送購買事件，必須使用此區段來提供必要的屬性 `currency` 和 `value`. |
| [!UICONTROL 測試事件] | 此選項用於驗證您的配置是否導致接收伺服器事件 [!DNL Meta] 如預期。 若要使用此功能，請選取 **[!UICONTROL 以測試事件的形式傳送]** 核取方塊，然後在下方輸入中提供您所選取的測試事件程式碼。 部署事件轉送規則後，如果您正確設定擴充功能和動作，應該會看到活動出現在 **[!DNL Test Events]** 檢視 [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

完成後，請選取 **[!UICONTROL 保留變更]** 將動作新增至規則設定。

![[!UICONTROL 保留變更] 正在為操作配置選擇。](../../../images/extensions/server/meta/keep-changes.png)

對規則感到滿意時，請選取 **[!UICONTROL 儲存至程式庫]**. 最後，發佈新的事件轉送 [建置](../../../ui/publishing/builds.md) 啟用對程式庫所做的變更。

## 事件重複資料刪除 {#deduplication}

如 [必要條件一節](#prerequisites)，建議您同時使用 [!DNL Meta Pixel] 標籤擴充功能和 [!DNL Conversions API] 事件轉送擴充功能，在備援設定中從用戶端和伺服器傳送相同事件。 這有助於復原某個擴充功能或其他擴充功能未擷取的事件。

如果您從客戶端和伺服器發送不同的事件類型，且兩者之間沒有重疊，則不需要重複資料刪除。 不過，如果兩者共用任何單一事件 [!DNL Meta Pixel] 和 [!DNL Conversions API]，您必須確保這些重複事件已去除重複資料，以免對您的報表造成不利影響。

傳送共用事件時，請務必在您從用戶端和伺服器傳送的每個事件中加入事件ID和名稱。 收到多個ID和名稱相同的事件時， [!DNL Meta] 會自動採用數種策略來去除重複項目，並保留最相關的資料。 請參閱 [!DNL Meta] 檔案 [重複資料消除 [!DNL Meta Pixel] 和 [!DNL Conversions API] 事件](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) 以取得此程式的詳細資訊。

## 後續步驟

本指南說明如何將伺服器端事件資料傳送至 [!DNL Meta] 使用 [!DNL Meta Conversions API] 擴充功能。 在此處，建議您透過連接更多 [!DNL Pixels] 和共用更多事件（若適用）。 執行下列任一操作有助於進一步提高廣告效能：

* 連接任何其他 [!DNL Pixels] 尚未連線至 [!DNL Conversions API] 整合。
* 如果您只是透過 [!DNL Meta Pixel] 在用戶端上，將這些相同的事件傳送至 [!DNL Conversions API] 從伺服器端。

請參閱 [!DNL Meta] 檔案 [最佳實務 [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 以取得如何有效實作整合的詳細指引。 如需Adobe Experience Cloud中標籤和事件轉送的更一般資訊，請參閱 [標籤概述](../../../home.md).
