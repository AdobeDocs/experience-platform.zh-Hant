---
title: 身分名稱空間總覽
description: 瞭解Identity Service中的身分識別名稱空間。
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 6ae3626c2e0f7e58968b5582ca1895bd03ab1c32
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 12%

---

# 身分名稱空間總覽

請閱讀以下檔案，深入瞭解您可以在Adobe Experience Platform Identity Service中處理身分識別名稱空間的動作。

## 快速入門

身分名稱空間需要瞭解各種Adobe Experience Platform服務。 開始使用命名空間之前，請先檢閱下列服務文件：

* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [[!DNL Identity Service]](../home.md)：透過跨裝置和系統橋接身分，更能瞭解個別客戶及其行為。
* [[!DNL Privacy Service]](../../privacy-service/home.md)：身分名稱空間用於一般資料保護規範(GDPR)等法律隱私權法規的合規性請求中。 每個隱私權請求都是相對於名稱空間提出，以識別哪些消費者的資料應該受到影響。

## 了解身分命名空間 {#understanding-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="身分識別命名空間"
>abstract="身分命名空間是特定身分的背景。例如，`Email`的命名空間可以對應 **name<span>@acme.com**。同樣地，`Phone` 的命名空間可以對應 `555-555-1234`。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="身分識別值"
>abstract="身分識別值是代表唯一個人、組織或資產的識別碼。該值代表的身分識別的內容或類型由相對應的身分識別命名空間定義。當全部設定檔片段都符合記錄資料時，命名空間和識別值必須相符。當全部設定檔片段都符合記錄資料時，命名空間和識別值必須相符。"
>text="Learn more in documentation"

完整身分包含兩個元件： **身分值** 和 **身分名稱空間**. 例如，如果身分的值是 `scott@acme.com`，則名稱空間會將此值識別為電子郵件地址，以提供其內容。 同樣地，名稱空間可以區分 `555-123-456` 作為電話號碼，以及 `3126ABC` 作為CRM ID。 基本上， **名稱空間會提供指定身分的上下文**. 跨設定檔片段比對記錄資料時，例如 [!DNL Real-Time Customer Profile] 會合併設定檔資料，身分值和名稱空間必須相符。

例如，兩個設定檔片段可能包含不同的主要ID，但兩者的「電子郵件」名稱空間值相同，因此Experience Platform能看到這些片段實際上是同一個人，並將個人資料一起匯入身分圖表中。

>[!BEGINSHADEBOX]

**身分名稱空間說明**

要更清楚瞭解名稱空間的另一個方法是考量現實世界的範例，例如城市及其對應的州。 例如，緬因州的波特蘭和奧勒岡州的波特蘭是美國兩個不同的地方。 雖然城市有相同的名稱，但國家是以名稱空間的方式運作，並提供區分這兩個城市的必要內容。

將相同的邏輯套用至Identity Service：

* 身分值總覽： `1-234-567-8900` 看起來可能像電話號碼。 但是，從系統的角度來看，此值可能設定為CRM ID。 如果沒有對應的名稱空間，Identity Service無法將必要的內容套用至此身分值。
* 另一個範例是身分值： `john@gmail.com`. 雖然您可輕鬆將此身分值假設為電子郵件，但完全有可能將其設定為自訂名稱空間CRM ID。 使用名稱空間，您可以區分 `Email:john@gmail.com` 從 `CRM ID:john@gmail.com`.

>[!ENDSHADEBOX]

### 名稱空間的元件

名稱空間包含下列元件：

* **顯示名稱**：指定名稱空間的好記名稱。
* **身分符號**：身分服務內部用來代表名稱空間的程式碼。
* **身分型別**：指定名稱空間的分類。
* **說明**：（選用）您可以提供的有關指定名稱空間的任何補充資訊。

### 身分類型 {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="指定身分類型"
>abstract="身分類型控制資料是否儲存到身分識別圖中。不會為下列身分類型產生身分識別圖：非個人識別碼和合作夥伴 ID。"
>text="Learn more in documentation"

身分名稱空間的一個元素是 **身分型別**. 身分型別會判斷：

* 是否要產生身分圖表：
   * 不會為下列身分類型產生身分識別圖：非個人識別碼和合作夥伴 ID。
   * 會針對所有其他身分型別產生身分圖表。
