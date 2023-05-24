---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標；sendgrid;sendgrid目標
title: SendGrid連接
description: SendGrid目標允許您導出第一方資料，並在SendGrid中根據您的業務需要激活它。
exl-id: 6f22746f-2043-4a20-b8a6-097d721f2fe7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 2%

---

# [!DNL SendGrid] 連接

## 總覽 {#overview}

[發送網格](https://www.sendgrid.com) 是用於交易和營銷電子郵件的常用客戶溝通平台。

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [[!DNL SendGrid Marketing Contacts API]](https://api.sendgrid.com/v3/marketing/contacts)，允許您導出第一方電子郵件配置檔案，並在新的SendGrid網段中根據您的業務需要激活它們。

SendGrid使用API承載令牌作為與SendGrid API通信的驗證機制。

## 先決條件 {#prerequisites}

在開始配置目標之前，需要以下項。

1. 您需要有SendGrid帳戶。
   * 轉到SendGrid [註冊](https://signup.sendgrid.com/) 頁，以註冊和建立SendGrid帳戶（如果尚未）。
1. 登錄到SendGrid門戶後，還需要生成API令牌。
1. 導航到SendGrid網站並訪問 **[!DNL Settings]** > **[!DNL API Keys]** 的子菜單。 或者，請參閱 [SendGrid文檔](https://app.sendgrid.com/settings/api_keys) 訪問SendGrid應用中的相應部分。
1. 最後，選擇 **[!DNL Create API Key]** 按鈕
   * 請參閱 [SendGrid文檔](https://docs.sendgrid.com/ui/account-and-settings/api-keys#creating-an-api-key)，但需要指導您執行哪些操作。
   * 如果希望以寫程式方式生成API密鑰，請參閱 [SendGrid文檔](https://docs.sendgrid.com/api-reference/api-keys/create-api-keys)。

![](../../assets/catalog/email-marketing/sendgrid/01-api-key.jpg)

在將資料激活到SendGrid目標之前，必須 [架構](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hant)的 [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), [段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立 [!DNL Experience Platform]。 另請參閱 [限制](#limits) 的下一頁。

>[!IMPORTANT]
>
>* 用於從電子郵件配置檔案建立郵件清單的SendGrid API要求在每個配置檔案中提供唯一的電子郵件地址。 無論是否將其用作 *電子郵件* 或 *備用電子郵件*。 由於SendGrid連接支援電子郵件值和備用電子郵件值的映射，因此請確保在每個配置檔案中使用的所有電子郵件地址都應是唯一的 *資料集*。 否則，當電子郵件配置檔案被發送到SendGrid時，將導致錯誤，且該電子郵件配置檔案在資料導出中將不存在。
>
>* 當前，當從Experience Platform中的段中刪除配置檔案時，沒有從SendGrid中刪除配置檔案的功能。


## 支援的身份 {#supported-identities}

SendGrid支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 電子郵件地址 | 請注意，支援純文字檔案和SHA256散列電子郵件地址 [!DNL Adobe Experience Platform]。 如果「體驗平台」源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。<br/><br/> 請注意 **發送網格** 不支援散列的電子郵件地址，因此只會將未轉換的純文字檔案資料發送到目標。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

為幫助您更好地瞭解應如何以及何時使用SendGrid目標，以下是示例使用案例 [!DNL Experience Platform] 客戶可以通過使用此目標來解決問題。

### 為多個市場營銷活動建立市場營銷清單

使用SendGrid的市場營銷團隊可以在SendGrid內建立郵件清單，並用電子郵件地址填充該清單。 現在在SendGrid中建立的郵件清單隨後可用於多個市場營銷活動。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

1. 在 [!DNL Adobe Experience Platform] 控制台，導航至 **目標**。

1. 選擇 **目錄** 頁籤和搜索 *發送網格*。 然後選擇 **設定**。 建立到目標的連接後，UI標籤將更改為 **激活段**。
   ![](../../assets/catalog/email-marketing/sendgrid/02-catalog.jpg)

1. 將顯示一個嚮導，幫助您配置SendGrid目標。 通過選擇 **配置新目標**。
   ![](../../assets/catalog/email-marketing/sendgrid/03.jpg)

1. 選擇 **新帳戶** 的 **持有者令牌** 值。 此值為SendGrid *API密鑰* 前面提到的 [先決條件部分](#prerequisites)。
   ![](../../assets/catalog/email-marketing/sendgrid/04.jpg)

1. 選擇 **連接到目標**。 如果SendGrid *API密鑰* 您提供的是有效的，UI顯示 **已連接** 狀態為綠色複選標籤，然後可以繼續執行下一步以填寫附加資訊欄位。

![](../../assets/catalog/email-marketing/sendgrid/05.jpg)

### 填寫目標詳細資訊 {#destination-details}

同時 [設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:可選的說明，將幫助您在將來確定此目標。

![](../../assets/catalog/email-marketing/sendgrid/06.jpg)

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

有關特定於此目標的詳細資訊，請參閱以下映像。

1. 選擇一個或多個要導出到SendGrid的段。
   ![](../../assets/catalog/email-marketing/sendgrid/11.jpg)

1. 在 **[!UICONTROL 映射]** 步驟，在選擇 **[!UICONTROL 添加新映射]**，將顯示映射頁，將源XDM欄位映射到SendGrid API目標欄位。 下面的影像演示了如何在Experience Platform和SendGrid之間映射標識命名空間。 請確保 **[!UICONTROL 源欄位]** *電子郵件* 應映射到 **[!UICONTROL 目標欄位]** *外部ID* 如下所示。
   ![](../../assets/catalog/email-marketing/sendgrid/13.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/14.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/15.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/16.jpg)

1. 同樣，映射所需 [!DNL Adobe Experience Platform] 要導出到SendGrid目標的屬性。
   ![](../../assets/catalog/email-marketing/sendgrid/17.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/18.jpg)

1. 完成映射後，選擇 **[!UICONTROL 下一個]** 進入審閱螢幕。
   ![](../../assets/catalog/email-marketing/sendgrid/22.png)

1. 選擇 **[!UICONTROL 完成]** 完成設定。
   ![](../../assets/catalog/email-marketing/sendgrid/23.jpg)

可為 [SendGrid市場營銷聯繫人>添加或更新聯繫人API](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact) 下。

| 源欄位 | 目標欄位 | 類型 | 說明 | 限制 |
|---|---|---|---|---|
| xdm:<br/> homeAddress.street1 | xdm:<br/> 地址_行_1 | 字串 | 地址的第一行。 | 最大長度：<br/> 100個字元 |
| xdm:<br/> homeAddress.street2 | xdm:<br/> 地址_行_2 | 字串 | 地址的可選第二行。 | 最大長度：<br/> 100個字元 |
| xdm:<br/> _extcondev.alternate電子郵件 | xdm:<br/> 備用電子郵件 | 字串陣列 | 與聯繫人關聯的其他電子郵件。 | <ul><li>最大：5項</li><li>最小：0個項目</li></ul> |
| xdm:<br/> homeAddress.city | xdm:<br/> 城市 | 字串 | 聯絡人所在的城市。 | 最大長度：<br/> 60個字元 |
| xdm:<br/> homeAddress.country | xdm:<br/> 鄉 | 字串 | 聯繫人所在的國家。 可以是全名或縮寫。 | 最大長度：<br/> 50個字元 |
| identityMap:<br/> 電子郵件 | 標識：<br/> 外部ID | 字串 | 聯繫人的主要電子郵件。 這必須是有效的電子郵件。 | 最大長度：<br/> 254個字元 |
| xdm:<br/> person.name.firstName | xdm:<br/> 名字 | 字串 | 聯繫人姓名 | 最大長度：<br/> 50個字元 |
| xdm:<br/> person.name.lastName | xdm:<br/> 姓氏 | 字串 | 聯繫人的姓 | 最大長度：<br/> 50個字元 |
| xdm:<br/> homeAddress.postalCode | xdm:<br/> 郵遞區號 | 字串 | 聯繫人的郵遞區號或其他郵遞區號。 |  |
| xdm:<br/> homeAddress.state省 | xdm:<br/> 省/自治區 | 字串 | 聯繫人所在的州、省或地區。 | 最大長度：<br/> 50個字元 |

## 驗證SendGrid中的資料導出 {#validate}

要驗證您是否正確設定了目標，請執行以下步驟：

1. 選擇 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]** 導航至目標清單。
   ![](../../assets/catalog/email-marketing/sendgrid/25.jpg)

1. 選擇目標並驗證狀態是否為 **[!UICONTROL 啟用]**。
   ![](../../assets/catalog/email-marketing/sendgrid/26.jpg)

1. 切換到 **[!DNL Activation data]** ，然後選擇段名稱。
   ![](../../assets/catalog/email-marketing/sendgrid/27.jpg)

1. 監視段摘要，並檢查配置檔案計數是否與在資料集中建立的計數相對應。
   ![](../../assets/catalog/email-marketing/sendgrid/28.jpg)

1. 的 [SendGrid市場營銷清單>建立清單API](https://docs.sendgrid.com/api-reference/lists/create-list) 用於通過連接SendGrid的 *清單名稱* 屬性和資料導出的時間戳。 導航到SendGrid站點並檢查是否建立了符合名稱模式的新聯繫人清單。
   ![](../../assets/catalog/email-marketing/sendgrid/29.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/30.jpg)

1. 選擇新建立的聯繫人清單，並檢查您建立的資料集中的新電子郵件記錄是否正在新聯繫人清單中填充。

1. 此外，還檢查幾封電子郵件以驗證欄位映射是否正確。
   ![](../../assets/catalog/email-marketing/sendgrid/31.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/32.jpg)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

此SendGrid目標利用以下API:
* [SendGrid市場營銷清單>建立清單API](https://docs.sendgrid.com/api-reference/lists/create-list)
* [SendGrid市場營銷聯繫人>添加或更新聯繫人API](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact)

### 限制 {#limits}

* 的 [SendGrid市場營銷聯繫人>添加或更新聯繫人API](https://api.sendgrid.com/v3/marketing/contacts) 可以接受30,000個聯繫人，或6MB的資料（以較低者為準）。
