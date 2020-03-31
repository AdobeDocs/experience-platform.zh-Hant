---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 資料使用政策概觀
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# 資料使用政策概觀

為了讓資料使用標籤有效支援資料合規性，必須實作資料使用政策。 資料使用原則是描述您在Experience Platform內對資料執行的行銷動作類型或限制的規則。

行銷動作的範例可能是想要將資料集匯出至第三方服務。 如果有原則指出無法匯出特定類型的資料，例如個人識別資訊(PII)，且「I」標籤（身分資料）已套用至資料集，您會收到來自原則服務的回覆，告知您已違反資料使用原則。

## 如何建立和使用資料使用政策

在套用資料使用標籤後，資料管理員就可以使用 [DULE Policy Service API建立原則](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。

身為資料管理員，您可以使用原則服務API來管理和評估與針對包含DULE標籤的資料所執行之行銷動作相關的原則。 使用API，您可以建立和更新原則、判斷原則的狀態，以及使用行銷動作來評估特定動作是否違反資料使用原則。

在「原則服務API」中，所有原則和行銷動作皆稱為 `core` 或資 `custom` 源。 `core` 資源由Adobe定義和維護，而資 `custom` 源則由個別客戶建立和維護。 因此， `custom` 資源是唯一的，並且僅對建立資源的組織可見。

有關執行DULE Policy Service API提供的關鍵操作的詳細資訊，請參 [閱Policy Service開發人員指南](../api/getting-started.md)。 有關使用DULE策略的逐步說明，請參見有關建立和評估DULE策 [略的教程](create.md)。