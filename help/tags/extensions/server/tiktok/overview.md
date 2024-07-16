---
title: AdobeTikTok網站事件API擴充功能整合
description: 此Adobe Experience Platform網頁事件API可讓您直接與TikTok共用網站互動。
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 2%

---

# [!DNL TikTok]網站事件API擴充功能總覽

[!DNL TikTok] events API是安全的[Edge Network伺服器API](/help/server-api/overview.md)介面，可讓您直接與[!DNL TikTok]共用您網站上使用者動作的資訊。 您可以使用[!DNL TikTok] Web Events API擴充功能，運用事件轉送規則，將資料從[!DNL Adobe Experience Platform Edge Network]傳送至[!DNL TikTok]。

## [!DNL TikTok]必要條件 {#prerequisites}

若要設定[!DNL TikTok]網頁事件API以使用[!DNL TikTok]事件API，您必須產生[!DNL TikTok]畫素代碼並存取權杖。

您必須擁有商務帳戶的有效[!DNL TikTok]，才能使用合作夥伴設定建立[!DNL TikTok]畫素。 移至[[!DNL TikTok] 企業註冊頁面](https://www.tiktok.com/business/en-US/solutions/business-account)進行註冊並建立帳戶（如果尚未建立帳戶）。

您必須登入您的企業帳戶，才能使用合作夥伴設定來設定[!DNL TikTok] Pixel。 請依照下列步驟執行此操作：

1. 導覽至&#x200B;**[!UICONTROL Assets]**&#x200B;索引標籤並選取&#x200B;**[!UICONTROL 事件]**。
2. 在「Web事件」底下，選取&#x200B;**[!UICONTROL 管理]**。
3. 選取&#x200B;**[!UICONTROL 設定網頁事件]**。
4. 選取&#x200B;**[!UICONTROL 夥伴安裝程式]**&#x200B;作為您的連線方法。

如需如何設定[!DNL TikTok]畫素的詳細資訊，請參閱[開始使用Pixel](https://ads.tiktok.com/help/article/get-started-pixel)指南。

成功建立畫素後，您就可以產生存取權杖。 若要這麼做，請導覽至「畫素」並選取「**[!UICONTROL 設定]**」標籤。 在Events API底下，選取&#x200B;**[!UICONTROL 產生存取權杖]**。

請參閱[[!DNL TikTok] 快速入門手冊](https://business-api.tiktok.com/portal/docs?id=1739584855420929)，以取得如何設定畫素程式碼和存取Token的詳細資訊。

## 安裝及設定[!DNL TikTok]網頁事件API擴充功能 {#install}

若要安裝擴充功能，請在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中，選取&#x200B;**[!UICONTROL TikTok Web Events API擴充功能]**，然後選取&#x200B;**[!UICONTROL 安裝]**。

![顯示[!DNL TikTok]擴充卡醒目提示安裝的擴充功能目錄。](../../../images/extensions/server/tiktok/install-extension.png)

在下一個畫面中，輸入您先前從[!DNL TikTok]廣告管理員產生的下列設定值：

* **[!UICONTROL 畫素代碼]**
* **[!UICONTROL 存取Token]**

完成後，選取&#x200B;**[!UICONTROL 儲存]**。

[!DNL TikTok] Web事件API擴充功能的![[!DNL TikTok]設定畫面。](../../../images/extensions/server/tiktok/configure.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，以判斷將事件傳送至[!DNL TikTok]的時間和方式。

在您的事件轉送屬性中建立新的[規則](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL 動作]**&#x200B;底下，新增動作並將擴充功能設為&#x200B;**[!UICONTROL TikTok Web Events API擴充功能]**。 若要將Edge Network事件傳送至[!DNL TikTok]，請將&#x200B;**[!UICONTROL 動作型別]**&#x200B;設定為&#x200B;**[!UICONTROL 傳送TikTok Web事件API事件]。**

![正在為資料收集UI中的[!DNL TikTok]規則選取[!UICONTROL 傳送TikTok Web事件API事件]動作型別。](../../../images/extensions/server/tiktok/select-action.png)

選取後，會顯示其他控制項以進一步設定事件，如下所述。 完成後，選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以儲存規則。

**[!UICONTROL 網頁事件和引數]**

Web事件和引數包含有關事件的一般資訊。 [!DNL TikTok]整合工具支援標準事件，且可用於報表、轉換最佳化及建立對象。

| 輸入 | 說明 |
| --- | --- |
| 活動名稱 | 事件的名稱。 這些動作具有預先定義的名稱，由[!DNL TikTok]建立，是必要欄位。 請參閱[[!DNL TikTok] 行銷API](https://business-api.tiktok.com/portal/docs?id=1741601162187777)檔案，以取得支援事件的詳細資訊。 |
| 事件時間 | 以ISO 8601或`yyyy-MM-dd'T'HH:mm:ss:SSSZ`格式作為字串的日期時間。 這是必填欄位。 |
| 事件ID | 廣告商產生的唯一ID可指出每個事件。 這是選用欄位，用於重複資料刪除。 |

{style="table-layout:auto"}

![顯示輸入欄位之範例資料的[!DNL Web Events and Parameters]區段。](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL 使用者內容引數]**

使用者內容引數包含用來比對Web訪客事件與[!DNL TikTok]位使用者的客戶資訊。 包含多種型別的相符資料，可讓您提高目標定位和最佳化模型的準確性。

| 輸入 | 說明 |
| --- | --- |
| IP位址 | 瀏覽器的非雜湊公用IP位址。 支援IPv4和IPv6位址。 可辨識IPv6位址的完整和壓縮形式。 |
| 使用者代理 | 來自使用者裝置的非雜湊使用者代理。 |
| 電子郵件 | 與轉換事件相關之連絡人的電子郵件地址。 |
| 電話 | 在雜湊之前，電話號碼必須是E164格式[+][國家代碼][區號][local phone number]。 |
| Cookie ID | 如果您使用Pixel SDK，將會在`_ttp` Cookie中自動儲存唯一識別碼（如果已啟用Cookie）。 `_ttp`值可以擷取並用於此欄位。 |
| 外部 ID | 任何唯一識別碼，例如使用者ID、外部Cookie ID等，都必須使用SHA256進行雜湊處理。 |
| TikTok點按ID | 每次在[!DNL TikTok]上選取廣告時，都會新增至登陸頁面URL的`ttclid`。 |
| 頁面 URL | 事件時的頁面URL。 |
| 頁面反向連結URL | 頁面反向連結的URL。 |

{style="table-layout:auto"}

![顯示輸入欄位之範例資料的[!DNL User Context Parameters]區段。](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL 屬性引數]**

使用屬性引數來設定其他支援的屬性。

| 輸入 | 說明 |
| --- | --- |
| 價格 | 單一料號的成本。 |
| 數量 | 在事件中購買的專案數。 這必須是大於0的正數。 |
| 內容類型 | 必須將`product`或`product_group`的值指派給content_type物件屬性，這取決於當您設定產品目錄時如何設定資料摘要。 |
| 內容ID | 產品專案的唯一識別碼。 |
| 內容類別 | 頁面/產品的類別。 |
| 內容名稱 | 頁面/產品的名稱。 |
| 貨幣 | 事件中購買專案的貨幣。 這以ISO-4217表示。 |
| 值 | 訂單的總價。 此值將等於價格*數量。 |
| 說明 | 專案或頁面的說明。 |
| 查詢 | 用來查詢產品的文字字串。 |
| 狀態 | 訂單、料號或服務的狀態。 例如，「submitted」。 |

{style="table-layout:auto"}

![顯示輸入欄位之範例資料的[!DNL Properties Parameters]區段。](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## 事件重複資料刪除 {#deduplication}

如果您同時使用[!DNL TikTok] pixel SDK和[!DNL TikTok] Web事件API擴充功能，將相同的事件傳送至[!DNL TikTok]，則需要設定[!DNL TikTok]畫素以進行重複資料刪除。

如果從使用者端和伺服器傳送的相異事件型別沒有任何重疊，則不需要重複資料刪除。 若要確保您的報表不會受到負面影響，您必須確定已針對[!DNL TikTok]畫素SDK與[!DNL TikTok]網頁事件API擴充功能共用的任何單一事件，進行重複資料刪除。

傳送共用事件時，請確定每個事件都包含畫素ID、事件ID和名稱。 相隔五分鐘內送達的重複事件將會合併。 如果第一個事件中沒有資料欄位，則會與後續事件結合。 我們將移除48小時內收到的所有重複事件。

如需此程式的詳細資訊，請參閱有關[事件重複資料刪除](https://ads.tiktok.com/help/article/event-deduplication)的[!DNL TikTok]檔案。

## 後續步驟

本指南說明如何使用[!DNL TikTok]網頁事件API擴充功能，將伺服器端事件資料傳送至[!DNL TikTok]。 如需[!DNL Adobe Experience Platform]中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。
