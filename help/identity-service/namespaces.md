---
keywords: Experience Platform;home；常用主題；namespace；命名空間；命名空間；標識名稱空間；標識名稱空間；標識；標識服務；標識服務
solution: Experience Platform
title: Identity Namespace概觀
topic-legacy: overview
description: 身分識別命名空間是 Identity Service 的元件，用途是作為身分識別相關內容的指標。例如，他們會將"name@email.com"值區分為電子郵件地址或"443522"作為數值CRM ID。
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
translation-type: tm+mt
source-git-commit: ca092af61ac26fcfb6839b7ba0887178c899f89f
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 2%

---

# 身分命名空間概觀

身分名稱空間是[[!DNL Identity Service]](./home.md)的一個元件，用作身份相關上下文的指示器。 例如，他們會將&quot;name<span>@email.com&quot;值區分為電子郵件地址，或將&quot;443522&quot;區分為數值CRM ID。

## 快速入門

使用身分名稱空間需要瞭解所涉及的各種Adobe Experience Platform服務。 開始使用名稱空間之前，請先閱讀下列服務的檔案：

- [[!DNL Real-time Customer Profile]](../profile/home.md):根據來自多個來源的匯總資料即時提供統一的客戶個人檔案。
- [[!DNL Identity Service]](./home.md):跨裝置和系統橋接身分，以更全面地瞭解個別客戶及其行為。
- [[!DNL Privacy Service]](../privacy-service/home.md):身分名稱空間用於遵守通用資料保護規則(GDPR)，在GDPR中，可以相對於名稱空間提出GDPR請求。

## 瞭解身分名稱空間

完全限定身份包括ID值和命名空間。 當在描述檔片段間比對記錄資料時（如[!DNL Real-time Customer Profile]合併描述檔資料時），識別值和命名空間都必須相符。

例如，兩個描述檔片段可能包含不同的主要ID，但是它們對&quot;Email&quot;命名空間有相同的值，因此[!DNL Platform]可以看到這些片段實際上是同一個個體，並將資料匯整在個體的識別圖中。

![](images/identity-service-stitching.png)

### 身分類型

資料可由數種不同的身分類型識別。 在建立身份名稱空間時指定身份類型，並控制資料是否保存到身份圖以及如何處理該資料的任何特殊說明。 除&#x200B;**非人員識別碼**&#x200B;之外的所有身份類型都遵循將命名空間及其對應ID值拼接到身份圖簇的相同行為。 使用&#x200B;**非人員識別碼**&#x200B;時，資料不會銜接在一起。

[!DNL Platform]中提供以下身份類型：

| 身分類型 | 說明 |
| --- | --- |
| Cookie ID | Cookie ID可識別網頁瀏覽器。 這些身份對於擴展至關重要，並且是身份圖的大部分。 然而，從本質上講，它們會迅速衰敗，並隨著時間而失去價值。 |
| 跨裝置ID | 跨裝置ID可識別個別ID，並通常將其他ID系結在一起。 例如登入ID、CRM ID和忠誠度ID。 這表示[!DNL Identity Service]可靈敏地處理該值。 |
| 裝置ID | 裝置ID可識別硬體裝置，例如IDFA（iPhone和iPad）、GAID(Android)和RIDA(Roku)，並可由家庭中的多人共用。 |
| 電子郵件地址 | 電子郵件地址通常與單一人員相關聯，因此可用於識別不同通道的該人員。 此類型的身分識別資訊(PII)。 這表示[!DNL Identity Service]可靈敏地處理該值。 |
| 非人員識別碼 | 非人員ID用於儲存需要名稱空間但未連接到人員群集的標識符。 例如，產品SKU、與產品、組織或商店相關的資料。 |
| 電話號碼 | 電話號碼通常與單一人員相關聯，因此可用於識別不同通道的該人員。 此類型的身份包括PII。 這表示[!DNL Identity Service]可靈敏地處理該值。 |

### 標準名稱空間

Experience Platform提供多個身份名稱空間，可供所有組織使用。 這些名稱空間稱為標準名稱空間，可使用[!DNL Identity Service] API或透過平台UI顯示。

平台內的所有組織都可使用下列標準名稱空間：

