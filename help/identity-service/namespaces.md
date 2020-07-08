---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---


# 身分命名空間概觀

身份名稱空間是用 [!DNL Identity Service](./home.md) 作身份相關上下文的指標的元件。 例如，他們會將&quot;name<span>@email.com&quot;值區分為電子郵件地址，或將&quot;443522&quot;區分為數值CRM ID。

## 快速入門

使用身分名稱空間需要瞭解所涉及的各種Adobe Experience Platform服務。 開始使用名稱空間之前，請先閱讀下列服務的檔案：

- [!DNL Real-time Customer Profile](../profile/home.md): 根據來自多個來源的匯整資料，即時提供統一的客戶個人檔案。
- [!DNL Identity Service](./home.md): 跨裝置和系統橋接身分，以更全面地瞭解個別客戶及其行為。
- [!DNL Privacy Service](../privacy-service/home.md): 身分名稱空間用於遵守通用資料保護規則(GDPR)，在GDPR中，可以相對於名稱空間提出GDPR請求。

## 瞭解身分名稱空間

完全限定身份包括ID值和命名空間。 當跨描述檔片段比對記錄資料時(如合 [!DNL Real-time Customer Profile] 並描述檔資料時)，識別值和命名空間都必須相符。

例如，兩個描述檔片段可能包含不同的主要ID，但是它們對「電子郵件」命名空間的值相同，因此平台可以看到這些片段實際上是相同的個人，並將資料匯整到個人的識別圖中。

![](images/identity-service-stitching.png)

### 身分類型

資料可由數種不同的身分類型識別。 在建立身份名稱空間時指定身份類型，並控制資料是否保存到身份圖以及如何處理該資料的任何特殊說明。

下列識別類型可在中使用 [!DNL Platform]:

| 身分類型 | 說明 |
| --- | --- |
| Cookie | 這些身份對於擴展至關重要，並且是身份圖的大部分。 然而，從本質上講，它們會迅速衰敗，並隨著時間而失去價值。 刪除Cookie會特別在識別圖中處理。 |
| 跨裝置 | 這表明， [!DNL Identity Service] 應將此視為強大的人物識別碼，並永久保留。 例如登入ID、CRM ID、忠誠度ID等。 |
| 裝置 | 包含IDFA、GAID和其他IOT ID。 家庭中的人可以分享。 |
| 電子郵件 | 此類型的身分識別資訊(PII)。 這是一個靈敏 [!DNL Identity Service] 地處理值的指標。 |
| 行動 | 此類型的身份包括PII。 這是一個靈敏地處 [!DNL Identity Service] 理這個值的指示。 |
| 非人 | 用於儲存需要名稱空間但未綁定到人員群集的標識符。 然後，從標識圖中過濾這些標識符。 可能的使用案例包括與產品、組織、商店等相關的資料。 （例如產品SKU。） |
| 電話 | 此類型的身份包括PII。 這表明該 [!DNL Identity Service] 值處理靈敏。 |

### 標準名稱空間

Adobe Experience Platform提供數個可供所有組織使用的身分名稱空間。 這些名稱空間稱為標準名稱空間，可使用 [!DNL Identity Service] API或透過 [!DNL Platform] UI顯示。

若要在UI中檢視「標準」名稱空間，請按一 **[!UICONTROL 下左側導軌中的]** 「身分識別」，然後按一下「 *[!UICONTROL 瀏覽]* 」標籤。 您的組織可存取的所有身分名稱空間都會顯示出來，但以「[!UICONTROL Standard]」為「[!UICONTROL Owner]」的身分名稱空間是Adobe提供的「標準」名稱空間。

然後，您可以按一下其中一個列出的名稱空間，以檢視詳細資訊。

![](./images/standard-namespace-detail.png)

## 管理組織的命名空間

根據您的組織資料和使用案例，您可能需要自訂命名空間。

在UI中，這些名稱空間會顯示為「自[!UICONTROL 訂]」為「擁有[!UICONTROL 者]」。 您可使用 [!DNL Identity Service] API或使用者介面來建立自訂命名空間。

若要使用UI建立自訂命名空間，請按一下「 **[!UICONTROL 建立身分命名空間]**」，然後完成對話方塊並按一下「 **[!UICONTROL 建立」]**。

您定義的名稱空間是專屬於您的組織，且需要唯一的「[!UICONTROL Identity Symbol]」（若您使用API，則為「程式碼」），才能成功建立。

![](./images/create-identity-namespace.png)

與「標準」名稱空間類似，您可以從「瀏覽」索引標籤按一下「自訂」名稱空間來檢視其詳細資訊，但是使用「自訂」名稱空間，您也可以從詳細資訊區域編輯其「顯示名稱」和「說明」。 **

>[!NOTE]
>
>命名空間一旦建立後，就無法刪除，其「身分符號」（或API中的「程式碼」）和「類型」也無法變更。

## 身分資料中的命名空間

提供身分的命名空間取決於您提供身分資料的方法。 有關提供資料身分資料的詳細資訊，請參閱總 [覽中有關提供身](./home.md#supplying-identity-data-to-identity-service) 分資料 [!DNL Identity Service] 的章節。
