---
title: Linkedin轉換API事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能可讓您測量Linkedin行銷活動的效能。
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# [!DNL LinkedIn] Conversions API 擴充功能

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api)是一種轉換追蹤工具，可在來自廣告商伺服器的行銷資料與[!DNL LinkedIn]之間建立直接連線。 這可讓廣告商評估其[!DNL LinkedIn]行銷活動的成效，無論轉換的位置為何，並利用此資訊來推動行銷活動最佳化。 [!DNL LinkedIn Conversions API]擴充功能可透過更完整的歸因、改善資料可靠性和更理想的傳遞方式，協助加強效能並降低每個動作的成本。

## 先決條件 {#prerequisites}

您必須在您的[!DNL LinkedIn Campaign Manager]帳戶中[建立轉換規則](https://www.linkedin.com/help/lms/answer/a1657171)。 [!DNL Adobe]建議在交談規則名稱的開頭加入「CAPI」，將其與您可能已設定的其他轉換規則型別區分開來。

### 建立密碼和資料元素

建立新的[!DNL LinkedIn] [事件轉送密碼](../../../ui/event-forwarding/secrets.md)，並提供代表驗證成員的唯一名稱。 這將用於驗證與您的帳戶的連線，同時保持值的安全。

接著，[使用[!UICONTROL Core]擴充功能和[!UICONTROL Secret]資料元素型別，建立資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element)以參考您剛才建立的`LinkedIn`密碼。

## 安裝並設定[!DNL LinkedIn]擴充功能 {#install}

若要安裝擴充功能，[請建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties)或選取要編輯的現有屬性。

在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤中，選取&#x200B;**[!UICONTROL LinkedIn]**&#x200B;擴充功能，然後選取&#x200B;**[!UICONTROL 安裝]**。

![顯示[!DNL LinkedIn]擴充卡醒目提示安裝的擴充功能目錄。](../../../images/extensions/server/linkedin/install-extension.png)

在下一個畫面中，於`Access Token`欄位中輸入您先前建立的資料元素密碼。 資料元素密碼將包含您的[!DNL LinkedIn] OAuth 2權杖。 完成時選取&#x200B;**[!UICONTROL 儲存]**。

![包含[!UICONTROL 存取權杖]欄位和[!UICONTROL 儲存]的[!DNL LinkedIn]延伸設定頁面已反白顯示。](../../../images/extensions/server/linkedin/configure-extension.png)

## 建立[!DNL Send Conversion]規則 {#tracking-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，以判斷將事件傳送至[!DNL LinkedIn]的時間和方式。

在您的事件轉送屬性中建立新的事件轉送[規則](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL 動作]**&#x200B;底下，新增動作並將擴充功能設為&#x200B;**[!UICONTROL LinkedIn]**。 接著，針對&#x200B;**[!UICONTROL 動作型別]**&#x200B;選取&#x200B;**[!UICONTROL 傳送轉換]**。

![「事件轉送屬性規則」檢視中，醒目顯示新增事件轉送規則動作設定所需的欄位。](../../../images/extensions/server/linkedin/linkedin-event-action.png)

選取後，會出現其他控制項以進一步設定事件。 選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以儲存規則。

**[!UICONTROL 使用者資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 電子郵件] | 與轉換事件相關之連絡人的電子郵件地址。 除非提供的值已經是SHA256字串，否則電子郵件值將會以SHA256中的擴充功能代碼編碼。 |
| [!UICONTROL LinkedIn第一方廣告追蹤UUID] | 這是第一方Cookie ID。 廣告商需要啟用來自[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag)的增強型轉換追蹤，才能啟用將點選ID引數`li_fat_id`附加至點選URL的第一方Cookie。 |
| [!UICONTROL 客戶資訊資料] | 此欄位包含具有額外屬性的JSON物件，將隨訊息一併傳送。<br><br>在&#x200B;**[!UICONTROL 原始]**&#x200B;選項下，您可以將JSON物件直接貼上到提供的文字欄位中，或者您可以選取資料元素圖示（![資料集圖示](/help/images/icons/database.png)），從現有資料元素清單中選取以代表資料。<br><br>您也可以使用&#x200B;**[!UICONTROL JSON索引鍵/值組編輯器]**&#x200B;選項，透過UI編輯器手動新增每個索引鍵/值組。 每個值都可表示為原始輸入，或是可改為選取資料元素。 接受的機碼值為： `firstName`、`lastName`、`companyName`、`title`和`country`。 |

{style="table-layout:auto"}

![顯示輸入欄位之範例資料的[!DNL User Data]區段。](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL 轉換資料]**

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 轉換] | 在[LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171)中建立的轉換規則識別碼。 選取轉換規則以取得ID，然後從瀏覽器URL （例如，`/campaignmanager/accounts/508111232/conversions/15588877`）複製ID做為`/conversions/<id>`。 |
| [!UICONTROL 轉換時間] | 轉換事件發生的每個時間戳記（毫秒）。 <br><br>注意：如果您的來源以秒為單位記錄轉換時間戳記，請在結尾插入000以將其轉換為毫秒。 |
| [!UICONTROL 貨幣] | ISO格式的貨幣代碼。 |
| [!UICONTROL 金額] | 十進位字串中的轉換值（例如「100.05」）。 |
| [!UICONTROL 事件識別碼] | 廣告商產生的唯一ID可指出每個事件。 這是選擇性欄位，用於[重複資料刪除](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02)。 |

{style="table-layout:auto"}

![顯示欄位範例資料的[!DNL Conversion Data]區段。](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL 設定覆寫]**

>注意
>
>[!UICONTROL 設定覆寫]欄位可讓使用者在每個規則上設定不同的[!DNL LinkedIn]存取權杖，讓每個規則使用可能存取不同[!DNL LinkedIn]廣告帳戶的存取權杖。

| 輸入 | 說明 |
| --- | --- |
| [!UICONTROL 存取Token] | [!DNL LinkedIn]存取權杖。 |

![顯示欄位中輸入範例資料的[!DNL Configuration Overrides]區段。](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## 後續步驟

本指南說明如何使用[!DNL LinkedIn Conversions API]事件轉送擴充功能將資料傳送至[!DNL LinkedIn]。 如需[!DNL Adobe Experience Platform]中事件轉送功能的詳細資訊，請閱讀[事件轉送概觀](../../../ui/event-forwarding/overview.md)。

如需使用Experience Platform偵錯工具與事件轉送監視工具對實作進行偵錯的詳細資訊，請閱讀[Adobe Experience Platform Debugger總覽](../../../../debugger/home.md)與[監視事件轉送中的活動](../../../ui/event-forwarding/monitoring.md)。