| 顯示名稱 | 說明 |
| ------------ | ----------- |
| AdCloud | 代表AdobeAdCloud的命名空間。 |
| Adobe Analytics（舊版ID） | 代表Adobe Analytics的命名空間。 如需詳細資訊，請參閱[Adobe Analytics名稱空間](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces)上的下列檔案。 |
| Apple IDFA（廣告商的ID） | 代表廣告商Apple ID的命名空間。 如需詳細資訊，請參閱[喜好式廣告](https://support.apple.com/en-us/HT202074)上的下列檔案。 |
| Apple推播通知服務 | 代表使用Apple推播通知服務收集之身分的命名空間。 如需詳細資訊，請參閱[Apple推播通知服務](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1)上的下列檔案。 |
| 核心 | 代表Adobe Audience Manager的命名空間。 此命名空間也可以其舊名稱引用：「Adobe AudienceManager」。 如需詳細資訊，請參閱[Audience ManagerID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids)上的下列檔案。 |
| ECID | 代表ECID的命名空間。 此命名空間也可由以下別名引用：&quot;Adobe Marketing CloudID&quot;、&quot;Adobe Experience CloudID&quot;、&quot;Adobe Experience PlatformID&quot;。 如需詳細資訊，請參閱[ECID](./ecid.md)上的下列檔案。 |
| 電子郵件 | 代表電子郵件地址的命名空間。 此類型的命名空間通常與單一人員相關聯，因此可用於識別不同通道的該人員。 |
| 電子郵件（SHA256，小寫） | 預先雜湊電子郵件地址的命名空間。 在使用SHA256進行散列之前，此命名空間中提供的值將轉換為小寫。 前導和尾隨空格必須在電子郵件位址標準化之前加以修剪。 此設定無法追溯變更。 如需詳細資訊，請參閱[SHA256雜湊支援](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support)的下列檔案。 |
| Firebase Cloud訊息 | 代表使用Google Firebase Cloud訊息收集的推播通知身分的命名空間。 如需詳細資訊，請參閱[Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging)上的下列檔案。 |
| Google廣告ID(GAID) | 代表Google廣告ID的命名空間。 如需詳細資訊，請參閱[Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en)上的下列檔案。 |
| Google點按ID | 代表Google點按ID的命名空間。 如需詳細資訊，請參閱[在Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking)中按一下追蹤的下列檔案。 |
| 電話 | 代表電話號碼的命名空間。 此類型的命名空間通常與單一人員相關聯，因此可用於識別不同通道的該人員。 |
| 電話(E.164) | 表示需要以E.164格式雜湊的原始電話號碼的命名空間。 E.164格式包括加號(`+`)、國際國家呼叫代碼、區域代碼和電話號碼。 例如: `(+)(country code)(area code)(phone number)`。 |
| 電話(SHA256) | 表示需要使用SHA256雜湊的電話號碼的命名空間。 您必須移除符號、字母和任何行距零。 您也必須新增國家／地區呼叫代碼作為首碼。 |
| 電話(SHA256_E.164) | 表示需要使用SHA256和E.164格式雜湊的原始電話號碼的命名空間。 |
| TNTID | 代表Adobe Target的命名空間。 如需詳細資訊，請參閱[Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en)上的下列檔案。 |
| Windows AID | 代表Windows廣告ID的命名空間。 如需詳細資訊，請參閱[Windows廣告ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041)上的下列檔案。 |

若要在UI中檢視標準名稱空間，請在左側導覽中選取&#x200B;**[!UICONTROL Identities]**，然後選取&#x200B;**[!UICONTROL Browse]**&#x200B;標籤以顯示組織可存取的標準身分名稱空間清單。 您可以按名稱空間的&#x200B;**[!UICONTROL Display name]**、**[!UICONTROL Identity symbol]**&#x200B;或&#x200B;**[!UICONTROL Owner]**&#x200B;的字母順序對名稱空間進行排序。 或者，您也可以依名稱空間的最近更新日期，按時間順序排序名稱空間。

選取名稱空間，以檢視右側邊欄上的更多特定資訊。

>[!NOTE]
>
>平台也提供名稱空間以進行整合。 這些名稱空間預設為隱藏，因為它們用於連接其他系統，而不是用於縫合標識。 要查看整合命名空間，請選擇&#x200B;**[!UICONTROL View integration identities]**。

![](./images/browse-namespaces.png)

## 管理自訂命名空間{#manage-namespaces}

根據您的組織資料和使用案例，您可能需要自訂命名空間。 可使用[[!DNL Identity Service]](./api/create-custom-namespace.md) API或透過UI建立自訂命名空間。

若要使用UI建立自訂命名空間，請導覽至&#x200B;**[!UICONTROL Identities]**&#x200B;工作區，選取&#x200B;**[!UICONTROL Browse]**，然後選取&#x200B;**[!UICONTROL Create identity namespace]**。

![](./images/create.png)

出現&#x200B;**[!UICONTROL Create identity namespace]**&#x200B;對話框。 提供唯一的&#x200B;**[!UICONTROL Display name]**&#x200B;和&#x200B;**[!UICONTROL Identity symbol]**，然後選擇要建立的身份類型。 您也可以新增選擇性說明，以進一步瞭解命名空間。 除&#x200B;**非人員識別碼**&#x200B;之外的所有識別類型都遵循相同的拼接行為。 如果您在建立命名空間時選擇「非人員識別碼&#x200B;**」作為識別類型，則不會進行拼接。**&#x200B;有關每個身份類型的具體資訊，請參閱[身份類型](#identity-types)上的表。

完成後，選擇&#x200B;**[!UICONTROL Create]**。

>[!IMPORTANT]
>
>您定義的名稱空間是貴組織專用的，且需要唯一的識別符號，才能成功建立。

![](./images/create-namespace.png)

與標準名稱空間類似，您可以從&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中選擇自訂名稱空間，以檢視其詳細資訊。 不過，使用自訂命名空間，您也可以從詳細資料區域編輯其顯示名稱和說明。

>[!NOTE]
>
>命名空間一旦建立後，就無法刪除，其標識符號和類型也無法更改。

## 身分資料中的命名空間

提供身分的命名空間取決於您提供身分資料的方法。 有關提供資料身份資料的詳細資訊，請參閱[!DNL Identity Service]概述中關於提供身份資料](./home.md#supplying-identity-data-to-identity-service)的部分。[

## 後續步驟

現在，您已瞭解身分名稱空間的主要概念，可以開始學習如何使用[身分圖表檢視器](./ui/identity-graph-viewer.md)來處理您的身分圖表。