* 達到系統限制時，會從身分圖表移除哪些身分。 如需詳細資訊，請閱讀 [身分資料的護欄](../guardrails.md).

Experience Platform中有以下身分型別：

| 身分類型 | 說明 |
| --- | --- |
| Cookie ID | Cookie ID可識別網頁瀏覽器。 這些身分對於擴充至關重要，並構成身分圖表的大多數。 然而，自然而然地，它們會迅速衰落，並隨著時間而失去價值。 |
| 跨裝置ID | 跨裝置ID會識別個人，通常會將其他ID連結在一起。 範例包括登入ID、CRM ID和熟客ID。 此表示會 [!DNL Identity Service] 以敏感地處理值。 |
| 裝置ID | 裝置ID會識別硬體裝置，例如IDFA (iPhone和iPad)、GAID (Android)和RIDA (Roku)，而且可由家中的多個人共用。 |
| 電子郵件地址 | 電子郵件地址通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 此型別的身分包含個人識別資訊(PII)。 此表示會 [!DNL Identity Service] 以敏感地處理值。 |
| 非人員識別碼 | 非人員ID是用來儲存需要名稱空間但未連線至人員叢集的識別碼。 例如，產品SKU、與產品、組織或商店相關的資料。 |
| 合作夥伴 ID | <ul><li>合作夥伴 ID 指資料合作夥伴用於代表人員的識別碼。合作夥伴ID通常使用假名，以免揭露個人的真實身分，而且可能是機率。 在Real-time Customer Data Platform中，合作夥伴ID主要用於擴充受眾啟用和資料擴充，而非用於建立身分圖表連結。</li><li>擷取包含指定為合作夥伴ID型別的身分名稱空間的身分時，不會產生身分圖表。</li><li>若無法使用合作夥伴ID的身分型別來內嵌合作夥伴資料，可能會導致身分服務受到系統圖表限制，且個人資料可能會不必要地合併。</li><ul> |
| 電話號碼 | 電話號碼通常與單一人員相關聯，因此可用於跨不同頻道識別該人員。 此型別的身分識別包括PII。 此表示會 [!DNL Identity Service] 以敏感地處理值。 |

{style="table-layout:auto"}

### 標準名稱空間 {#standard}

Experience Platform提供數個適用於所有組織的身分識別名稱空間。 這些稱為標準名稱空間，並可使用檢視 [!DNL Identity Service] API或透過Platform UI。

提供下列標準名稱空間，供Platform內的所有組織使用：

