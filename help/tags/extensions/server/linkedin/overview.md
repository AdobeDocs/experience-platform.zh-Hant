---
title: Linkedin轉換API事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能可讓您測量Linkedin行銷活動的效能。
last-substantial-update: 2023-10-25T00:00:00Z
source-git-commit: e1ed18aa79abae70974df1845c211a00390ecca4
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---

# [!DNL LinkedIn] Conversions API 擴充功能

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) 是一種轉換追蹤工具，可在來自廣告商伺服器的行銷資料之間建立直接連線，並且 [!DNL LinkedIn]. 這可讓廣告商評估其效益 [!DNL LinkedIn] 行銷活動，無論轉換的位置為何，都可使用此資訊來推動行銷活動最佳化。 此 [!DNL LinkedIn Conversions API] 擴充功能可透過更完整的歸因、改善資料可靠性和更理想的傳送方式，協助加強效能並降低每項動作的成本。

## 先決條件 {#prerequisites}

您必須在 [!DNL LinkedIn] 行銷活動廣告帳戶。 [!DNL Adobe] 建議在交談規則名稱開頭加入「CAPI」，將其與您可能已設定的其他轉換規則型別區分開來。

### 建立密碼和資料元素

建立新的 [!DNL LinkedIn] [事件轉送密碼](../../../ui/event-forwarding/secrets.md) 並為它提供唯一名稱，以表示驗證成員。 這將用於驗證與您的帳戶的連線，同時保持值的安全。

下一個， [建立資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 [!UICONTROL 核心] 擴充功能和 [!UICONTROL 密碼] 資料元素型別以參照 `LinkedIn` 您剛才建立的密碼。

## 安裝並設定 [!DNL LinkedIn] 副檔名 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選取要編輯的現有屬性。

選取 **[!UICONTROL 擴充功能]** ，位於左側導覽器中。 在 **[!UICONTROL 目錄]** 索引標籤中，選取 **[!UICONTROL linkedIn]** 擴充功能，然後選取 **[!UICONTROL 安裝]**.

![擴充功能目錄顯示 [!DNL LinkedIn] 擴充卡醒目提示安裝。](../../../images/extensions/server/linkedin/install-extension.png)

在下一個畫面，將您先前建立的資料元素密碼輸入至 `Access Token` 欄位。 資料元素密碼將包含 [!DNL LinkedIn] OAuth 2 Token。 選取 **[!UICONTROL 儲存]** 完成後。

![此 [!DNL LinkedIn] 擴充功能設定頁面，其中包含 [!UICONTROL 存取權杖] 欄位和 [!UICONTROL 儲存] 反白顯示。](../../../images/extensions/server/linkedin/configure-extension.png)

## 建立 [!DNL Send Conversion] 規則 {#tracking-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，以判斷將事件傳送至的時間和方式 [!DNL LinkedIn].

建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 在事件轉送屬性中。 在 **[!UICONTROL 動作]**，新增動作並將擴充功能設為 **[!UICONTROL linkedIn]**. 接下來，選取 **[!UICONTROL 傳送網頁轉換]** 針對 **[!UICONTROL 動作型別]**.

![「事件轉送屬性規則」檢視中，醒目顯示新增事件轉送規則動作設定所需的欄位。](../../../images/extensions/server/linkedin/linkedin-event-action.png)

選取後，會出現其他控制項以進一步設定事件。 選取 **[!UICONTROL 保留變更]** 以儲存規則。

**[!UICONTROL 使用者資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 電子郵件] | 與轉換事件相關之連絡人的電子郵件地址。 除非提供的值已經是SHA256字串，否則電子郵件值將會以SHA256中的擴充功能代碼編碼。 |
| [!UICONTROL linkedIn第一方廣告追蹤UUID] | 這是第一方Cookie ID。 廣告商需要啟用來自的增強轉換追蹤 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) 為了啟用附加點選ID引數的第一方Cookie `li_fat_id` 至按一下URL。 |
| [!UICONTROL 客戶資訊資料] | 此欄位包含具有額外屬性的JSON物件，將隨訊息一併傳送。<br><br>在 **[!UICONTROL 原始]** 選項，您可以將JSON物件直接貼到提供的文字欄位中，或選取資料元素圖示(![資料集圖示](../../../images/extensions/server/aws/data-element-icon.png))從現有資料元素清單中選取以代表資料。<br><br>您也可以使用 **[!UICONTROL JSON索引鍵值配對編輯器]** 用於透過UI編輯器手動新增每個索引鍵/值組的選項。 每個值都可表示為原始輸入，或是可改為選取資料元素。 接受的索引鍵值為： `firstName`， `lastName`， `companyName`， `title` 和 `country`. |

{style="table-layout:auto"}

![此 [!DNL User Data] 區段顯示輸入欄位的範例資料。](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL 轉換資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 轉換] | 在中建立的轉換規則ID [linkedIn行銷活動管理員](https://www.linkedin.com/help/lms/answer/a1657171) 或透過 [!DNL LinkedIn Campaign Manager]. |
| [!UICONTROL 轉換時間] | 轉換事件發生的每個時間戳記（毫秒）。 <br><br> 注意：如果您的來源以秒為單位記錄轉換時間戳記，請在結尾插入000以將其轉換為毫秒。 |
| [!UICONTROL 貨幣] | ISO格式的貨幣代碼。 |
| [!UICONTROL 數量] | 十進位字串中的轉換值（例如「100.05」）。 |
| [!UICONTROL 事件ID] | 廣告商產生的唯一ID可指出每個事件。 這是選用欄位，用於重複資料刪除。 |

{style="table-layout:auto"}

![此 [!DNL Conversion Data] 區段，顯示欄位中的範例資料。](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL 設定覆寫]**

>注意
>
>此 [!UICONTROL 設定覆寫] 欄位可讓使用者設定其他 [!DNL LinkedIn] 每個規則的存取權杖，允許每個規則使用可能存取不同存取權的存取權杖 [!DNL LinkedIn] 廣告帳戶。

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 存取權杖] | 此 [!DNL LinkedIn] 存取權杖。 |

![此 [!DNL Configuration Overrides] 區段，顯示欄位中的範例資料輸入。](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## 後續步驟

本指南說明如何將資料傳送至 [!DNL LinkedIn] 使用 [!DNL LinkedIn Conversions API] 事件轉送擴充功能。 如需事件轉送功能的詳細資訊，請參閱 [!DNL Adobe Experience Platform]，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
