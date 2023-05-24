---
title: XDM中的敏感和個人資訊
description: 瞭解有關體驗資料模型(XDM)中敏感個人資訊(SPI)和個人識別資訊(PII)的主要注意事項。
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 9785b252b7c9cb3513858476753b6b4f71277ed7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# XDM中的敏感和個人資訊

體驗資料模型(XDM)提供標準資料結構供Adobe Experience Platform使用，使您能夠收集有關客戶體驗的資料。 此資料可以包括敏感個人資訊(SPI)和個人識別資訊(PII)，如客戶的電子郵件地址、名稱、帳戶ID和其他資料欄位。

組織規則和法律隱私法規(如一般資料保護條例(GDPR))對如何收集、儲存、使用和共用SPI和PII實施了限制。 因此，必須考慮在資料模型中哪些欄位代表敏感或個人資訊，並確保您的操作符合組織和法律准則。

本文檔介紹了XDM中有關敏感和個人資料的關鍵注意事項。

## 確定哪些欄位包含敏感或個人資料

SPI和PII的構成非常特定於上下文，因此您需要瞭解您的資料模型、業務運營和適用的法規，以確定哪些架構欄位代表敏感或個人資料。

例如，客戶的法律管轄權對哪些資訊被視為敏感資訊具有直接影響。 GDPR為SPI和PII提供了強有力的定義，但歐洲經濟區(EEA)之外的客戶可能受到不同定義和限制的影響。

## 處理敏感和個人資料

與敏感和個人資料本身的定義類似，處理此資料的限制也特定於上下文。

客戶同意通常是收集和處理哪些資料以及出於哪些目的的關鍵因素。 根據客戶所處的法律管轄區，可能需要明確同意才能收集其敏感和個人資料。 即使在不需要明確同意的情況下，資料處理限制仍然適用，具體取決於隱私聲明對客戶說什麼。

請咨詢您的法律團隊，以確定應如何為您的業務使用案例處理敏感和個人資料。

## 限制使用敏感和個人資料

XDM提供了多種標準的現場組和資料類型，以描述相關的、常用的資料結構，為客戶體驗提供動力。 如果建議的標準資源包含您不希望在方案中包括的受限欄位，則您不必使用該資源。

平台允許您定義自己的自定義欄位組和資料類型，使您可以在任何可用的標準資源無法滿足您的需求時，完全控制資料的結構。 有關如何定義這些自定義資源的詳細資訊，請參閱以下文檔：

* [建立自定義欄位組](../ui/resources/field-groups.md#create)
* [建立自定義資料類型](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## 後續步驟

本文檔介紹了XDM中有關敏感和個人資料的關鍵注意事項。 有關如何為架構建模以最好地滿足業務使用案例的詳細資訊，請參閱上的指南 [資料建模的最佳做法](./best-practices.md)。

有關Experience Platform中資料治理和隱私權功能的詳細資訊，請參閱 [治理、隱私和安全](../../landing/governance-privacy-security/overview.md)。