| 顯示名稱 | 說明 |
| ------------ | ----------- |
| AdCloud | 代表AdobeAdCloud的名稱空間。 |
| Adobe Analytics （舊版ID） | 代表Adobe Analytics的名稱空間。 請參閱以下檔案： [Adobe Analytics名稱空間](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html#namespaces) 以取得詳細資訊。 |
| Apple IDFA （廣告商的ID） | 代表廣告商Apple ID的名稱空間。 請參閱以下檔案： [興趣型廣告](https://support.apple.com/en-us/HT202074) 以取得詳細資訊。 |
| Apple推播通知服務 | 代表使用Apple推播通知服務所收集之身分的名稱空間。 請參閱以下檔案： [Apple推播通知服務](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) 以取得詳細資訊。 |
| 核心 | 代表Adobe Audience Manager的名稱空間。 此名稱空間也可以透過其舊版名稱「Adobe AudienceManager」來參照。 請參閱以下檔案： [AUDIENCE MANAGERID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html#aam-ids) 以取得詳細資訊。 |
| ECID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱以下檔案： [ECID](./ecid.md) 以取得詳細資訊。 |
| 電子郵件 | 代表電子郵件地址的名稱空間。 這種型別的名稱空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |
| 電子郵件（SHA256，小寫） | 預先雜湊電子郵件地址的名稱空間。 使用SHA256雜湊之前，此名稱空間中提供的值會轉換為小寫。 在電子郵件地址標準化之前，需要修剪前置和結尾空格。 無法回溯變更此設定。 請參閱以下檔案： [SHA256雜湊支援](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support) 以取得詳細資訊。 |
| Firebase雲端通訊 | 一個名稱空間，代表使用Google Firebase Cloud Messaging為推播通知所收集的身分。 請參閱以下檔案： [Google Firebase雲端通訊](https://firebase.google.com/docs/cloud-messaging) 以取得詳細資訊。 |
| Google廣告ID (GAID) | 代表Google Advertising ID的名稱空間。 請參閱以下檔案： [Google廣告ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 以取得詳細資訊。 |
| Google點按ID | 代表Google點選ID的名稱空間。 請參閱以下檔案： [Google Ads中的點選追蹤](https://developers.google.com/adwords/api/docs/guides/click-tracking) 以取得詳細資訊。 |
| 電話 | 代表電話號碼的名稱空間。 這種型別的名稱空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |
| 電話(E.164) | 代表需要以E.164格式雜湊的原始電話號碼的名稱空間。 E.164格式包含加號(`+`)、國際國家/地區撥號代碼、當地區號和電話號碼。 例如: `(+)(country code)(area code)(phone number)`。 |
| 電話(SHA256) | 代表需使用SHA256雜湊處理之電話號碼的名稱空間。 您必須移除符號、字母及任何前導零。 您也必須新增國家/地區呼叫代碼作為前置詞。 |
| 電話(SHA256_E.164) | 代表需要使用SHA256和E.164格式雜湊的原始電話號碼的名稱空間。 |
| TNTID | 代表Adobe Target的名稱空間。 請參閱以下檔案： [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html) 以取得詳細資訊。 |
| Windows AID | 代表Windows Advertising ID的名稱空間。 請參閱以下檔案： [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) 以取得詳細資訊。 |

### 檢視身分命名空間 {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="檢視整合身分"
>abstract="整合身分識別是用於連接其他系統的命名空間，不用於身分識別解析或拼接身分識別。<br>這些身分依預設是隱藏的。使用切換來檢視整合命名空間。"

若要在UI中檢視身分識別名稱空間，請選取 **[!UICONTROL 身分]** 在左側導覽中，然後選取 **[!UICONTROL 瀏覽]**.

您組織中的名稱空間目錄隨即出現，顯示其名稱、身分符號、上次更新日期、對應身分型別和說明的相關資訊。

![貴組織中的自訂身分名稱空間目錄。](../images/namespace/browse.png)

## 建立自訂名稱空間 {#create-namespaces}

根據您的組織資料和使用案例，您可能需要自訂名稱空間。 自訂名稱空間可透過以下方式建立： [[!DNL Identity Service]](../api/create-custom-namespace.md) API或透過UI。

若要建立自訂名稱空間，請選取 **[!UICONTROL 建立身分名稱空間]**.

>[!TIP]
>
>整合身分是用來連線其他系統的名稱空間。 它們不會用於身分解析，也不會用於拼接身分。 選取 **[!UICONTROL 檢視整合身分]** 以更新清單並包含整合身分。 不過，整合身分預設為隱藏，因為這些身分是僅限檢視的，您不需要加以設定。

![在身分工作區中建立身分名稱空間按鈕。](../images/namespace/create-identity-namespace.png)

此 [!UICONTROL 建立身分名稱空間] 視窗會出現。 首先，您必須為要建立的自訂名稱空間提供顯示名稱和身分符號。 您也可以選擇提供說明，在您正在建立的自訂名稱空間上新增更多內容。

![一個快顯視窗，您可以在其中輸入有關自訂身分名稱空間的資訊。](../images/namespace/name-and-symbol.png)

接著，選取您要指派給自訂名稱空間的身分型別。 完成後，選取 **[!UICONTROL 建立]**.

![身份型別選擇，您可以選擇並指派給自訂身份名稱空間。](../images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* 您定義的名稱空間是組織所私有，而且需要唯一的身分符號才能成功建立。
>
>* 建立名稱空間後，便無法刪除該名稱空間，也無法變更其身分符號和型別。
>
>* 不支援重複的名稱空間。 建立新名稱空間時，不能使用現有的顯示名稱和身分符號。

## 身分資料中的名稱空間

提供身分的名稱空間取決於您提供身分資料的方法。 如需有關提供資料身分資料的詳細資訊，請參閱 [[!DNL Identity Service] 實作指南](../implementation.md).

## 後續步驟

現在您已瞭解身分識別名稱空間的主要概念，可以開始瞭解如何使用身分識別圖表 [身分圖表檢視器](../features/identity-graph-viewer.md).
