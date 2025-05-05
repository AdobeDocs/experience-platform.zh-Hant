---
title: Bombora Intent
description: 瞭解Experience Platform上的Bombora Intent來源。
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hant#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hant#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 9ab2c4725d2188f772bde1f7a89db2bb47c7a46b
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 1%

---

# [!DNL Bombora Intent]

[!DNL Bombora]是全方位的受眾解決方案，專門處理B2B意圖資料。 [!DNL Bombora Intent]是Adobe Experience Platform來源，可用來將您的[!DNL Bombora]帳戶連線至Experience Platform並整合您的帳戶意圖資料。

透過[!DNL Bombora Intent]來源，您可以整合[!DNL Bombora's]公司突增意圖資料，以識別積極研究您產品或服務的帳戶。 使用[!DNL Bombora]優先處理市場內帳戶，以建立精確區段並執行超目標的ABM行銷活動，確保您的行銷工作聚焦於最有可能轉換的帳戶。 此外，您也可以運用意圖導向的策略，將廣告支出最佳化、提高參與度，並大幅提高ROI。

閱讀本檔案以瞭解[!DNL Bombora]來源的先決條件資訊。

## 使用案例 {#use-cases}

請閱讀下列可套用至[!DNL Bombora]來源的使用案例範例。

### Demand-Side Platform (DSP)整合

身為B2B行銷人員，您可以在Real-Time CDP中建立帳戶清單，識別對您的產品有較高意圖的公司，然後在[!DNL Bombora]中啟用此清單（直接與DSP整合），好讓您使用[!DNL Bombora's]資料執行目標性的程式化廣告行銷活動。 這可確保您的廣告支出聚焦於最有可能轉換的公司。

### Account-Based Marketing (ABM)功能

身為B2B行銷人員，您可以根據第一方和第三方意圖訊號建立帳戶清單。 然後，您可以在[!DNL Bombora]中啟用此清單，其中ABM功能可讓您特別鎖定這些帳戶中的員工，以確保您的廣告觸及決策者而非廣泛的對象。

### 多管道ABM啟用

身為B2B行銷人員，您可以在Real-Time CDP中建立帳戶清單，識別高意圖的公司並在[!DNL Bombora]中將其啟用，以跨多個管道執行目標式行銷活動。 在付費社群媒體上，您可以[!DNL Linkedin]和[!DNL Facebook]等平台上，在目標帳戶向專業人員提供個人化廣告。

使用原生廣告平台，您可以確保內容可到達相關內容中的決策者。 您也可以將行銷活動延伸至進階電視，將廣告遞送至重要帳戶。 這種多管道方法可確保跨平台傳送一致的訊息，最大化參與度和轉換率。

## 先決條件 {#prerequisites}

在連線[!DNL Bombora]至Experience Platform之前，請閱讀下列章節中的先決條件步驟。

### IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

### 在Experience Platform上設定許可權

您必須同時為您的帳戶啟用&#x200B;**[!UICONTROL 檢視來源]**&#x200B;和&#x200B;**[!UICONTROL 管理來源]**&#x200B;許可權，才能將您的[!DNL Bombora]帳戶連線至Experience Platform。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/abac/ui/permissions.md)。

### 檔案和目錄的命名限制

在命名您的雲端儲存空間檔案或目錄時，必須考慮下列限制：

* 目錄和檔案元件名稱不能超過255個字元。
* 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
* 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
* 不允許下列字元： `" \ / : | < > * ?`。
* 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
* 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

### 收集必要的認證

Experience Platform上的[!DNL Bombora]由[!DNL Google Cloud Storage]代管。 為了成功驗證您的[!DNL Bombora]帳戶，您必須為下列認證提供適當的值：

| 認證 | 說明 |
| --- | --- |
| 存取金鑰 ID | [!DNL Bombora]存取金鑰識別碼。 這是61個字元的英數字串，需要它才能向Experience Platform驗證您的帳戶。 |
| 祕密存取金鑰 | [!DNL Bombora]秘密存取金鑰。 這是40個字元、以Base64編碼的字串，驗證您的帳戶給Experience Platform是必要的。 |
| 貯體名稱 | 將從其中提取資料的[!DNL Bombora]貯體。 |

如需這些認證的詳細資訊，請閱讀[[!DNL Google Cloud Storage] HMAC金鑰指南](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)。 如需如何產生您自己的存取金鑰的步驟，請參閱 [!DNL Google Cloud Storage] 來源概觀[&#128279;](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account)中的先決條件指南。

## [!DNL Bombora]結構描述 {#schema}

請閱讀本節，以瞭解[!DNL Bombora]結構描述和資料結構的相關資訊。

[!DNL Bombora]結構描述稱為&#x200B;**帳戶意圖每週**。 這是指定帳戶和主題的每週意圖資訊（匿名B2B購買者研究和內容使用）。 資料為parquet格式。

| 欄位名稱 | 資料類型 | 必要 | 商務金鑰 | 附註 |
| --- | --- | --- | --- | --- |
| `Account_Name` | STRING | TRUE | 是 | 公司的正式名稱。 |
| `Domain` | STRING | TRUE | 是 | 顯示意圖的已識別帳戶的網域。 |
| `Topic_Id` | STRING | TRUE | 是 | [!DNL Bombora]主題識別碼。 |
| `Topic_Name` | STRING | TRUE | | [!DNL Bombora]主題名稱。 |
| `Cluster_Name` | STRING | TRUE | | 指定主題[!DNL Bombora]上的叢集名稱。 |
| `Cluster_Id` | STRING | TRUE | | 與指定主題相關聯的叢集ID。 |
| `Composite_Score` | 整數 | TRUE | | 複合分數代表指定主題在指定時段內的消耗模式。 複合分數是介於0到100之間測量，其中100代表最高可能分數，0代表最低可能分數。 超過60的複合分數表示某個網域對特定主題的興趣增加。 這也稱為「突波」。 |
| `Partition_Date` | 日期 | TRUE | | 快照的日曆日期。 這會在每週的週末以`mm/dd/yyyy`格式完成。 |

{style="table-layout:auto"}

>[!TIP]
>
>結構描述的任何變更都會事先通知給Adobe。 若要支援順暢的架構演化，維持回溯相容性至關重要。 Experience Platform會強制實施僅限附加的版本設定方法，確保對結構描述所做的任何更新都是非破壞性的。 這表示嚴禁重大變更，且只允許增強或擴充現有結構的變更。

## 在使用者介面中將您的[!DNL Bombora]帳戶連線至Experience Platform

完成先決條件設定後，請閱讀有關[將您的 [!DNL Bombora] 帳戶連線至Experience Platform](../../tutorials/ui/create/data-partners/bombora.md)的教學課程，以開始整合。

## 常見問題 {#faq}

請閱讀本節，瞭解有關[!DNL Bombora]來源的常見問題解答。

### 我是否需要與[!DNL Bombora]的現有合約，才能在Real-Time CDP B2B edition中使用其帳戶意圖資料？

+++回答

是，您必須與[!DNL Bombora]簽訂有效合約，才能在Experience Platform和Real-Time CDP B2B edition中存取及運用其意圖資料。 此整合可運用您與[!DNL Bombora]的現有協定，在Experience Platform和Real-Time CDP中擷取及啟用帳戶意圖訊號。

+++

### 此整合是否支援[!DNL Bombora]的自訂欄位？

+++回答

目前，您只能使用標準[!DNL Bombora]欄位來擷取和啟用。 若要檢視支援的欄位清單，請閱讀[[!DNL Bombora] 結構描述指南](#schema)以瞭解欄位可用性的詳細資訊。

+++

### 我可以臨機將資料從[!DNL Bombora]擷取到Experience Platform嗎？

+++回答

是，您可以臨機從[!DNL Bombora]擷取資料。 只要有來自[!DNL Bombora]的新資料，您就可以建立新的資料流以擷取最新意圖資料。 不過，您一次只能有一個作用中資料流。 因此，在建立新資料流之前，請務必刪除現有資料流。

+++

### 意圖資料的驗證程式為何？如何檢查哪些意圖資料已連結至特定帳戶？

+++回答

若要驗證意圖資料，並判斷哪些意圖訊號連結至特定帳戶，請使用AccountID的[Adobe Experience Platform查詢服務](../../../query-service/home.md)。

+++

### 如何查詢特定公司的目的？

+++回答

在[查詢服務](../../../query-service/home.md)中執行SQL查詢，以使用公司名稱或AccountID搜尋意圖資料。 若要檢視特定公司的所有意圖資料，您可以使用公司名稱或AccountID在Query Service中執行SQL查詢，以擷取所有關聯的意圖訊號。

+++


### 我在Experience Platform中發現帳戶比對程式的問題，怎麼辦？

+++回答

解決方法取決於特定問題：

* **Experience Platform中的公司網域不正確或遺失**：如果問題是因為帳戶資料中的公司網域值不正確，請更新Experience Platform中的公司網域欄位，以確保正確比對。
* **資料流中的欄位對應不正確**：如果問題是因為資料流中的公司網域欄位路徑不正確，請更新資料流設定以參考正確的欄位路徑。

+++

### 如何刪除Experience Platform中的意圖資料？

+++回答

您必須[刪除資料集](../../../catalog/datasets/user-guide.md#delete-a-dataset)，才能刪除Experience Platform中的意圖資料。

+++

### 哪一個欄位可用來比對[!DNL Bombora]與Experience Platform的帳戶？

+++回答

`accountOrganization.domain`欄位用於比對帳戶。 如果您的組織使用不同的自訂欄位來儲存網站名稱，請確定您提供正確的欄位路徑，以精確對應。

+++

### 在Experience Platform中更新公司網域時會發生什麼事？

+++回答

更新公司網域時，新網域值將會在下次資料流執行中套用。 這可確保：

* 未來意圖資料擷取會使用更新的網域進行帳戶比對。
* 任何先前不符的意圖訊號現在可能會正確與預期帳戶對齊。
* 不會對過去僅擷取的資料進行追溯變更，新傳入的資料將反映更新。

+++

### 什麼是網域比對程式？

+++回答

Experience Platform中的網域比對是根據已清除網域欄位值的精確比對。 Experience Platform會自動移除首碼(例如https:/<span>/www.)，並保留最上層網域(例如adobe.com)。 相符專案需要精確的網域值，不支援模糊相符或子網域。

+++

### 我可以在哪裡使用意圖資料？

+++回答

意圖資料可用於[帳戶對象](../../../segmentation/types/account-audiences.md)，以強化目標定位、細分和個人化。 透過運用意圖訊號，企業可以識別對特定主題表現出高度興趣的客戶，並與他們互動，以最佳化行銷和銷售推廣。

+++
