---
title: XDM中的敏感與個人資訊
description: 了解Experience Data Model(XDM)中有關敏感個人資訊(SPI)和個人識別資訊(PII)的主要考量事項。
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 9785b252b7c9cb3513858476753b6b4f71277ed7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# XDM中的敏感與個人資訊

Experience Data Model(XDM)提供標準資料結構，可在Adobe Experience Platform中使用，讓您收集客戶體驗的資料。 此資料可包含敏感個人資訊(SPI)和個人識別資訊(PII)，例如客戶的電子郵件地址、名稱、帳戶ID和其他資料欄位。

組織規則和法律隱私權法規(例如一般資料保護規範(GDPR))強制限制如何收集、儲存、使用及共用SPI和PII。 因此，請務必考慮在您的資料模型中代表敏感或個人資訊的欄位，並確保您的操作符合組織和法律准則。

本檔案涵蓋XDM中敏感與個人資料的重要考量事項。

## 決定哪些欄位包含敏感或個人資料

SPI和PII的構成非常具體於內容，因此您必須了解您的資料模型、業務營運和適用法規，以判斷哪些結構欄位代表敏感或個人資料。

例如，客戶的法律管轄權對哪些資訊被視為敏感具有直接影響。 GDPR提供SPI和PII的強大定義，但歐洲經濟區(EEA)以外的客戶可能會受到不同定義和限制的約束。

## 處理敏感和個人資料

與敏感和個人資料本身的定義類似，處理此資料的限制也是內容特定的。

客戶同意通常是收集和處理資料及用途的關鍵因素。 根據您客戶所在的法律管轄權，可能需要明確同意才能收集其敏感和個人資料。 即使不需要明確同意，資料處理限制仍會根據隱私權通知對客戶的內容而適用。

請洽詢您的法律團隊，以判斷應針對您的業務使用案例處理敏感和個人資料的方式。

## 限制使用敏感和個人資料

XDM提供多種標準欄位群組和資料類型，以說明相關、常用的資料結構，以支援客戶體驗。 不過，如果建議的標準資源包含您不想在結構中包含的限制欄位，則您不需要使用該資源。

Platform可讓您定義自己的自訂欄位群組和資料類型，讓您在任何可用的標準資源皆不符合您的需求時，能完全掌控資料的結構。 如需如何定義這些自訂資源的詳細資訊，請參閱下列檔案：

* [建立自訂欄位群組](../ui/resources/field-groups.md#create)
* [建立自訂資料類型](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## 後續步驟

本檔案說明XDM中敏感與個人資料的相關重要考量事項。 如需如何建立結構模型以最符合業務使用案例的詳細資訊，請參閱 [資料模型最佳實務](./best-practices.md).

如需Experience Platform中資料控管和隱私權功能的詳細資訊，請參閱 [控管、隱私權和安全性](../../landing/governance-privacy-security/overview.md).
