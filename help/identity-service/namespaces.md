---
keywords: Experience Platform；首頁；熱門主題；命名空間；命名空間；命名空間；標識名稱空間；標識名稱空間；標識名稱空間；標識；標識；標識服務；標識服務
solution: Experience Platform
title: Identity Namespace概述
description: 身分識別命名空間是 Identity Service 的元件，用途是作為身分識別相關內容的指標。 例如，它們將值"name@email.com"區分為電子郵件地址，或將值"443522"區分為數字CRM ID。
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 482de6a50d14b9de095014b070ce400a2fd273cc
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 8%

---

# Identity命名空間概述

標識命名空間是 [[!DNL Identity Service]](./home.md) 作為身份相關背景的指標。 例如，它們會區分「 name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數字CRM ID。

## 快速入門

使用身分命名空間需先了解所涉及的各種 Adobe Experience Platform 服務。開始使用命名空間之前，請先檢閱下列服務文件：

- [[!DNL Real-Time Customer Profile]](../profile/home.md):根據來自多個來源的聚合資料即時提供統一的客戶配置檔案。
- [[!DNL Identity Service]](./home.md):通過跨設備和系統橋接身份，更好地瞭解單個客戶及其行為。
- [[!DNL Privacy Service]](../privacy-service/home.md):身份命名空間用於法律隱私法規(如一般資料保護法規(GDPR))的合規性請求。 每個隱私請求都相對於命名空間進行，以便確定哪些使用者的資料應受到影響。

## 瞭解標識命名空間

完全限定的標識包括ID值和命名空間。 在配置檔案片段間匹配記錄資料時，如何 [!DNL Real-Time Customer Profile] 合併配置檔案資料，標識值和命名空間必須匹配。

例如，兩個配置檔案片段可能包含不同的主ID，但它們共用「Email」命名空間的相同值，因此 [!DNL Platform] 能夠看到這些片段實際上是同一個個體並且把資料集合在個體的身份圖中

![](images/identity-service-stitching.png)

### 標識類型 {#identity-types}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="指定身分識別類型"
>abstract="身分識別類型控制資料是否儲存到身分識別圖中。非人識別碼不會儲存，所有其他身分識別類型都會儲存。"
>text="Learn more in documentation"

資料可以由幾種不同的標識類型來標識。 標識類型是在建立標識命名空間時指定的，並控制資料是否永續到標識圖形以及如何處理該資料的任何特殊說明。 除外的所有標識類型 **非人員標識符** 按照將命名空間及其相應ID值拼接到標識圖簇的相同行為進行操作。 使用時資料不會拼接在一起 **非人員標識符**。

以下標識類型在 [!DNL Platform]:

| 標識類型 | 說明 |
| --- | --- |
| Cookie ID | Cookie ID標識Web瀏覽器。 這些身份對於擴展至關重要，並且構成了身份圖的大部分。 然而，從本質上講，它們會迅速衰敗，並逐漸失去價值。 |
| 跨設備ID | 跨設備ID標識單個ID，並通常將其他ID連接在一起。 示例包括登錄ID、CRM ID和會員ID。 這表示 [!DNL Identity Service] 以靈敏地處理價值。 |
| 設備ID | 設備ID標識硬體設備，如IDFA(iPhone和iPad)、GAID(Android)和RIDA(Roku)，可由家庭中的多人共用。 |
| 電子郵件地址 | 電子郵件地址通常與一個人關聯，因此可以用於通過不同渠道識別此人。 此類型的身份包括個人身份資訊(PII)。 這表示 [!DNL Identity Service] 以靈敏地處理價值。 |
| 非人員識別碼 | 非人員ID用於儲存需要命名空間但未連接到人員群集的標識符。 例如，產品SKU、與產品、組織或商店相關的資料。 |
| 電話號碼 | 電話號碼通常與一個人關聯，因此可以用於通過不同渠道識別此人。 此類型的身份包括PII。 這表明 [!DNL Identity Service] 以靈敏地處理價值。 |

### 標準命名空間 {#standard}

Experience Platform提供了多個可用於所有組織的標識命名空間。 這些名稱空間稱為標準命名空間，使用 [!DNL Identity Service] API或通過平台UI。

以下標準命名空間可供平台內的所有組織使用：

