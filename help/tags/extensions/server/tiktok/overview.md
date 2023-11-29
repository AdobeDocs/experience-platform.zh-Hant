---
title: AdobeTikTok網站事件API擴充功能整合
description: 此Adobe Experience Platform網頁事件API可讓您直接與TikTok共用網站互動。
last-substantial-update: 2023-09-26T00:00:00Z
source-git-commit: d8b7006ade1dc82fdd79b7ed744c021bc304bca7
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 3%

---

# [!DNL TikTok] 網站事件API擴充功能概觀

此 [!DNL TikTok] events API是安全的 [Edge Network伺服器API](/help/server-api/overview.md) 可讓您共用資訊的介面 [!DNL TikTok] 直接說明使用者在您網站上的動作。 您可以善用事件轉送規則，從傳送資料 [!DNL Adobe Experience Platform Edge Network] 至 [!DNL TikTok] 藉由使用 [!DNL TikTok] 網頁事件API擴充功能。

## [!DNL TikTok] 必備條件 {#prerequisites}

若要設定 [!DNL TikTok] 用於的網站事件API [!DNL TikTok] events API，您必須產生 [!DNL TikTok] 畫素程式碼和存取Token。

您必須具備有效的 [!DNL TikTok] 商業帳戶，以建立 [!DNL TikTok] 使用合作夥伴設定的畫素。 前往 [[!DNL TikTok] 企業註冊頁面](https://www.tiktok.com/business/en-US/solutions/business-account) 註冊並建立帳戶。

您必須登入您的企業帳戶才能進行設定 [!DNL TikTok] 使用合作夥伴設定的畫素。 請依照下列步驟執行此操作：

1. 導覽至 **[!UICONTROL 資產]** 標籤並選取 **[!UICONTROL 事件]**.
2. 在「Web事件」底下，選取 **[!UICONTROL 管理]**.
3. 選取 **[!UICONTROL 設定網頁事件]**.
4. 選取 **[!UICONTROL 合作夥伴設定]** 作為您的連線方法。

請參閱 [開始使用畫素](https://ads.tiktok.com/help/article/get-started-pixel) 指南，以瞭解如何設定 [!DNL TikTok] 畫素。

成功建立畫素後，您就可以產生存取權杖。 若要這麼做，請導覽至「畫素」，然後選取 **[!UICONTROL 設定]** 標籤。 在Events API底下，選取 **[!UICONTROL 產生存取權杖]**.

請參閱 [[!DNL TikTok] 快速入門手冊](https://business-api.tiktok.com/portal/docs?id=1739584855420929) 如需如何設定畫素程式碼和存取Token的詳細資訊。

## 安裝並設定 [!DNL TikTok] 網站事件API擴充功能 {#install}

若要安裝擴充功能，請選取 **[!UICONTROL 擴充功能]** ，位於左側導覽器中。 在 **[!UICONTROL 目錄]** 索引標籤中，選取 **[!UICONTROL TikTok網站事件API擴充功能]** 然後選取 **[!UICONTROL 安裝]**.

![擴充功能目錄顯示 [!DNL TikTok] 擴充卡醒目提示安裝。](../../../images/extensions/server/tiktok/install-extension.png)

在下一個畫面中，輸入下列您先前產生的設定值 [!DNL TikTok] 廣告管理員：

* **[!UICONTROL 畫素代碼]**
* **[!UICONTROL 存取權杖]**

完成後，選取 **[!UICONTROL 儲存]**.

![[!DNL TikTok] 的設定畫面 [!DNL TikTok] 網站事件API擴充功能。](../../../images/extensions/server/tiktok/configure.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，以判斷將事件傳送至的時間和方式 [!DNL TikTok].

建立新的 [規則](../../../ui/managing-resources/rules.md) 在事件轉送屬性中。 在 **[!UICONTROL 動作]**，新增動作並將擴充功能設為 **[!UICONTROL TikTok網站事件API擴充功能]**. 傳送Edge Network事件給 [!DNL TikTok]，設定 **[!UICONTROL 動作型別]** 至 **[!UICONTROL 傳送TikTok網頁事件API事件].**

![此 [!UICONTROL 傳送TikTok網頁事件API事件] 為選取的動作型別 [!DNL TikTok] 資料收集UI中的規則。](../../../images/extensions/server/tiktok/select-action.png)

選取後，會顯示其他控制項以進一步設定事件，如下所述。 完成後，選取 **[!UICONTROL 保留變更]** 以儲存規則。

**[!UICONTROL Web事件和引數]**

Web事件和引數包含有關事件的一般資訊。 支援的標準事件包括 [!DNL TikTok] 整合工具和可用於報表、轉換最佳化及建立對象。

| 輸入 | 說明 |
| --- | --- |
| 活動名稱 | 事件的名稱。 這些是預先定義名稱的動作，建立者為 [!DNL TikTok] 和為必填欄位。 請參閱 [[!DNL TikTok] 行銷API](https://business-api.tiktok.com/portal/docs?id=1741601162187777) 檔案以取得支援事件的詳細資訊。 |
| 事件時間 | ISO 8601或yyyy-MM-dd&#39;T&#39;HH中的字串形式的日期 — 時間:mm:SSSZ格式。 這是必填欄位。 |
| 事件ID | 廣告商產生的唯一ID可指出每個事件。 這是選用欄位，用於重複資料刪除。 |

{style="table-layout:auto"}

![此 [!DNL Web Events and Parameters] 區段顯示輸入欄位的範例資料。](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL 使用者內容引數]**

使用者內容引數包含用來比對Web訪客事件的客戶資訊 [!DNL TikTok] 使用者。 包含多種型別的相符資料，可讓您提高目標定位和最佳化模型的準確性。

| 輸入 | 說明 |
| --- | --- |
| IP位址 | 瀏覽器的非雜湊公用IP位址。 支援IPv4和IPv6位址。 可辨識IPv6位址的完整和壓縮形式。 |
| 使用者代理 | 來自使用者裝置的非雜湊使用者代理。 |
| 電子郵件 | 與轉換事件相關之連絡人的電子郵件地址。 |
| 電話 | 電話號碼必須是E164格式[+][國家/地區代碼][區碼][local phone number] 雜湊處理前。 |
| Cookie ID | 如果您使用Pixel SDK，系統會自動將唯一識別碼儲存在 `_ttp` Cookie （如果已啟用Cookie）。 此 `_ttp` 值可以擷取並用於此欄位。 |
| 外部ID | 任何唯一識別碼，例如使用者ID、外部Cookie ID等，都必須使用SHA256進行雜湊處理。 |
| TikTok點按ID | 此 `ttclid` 會在每次選取廣告時新增至登入頁面的URL [!DNL TikTok]. |
| 頁面 URL | 事件時的頁面URL。 |
| 頁面反向連結URL | 頁面反向連結的URL。 |

{style="table-layout:auto"}

![此 [!DNL User Context Parameters] 區段顯示輸入欄位的範例資料。](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL 屬性引數]**

使用屬性引數來設定其他支援的屬性。

| 輸入 | 說明 |
| --- | --- |
| 價格 | 單一料號的成本。 |
| 數量 | 在事件中購買的專案數。 這必須是大於0的正數。 |
| 內容類型 | 任一的值 `product` 或 `product_group` 必須指派給content_type物件屬性，實際指派取決於您在設定產品目錄時設定資料摘要的方式。 |
| 內容 ID | 產品專案的唯一識別碼。 |
| 內容類別 | 頁面/產品的類別。 |
| 內容名稱 | 頁面/產品的名稱。 |
| 貨幣 | 事件中購買專案的貨幣。 這以ISO-4217表示。 |
| 值 | 訂單的總價。 此值將等於價格*數量。 |
| 說明 | 專案或頁面的說明。 |
| 查詢 | 用來查詢產品的文字字串。 |
| 狀態 | 訂單、料號或服務的狀態。 例如，「submitted」。 |

{style="table-layout:auto"}

![此 [!DNL Properties Parameters] 區段顯示輸入欄位的範例資料。](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## 事件重複資料刪除 {#deduplication}

[!DNL TikTok] 如果您同時使用 [!DNL TikTok] 畫素SDK和 [!DNL TikTok] 傳送相同事件至的網站事件API擴充功能 [!DNL TikTok].

如果從使用者端和伺服器傳送的相異事件型別沒有任何重疊，則不需要重複資料刪除。 若要確保您的報告不會受到負面影響，您必須確定已共用任何單一事件， [!DNL TikTok] 畫素SDK和 [!DNL TikTok] 網站事件API擴充功能會進行重複資料刪除。

傳送共用事件時，請確定每個事件都包含畫素ID、事件ID和名稱。 相隔五分鐘內送達的重複事件將會合併。 如果第一個事件中沒有資料欄位，則會與後續事件結合。 我們將移除48小時內收到的所有重複事件。

請參閱 [!DNL TikTok] 檔案： [事件重複資料刪除](https://ads.tiktok.com/help/article/event-deduplication) 以取得此程式的詳細資訊。

## 後續步驟

本指南說明如何將伺服器端事件資料傳送至 [!DNL TikTok] 使用 [!DNL TikTok] 網站事件API擴充功能。 如需事件轉送功能的詳細資訊，請參閱 [!DNL Adobe Experience Platform]，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
