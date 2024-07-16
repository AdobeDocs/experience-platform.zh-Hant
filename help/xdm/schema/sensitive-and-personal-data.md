---
title: XDM中的敏感和個人資訊
description: 瞭解關於Experience Data Model (XDM)中敏感個人資訊(SPI)和個人識別資訊(PII)的主要考量事項。
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 302dca9a9f834dba1fd3fdac15284ea4e2fba282
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# XDM中的敏感和個人資訊

Experience Data Model (XDM)提供用於Adobe Experience Platform的標準資料結構，可讓您收集客戶體驗的資料。 此資料可能包含敏感的個人資訊(SPI)和個人識別資訊(PII)，例如客戶的電子郵件地址、姓名、帳戶ID和其他資料欄位。

一般資料保護規範(GDPR)等組織規則和法律隱私權法規會強制限制SPI和PII的收集、儲存、使用和共用方式。 因此，請務必考慮哪些欄位代表資料模型中的敏感或個人資訊，並確保您的作業符合組織和法律准則。

本文介紹XDM中敏感資料和個人資料的相關考量事項。

## 決定哪些欄位包含敏感或個人資料

構成SPI和PII的內容與內容非常相關，因此，您可以自行瞭解您的資料模型、業務營運和適用的法規，以決定哪些結構描述欄位代表敏感或個人資料。

例如，客戶的法律管轄區會直接影響哪些資訊被視為敏感。 GDPR為SPI和PII提供完善的定義，但歐洲經濟區(EEA)以外的客戶可能有不同的定義和限制。

## 處理敏感和個人資料

與敏感資料和個人資料本身的定義類似，處理此資料的限制也是內容特定的。

就可收集和處理哪些資料以及出於哪些目的而言，客戶同意通常是關鍵因素。 根據您客戶的法律管轄範圍，收集其敏感和個人資料可能需要明確同意。 即使不需要明確同意，根據隱私權通知對客戶的內容，資料處理限制仍適用。

請洽詢您的法律團隊，以決定針對您的業務使用案例處理敏感和個人資料的方式。

## 限制使用敏感和個人資料

XDM提供各種標準欄位群組和資料型別，以說明可強化客戶體驗的相關常用資料結構。 但是，如果建議的標準資源包含您不想包含在結構描述中的受限制欄位，則不必使用該資源。

Platform可讓您定義自己的自訂欄位群組和資料型別，讓您在任何可用的標準資源無法滿足您的需求時，可以完全控制資料的結構。 請參閱下列檔案，以取得如何定義這些自訂資源的詳細資訊：

* [建立自訂欄位群組](../ui/resources/field-groups.md#create)
* [建立自訂資料型別](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

>[!IMPORTANT]
>
>SPI和PII應該只儲存到[XDM個別設定檔](../classes/individual-profile.md)和[XDM ExperienceEvent](../classes/experienceevent.md)類別中。 請勿將SPI和PII儲存在任何其他自訂或標準XDM類別中，做為資料刪除和隱私權及治理用途的最佳作法。

## 後續步驟

本檔案涵蓋XDM中敏感和個人資料的相關重要考量事項。 如需如何模型化您的結構以最符合業務使用案例的詳細資訊，請參閱[資料模型化最佳實務](./best-practices.md)指南。

如需Experience Platform資料控管和隱私權功能的詳細資訊，請參閱[控管、隱私權及安全性](../../landing/governance-privacy-security/overview.md)的概觀。