| 顯示名稱 | 說明 |
| ------------ | ----------- |
| AdCloud | 表示AdobeAdCloud的命名空間。 |
| Adobe Analytics（傳統ID） | 表示Adobe Analytics的命名空間。 請參閱以下文檔 [Adobe Analytics命名空間](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) 的子菜單。 |
| AppleIDFA（廣告商ID） | 表示廣告商的AppleID的命名空間。 請參閱以下文檔 [基於興趣的廣告](https://support.apple.com/en-us/HT202074) 的子菜單。 |
| Apple推送通知服務 | 表示使用Apple推送通知服務收集的標識的命名空間。 請參閱以下文檔 [Apple推送通知服務](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) 的子菜單。 |
| 核心 | 表示Adobe Audience Manager的命名空間。 此命名空間也可以通過其舊名稱引用：&quot;Adobe AudienceManager&quot; 請參閱以下文檔 [Audience ManagerID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) 的子菜單。 |
| ECID | 表示ECID的命名空間。 以下別名也可以引用此命名空間：&quot;Adobe Marketing CloudID&quot;,&quot;Adobe Experience CloudID&quot;,&quot;Adobe Experience PlatformID&quot; 請參閱以下文檔 [ECID](./ecid.md) 的子菜單。 |
| 電子郵件 | 表示電子郵件地址的命名空間。 此類型的命名空間通常與單個人關聯，因此可用於跨不同渠道標識該人。 |
| 電子郵件（SHA256，小寫） | 預散列電子郵件地址的命名空間。 在使用SHA256散列之前，此命名空間中提供的值將轉換為小寫。 在對電子郵件地址進行規範化之前，需要裁剪前導空格和尾隨空格。 無法追溯更改此設定。 請參閱以下文檔 [SHA256散列支援](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 的子菜單。 |
| Firebase雲消息 | 表示使用GoogleFirebase雲消息為推送通知收集的身份的命名空間。 請參閱以下文檔 [GoogleFirebase雲消息](https://firebase.google.com/docs/cloud-messaging) 的子菜單。 |
| Google廣告ID(GAID) | 表示Google廣告ID的命名空間。 請參閱以下文檔 [Google廣告ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 的子菜單。 |
| Google按一下ID | 表示Google按一下ID的命名空間。 請參閱以下文檔 [在Google廣告中點擊跟蹤](https://developers.google.com/adwords/api/docs/guides/click-tracking) 的子菜單。 |
| 電話 | 表示電話號碼的命名空間。 此類型的命名空間通常與單個人關聯，因此可用於跨不同渠道標識該人。 |
| 電話(E.164) | 表示需要以E.164格式散列的原始電話號碼的命名空間。 E.164格式包括加號(`+`)、國際國家/地區呼叫代碼、本地區代碼和電話號碼。 例如: `(+)(country code)(area code)(phone number)`. |
| 電話(SHA256) | 表示需要使用SHA256散列的電話號碼的命名空間。 必須刪除符號、字母和任何前導零。 您還必須將國家/地區的調用代碼添加為前置詞。 |
| 電話(SHA256_E.164) | 表示需要使用SHA256和E.164格式散列的原始電話號碼的命名空間。 |
| TNTID | 表示Adobe Target的命名空間。 請參閱以下文檔 [目標](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) 獲取更多資訊。 |
| Windows AID | 表示Windows廣告ID的命名空間。 請參閱以下文檔 [Windows廣告ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) 的子菜單。 |

### 查看標識命名空間 {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="檢視整合身分"
>abstract="整合身分識別是用於連接其他系統的命名空間，不用於身分識別解析或拼接身分識別。<br>這些身分依預設是隱藏的。使用切換來檢視整合命名空間。"

要在UI中查看標識命名空間，請選擇 **[!UICONTROL 身份]** 在左側導航中，然後選擇 **[!UICONTROL 瀏覽]**。

![瀏覽](./images/browse.png)

標識命名空間的清單將出現在頁面的主介面中，其中顯示了有關其名稱、標識符號、上次更新日期的資訊，以及它們是標準命名空間還是自定義命名空間。 右滑軌包含有關 [!UICONTROL 標識圖強度]。

![身份](./images/identities.png)

平台還提供用於整合目的的命名空間。 預設情況下，這些命名空間會隱藏，因為它們用於與其他系統連接，而不用於縫合標識。 要查看整合命名空間，請選擇 **[!UICONTROL 查看整合標識]**。

![視圖整合 — 標識](./images/view-integration-identities.png)

從清單中選擇標識命名空間以查看有關特定命名空間的資訊。 選擇標識名稱空間將更新右欄上的顯示，以顯示與您選擇的標識名稱空間相關的元資料，包括接收的標識數和失敗和跳過的記錄數。

![select-namespace](./images/select-namespace.png)

## 管理自定義命名空間 {#manage-namespaces}

根據您的組織資料和使用案例，您可能需要自定義命名空間。 可以使用 [[!DNL Identity Service]](./api/create-custom-namespace.md) API或通過UI。

要使用UI建立自定義命名空間，請導航到 **[!UICONTROL 身份]** 工作區，選擇 **[!UICONTROL 瀏覽]**，然後選擇 **[!UICONTROL 建立標識命名空間]**。

![選擇建立](./images/select-create.png)

的 **[!UICONTROL 建立標識命名空間]** 對話框。 提供唯一 **[!UICONTROL 顯示名稱]** 和 **[!UICONTROL 身份符號]** 然後選擇要建立的標識類型。 您還可以添加可選說明以添加有關命名空間的詳細資訊。 所有標識類型(除 **非人員標識符** 跟拼接一樣。 如果選擇 **非人員標識符** 作為建立命名空間時的標識類型，不會進行縫合。 有關每個標識類型的特定資訊，請參閱上的表 [標識類型](#identity-types)。

完成後，選擇 **[!UICONTROL 建立]**。

>[!IMPORTANT]
>
>您定義的命名空間對您的組織是專用的，並且需要唯一的標識符才能成功建立。

![create-identity-namespace](./images/create-identity-namespace.png)

與標準命名空間類似，您可以從 **[!UICONTROL 瀏覽]** 頁籤。 但是，使用自定義命名空間，您還可以從詳細資訊區域編輯其顯示名稱和說明。

>[!NOTE]
>
>命名空間一旦建立，就無法刪除，其標識符和類型也無法更改。

## 標識資料中的命名空間

為身份提供命名空間取決於您用於提供身份資料的方法。 有關提供資料標識資料的詳細資訊，請參閱 [提供身份資料](./home.md#supplying-identity-data-to-identity-service) 的 [!DNL Identity Service] 概述。

## 後續步驟

現在，您已經瞭解了標識命名空間的關鍵概念，可以開始學習如何使用標識圖 [標識圖查看器](./ui/identity-graph-viewer.md)。
