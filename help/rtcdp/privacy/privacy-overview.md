---
keywords: 資料管理rtcdp;rtcdp資料管理；即時客戶資料資料描述檔資料管理；隱私權rtcdp;rtcdp隱私
title: 即時客戶資料平台中的隱私權
seo-title: 即時客戶資料平台中的隱私權
description: 即時客戶資料平台可讓您簡化維持資料作業符合隱私權法規的程式。
seo-description: 即時客戶資料平台可讓您簡化維持資料作業符合隱私權法規的程式。
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# 即時客戶資料平台中的隱私權

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP])協助行銷人員將來自多個企業系統的資料整合在一起，讓他們能夠更好地識別、瞭解並吸引客戶。Adobe將消費者資料隱私視為基本的設計原則，並提供各種控制項以協助行銷人員管理其客戶的資料隱私。

[!DNL Real-time CDP]功能大部份都採用Adobe Experience Platform。 本檔案提供[!DNL Real-time CDP]支援的各種隱私權增強技術的相關資訊，以及[!DNL Experience Platform]檔案的連結，以取得詳細資訊。

## 允許客戶存取和刪除請求

[!DNL General Data Protection Regulation](GDPR)和[!DNL California Consumer Privacy Act](CCPA)等法律隱私權法規賦予客戶要求存取或刪除您從他們收集之個人資料的權利。 由於[!DNL Real-time CDP]利用[!DNL Experience Platform]功能進行資料收集和儲存，因此應在[!DNL Platform]內管理客戶存取和刪除其個人資料的請求。 如需詳細資訊，請參閱[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)的概觀。

## 退出功能

[!DNL Real-time CDP] 允許客戶選擇不將個人資料納入區段使用案例。[!DNL Real-time Customer Profile]會擷取並儲存客戶的退出偏好設定，並透過在區段謂語中使用布林邏輯(&quot;AND NOT&quot;)排除已退出區段的使用者，來強制執行這些偏好設定。

如需詳細資訊，請參閱Adobe Experience Platform Segmentation Service檔案中[檔案中的「遵守退出要求」](../../segmentation/honoring-opt-outs.md)。

## IAB TCF 2.0支援

[!DNL Real-time CDP] 以Adobe Experience Platform為基礎，如中所述，Adobe Experience Platform是註冊 [供](https://iabeurope.eu/vendor-list-tcf-v2-0/) 應商 [!DNL Transparency & Consent Framework (TCF)]清單的一部分 [!DNL Interactive Advertising Bureau (IAB)]。根據TCF 2.0的要求，Platform可讓您收集詳細的客戶同意資料，並將其整合到您儲存的客戶個人檔案中。 然後，可根據特定個人檔案的使用案例，將此同意資料納入匯出的受眾細分。

如需詳細資訊，請參閱Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md)中的[IAB TCF 2.0支援概觀。

## 後續步驟

本檔案對[!DNL Real-time CDP]的隱私權功能作了簡要介紹。 請參閱本指南中連結的檔案，以取得各項功能的詳細資訊。