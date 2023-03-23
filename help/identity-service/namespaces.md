---
keywords: Experience Platform；首頁；熱門主題；命名空間；命名空間；命名空間；命名空間；身分命名空間；身分命名空間；身分識別；身分識別；身分識別；身分識別；身分識別服務；身分識別服務
solution: Experience Platform
title: 身分命名空間概述
description: 身分識別命名空間是 Identity Service 的元件，用途是作為身分識別相關內容的指標。 例如，他們會將「name@email.com」值區分為電子郵件地址，或將「443522」區分為數值CRM ID。
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 482de6a50d14b9de095014b070ce400a2fd273cc
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 7%

---

# 身分命名空間概觀

身分識別命名空間是 [[!DNL Identity Service]](./home.md) 作為身份相關背景的指標。 例如，它們會區分「name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數值CRM ID。

## 快速入門

使用身分識別命名空間需要先了解所涉及的各種Adobe Experience Platform服務。 開始使用命名空間之前，請先檢閱以下服務的檔案：

- [[!DNL Real-Time Customer Profile]](../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。
- [[!DNL Identity Service]](./home.md):跨裝置和系統橋接身分，以更全面了解個別客戶及其行為。
- [[!DNL Privacy Service]](../privacy-service/home.md):身分命名空間用於法律隱私權法規(例如一般資料保護規範(GDPR))的法規遵循要求中。 每個隱私權要求都會相對於命名空間提出，以識別應該影響哪些消費者的資料。

## 了解身分識別命名空間

完全限定的身分包括ID值和命名空間。 在設定檔片段間比對記錄資料時，如 [!DNL Real-Time Customer Profile] 合併設定檔資料，身分值和命名空間必須相符。

例如，兩個設定檔片段可能包含不同的主要ID，但它們對「電子郵件」命名空間共用相同的值，因此 [!DNL Platform] 可以看到這些片段實際上是相同的個人，並將資料匯整在個人的身分圖表中。

![](images/identity-service-stitching.png)

### 身分類型 {#identity-types}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="指定身分識別類型"
>abstract="身分識別類型控制資料是否儲存到身分識別圖中。非人識別碼不會儲存，所有其他身分識別類型都會儲存。"
>text="Learn more in documentation"

資料可由數種不同的身分類型識別。 身分類型是在建立身分命名空間時指定，並控制資料是否會保存至身分圖表，以及如何處理該資料的任何特殊指示。 除外的所有身分類型 **非人員識別碼** 請遵循將命名空間及其對應ID值拼接至身分圖叢集的相同行為。 使用 **非人員識別碼**.

下列身分類型可在 [!DNL Platform]:

| 身分類型 | 說明 |
| --- | --- |
| Cookie ID | Cookie ID可識別網頁瀏覽器。 這些身分對於擴充至關重要，且構成身分圖的大部分。 然而，從本質上講，它們會迅速衰減，並隨著時間而失去價值。 |
| 跨裝置ID | 跨裝置ID可識別個人，且通常會將其他ID系結在一起。 例如登入ID、CRM ID和忠誠度ID。 這是 [!DNL Identity Service] 以靈敏地處理值。 |
| 裝置ID | 裝置ID可識別硬體裝置，例如IDFA(iPhone和iPad)、GAID(Android)和RIDA(Roku)，並可由家庭中的多人共用。 |
| 電子郵件地址 | 電子郵件地址通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 此類型的身分包括個人識別資訊(PII)。 這是 [!DNL Identity Service] 以靈敏地處理值。 |
| 非人員識別碼 | 非人員ID用於儲存需要命名空間但未連線至人員叢集的識別碼。 例如產品SKU、與產品、組織或商店相關的資料。 |
| 電話號碼 | 電話號碼通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 此類型的身分包含PII。 這表示 [!DNL Identity Service] 以靈敏地處理值。 |

### 標準命名空間 {#standard}

Experience Platform提供數個可供所有組織使用的身分識別命名空間。 這些稱為標準命名空間，可使用 [!DNL Identity Service] API或透過Platform UI。

提供下列標準命名空間，供Platform內的所有組織使用：

| 顯示名稱 | 說明 |
| ------------ | ----------- |
| AdCloud | 代表AdobeAdCloud的命名空間。 |
| Adobe Analytics（舊版ID） | 代表Adobe Analytics的命名空間。 請參閱下列檔案，內容如下 [Adobe Analytics命名空間](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) 以取得更多資訊。 |
| Apple IDFA（廣告商的ID） | 代表廣告商Apple ID的命名空間。 請參閱下列檔案，內容如下 [興趣型廣告](https://support.apple.com/en-us/HT202074) 以取得更多資訊。 |
| Apple推播通知服務 | 代表使用Apple推播通知服務所收集身分的命名空間。 請參閱下列檔案，內容如下 [Apple推播通知服務](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) 以取得更多資訊。 |
| 核心 | 代表Adobe Audience Manager的命名空間。 此命名空間也可以以其舊有名稱參照：「Adobe AudienceManager」。 請參閱下列檔案，內容如下 [Audience ManagerID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) 以取得更多資訊。 |
| ECID | 代表ECID的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 請參閱下列檔案，內容如下 [ECID](./ecid.md) 以取得更多資訊。 |
| 電子郵件 | 代表電子郵件地址的命名空間。 此類型的命名空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |
| 電子郵件（SHA256，小寫） | 預先雜湊電子郵件地址的命名空間。 此命名空間中提供的值在以SHA256進行雜湊處理前會轉換為小寫。 在標準化電子郵件地址之前，需要先裁剪開頭和結尾空格。 無法回溯變更此設定。 請參閱下列檔案，內容如下 [SHA256雜湊支援](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 以取得更多資訊。 |
| Firebase雲端訊息 | 代表使用Google Firebase雲端訊息傳送推播通知所收集身分的命名空間。 請參閱下列檔案，內容如下 [Google Firebase雲端訊息](https://firebase.google.com/docs/cloud-messaging) 以取得更多資訊。 |
| Google廣告ID(GAID) | 代表Google Advertising ID的命名空間。 請參閱下列檔案，內容如下 [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 以取得更多資訊。 |
| Google點按ID | 代表Google點按ID的命名空間。 請參閱下列檔案，內容如下 [Google Ads中的點擊追蹤](https://developers.google.com/adwords/api/docs/guides/click-tracking) 以取得更多資訊。 |
| 電話 | 代表電話號碼的命名空間。 此類型的命名空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |
| 電話(E.164) | 代表需要以E.164格式雜湊的原始電話號碼的命名空間。 E.164格式包含加號(`+`)、國際國家/地區呼叫代碼、區域代碼和電話號碼。 例如: `(+)(country code)(area code)(phone number)`. |
| 電話(SHA256) | 代表需使用SHA256雜湊的電話號碼的命名空間。 您必須移除符號、字母和任何前導零。 您也必須將國家/地區呼叫代碼新增為首碼。 |
| 電話(SHA256_E.164) | 表示需要同時使用SHA256和E.164格式雜湊的原始電話號碼的命名空間。 |
| TNTID | 代表Adobe Target的命名空間。 請參閱下列檔案，內容如下 [目標](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) 以取得詳細資訊。 |
| Windows AID | 代表Windows廣告ID的命名空間。 請參閱下列檔案，內容如下 [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) 以取得更多資訊。 |

### 檢視身分識別命名空間 {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="檢視整合身分"
>abstract="整合身分識別是用於連接其他系統的命名空間，不用於身分識別解析或拼接身分識別。<br>這些身分依預設是隱藏的。使用切換來檢視整合命名空間。"

若要在UI中檢視身分識別命名空間，請選取 **[!UICONTROL 身分]** 在左側導覽器中，然後選取 **[!UICONTROL 瀏覽]**.

![瀏覽](./images/browse.png)

頁面的主介面中會顯示身份命名空間清單，顯示其名稱、身份符號、上次更新日期的相關資訊，以及這些命名空間是標準命名空間還是自定義命名空間。 右側邊欄包含 [!UICONTROL 身分圖強度].

![身分](./images/identities.png)

Platform也提供命名空間以供整合之用。 這些命名空間預設會隱藏，因為它們用於連線其他系統，而非用於連結身分識別。 若要檢視整合的命名空間，請選取 **[!UICONTROL 檢視整合身分]**.

![view-integration-identities](./images/view-integration-identities.png)

從清單中選取身分命名空間，以檢視特定命名空間的資訊。 選取身分命名空間會更新右側邊欄的顯示，以顯示與您選取的身分命名空間相關的中繼資料，包括擷取的身分數量以及失敗和略過的記錄數量。

![select-namespace](./images/select-namespace.png)

## 管理自訂命名空間 {#manage-namespaces}

視您的組織資料和使用案例而定，您可能需要自訂命名空間。 可使用 [[!DNL Identity Service]](./api/create-custom-namespace.md) API或透過UI。

若要使用UI建立自訂命名空間，請導覽至 **[!UICONTROL 身分]** 工作區，選取 **[!UICONTROL 瀏覽]**，然後選取 **[!UICONTROL 建立身分命名空間]**.

![select-create](./images/select-create.png)

此 **[!UICONTROL 建立身分命名空間]** 對話框。 提供唯一 **[!UICONTROL 顯示名稱]** 和 **[!UICONTROL 標識符]** 然後選取您要建立的身分類型。 您也可以新增選用說明，以新增命名空間的詳細資訊。 除了 **非人員識別碼** 會遵循相同的匯整行為。 如果您選取 **非人員識別碼** 由於是建立命名空間時的身分類型，因此不會進行連結。 有關每種身份類型的特定資訊，請參閱 [身分類型](#identity-types).

完成後，請選取 **[!UICONTROL 建立]**.

>[!IMPORTANT]
>
>您定義的命名空間為組織專用，且必須有唯一身分符號，才能成功建立。

![create-identity-namespace](./images/create-identity-namespace.png)

與標準命名空間類似，您可以從 **[!UICONTROL 瀏覽]** 標籤來檢視其詳細資訊。 不過，使用自訂命名空間，您也可以從詳細資訊區域編輯其顯示名稱和說明。

>[!NOTE]
>
>建立命名空間後，將無法刪除該命名空間，其標識符號和類型將無法更改。

## 身分資料中的命名空間

提供身分識別的命名空間取決於您用來提供身分資料的方法。 如需提供資料身分資料的詳細資訊，請參閱 [提供身分資料](./home.md#supplying-identity-data-to-identity-service) 在 [!DNL Identity Service] 概述。

## 後續步驟

現在您已了解身分識別命名空間的重要概念，開始了解如何使用 [身分圖表檢視器](./ui/identity-graph-viewer.md).
