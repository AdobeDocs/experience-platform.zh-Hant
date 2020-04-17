---
title: 即時客戶資料設定檔中的隱私權
seo-title: 即時客戶資料設定檔中的隱私權
description: 即時客戶資料設定檔可讓您簡化維持資料作業符合隱私權規範的程式。
seo-description: 即時客戶資料設定檔可讓您簡化維持資料作業符合隱私權規範的程式。
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# 即時CDP中的隱私權

即時客戶資料平台（即時CDP）可協助行銷人員將來自多個企業系統的資料整合在一起，讓他們能夠更好地識別、瞭解並吸引客戶。 Adobe將消費者資料隱私視為基本的設計原則，並提供各種控制項以協助行銷人員管理其客戶的資料隱私。

大部分的即時CDP功能都由Adobe Experience Platform提供支援。 本檔案提供有關即時CDP支援的各種隱私權增強技術的資訊，並提供Experience Platform檔案的連結，以取得詳細資訊。

## 隱私權服務

Adobe Experience Platform Privacy Service可讓您簡化程式，確保資料作業符合隱私權規範，例如通用資料保護規則(GDPR)和加州消費者隱私權法案(CCPA)。 由於即時CDP利用Experience Platform功能收集和儲存資料，因此應在平台中管理對GDPR和CCPA的訪問和刪除請求。 如需服務 [的詳細簡介](../../privacy-service/home.md) ，請參閱隱私權服務概觀檔案。

提交個別GDPR和CCPA資料主體要求存取和刪除客戶資料的方法有兩種：

* 使用隱 [私服務UI](https://gdprui.cloud.adobe.io/) ，在視覺化工作區中建立和監控存取和刪除要求。 請參閱 [隱私服務UI教學課程](../../privacy-service/ui/overview.md) ，以取得逐步指示。
* 使用隱 [私服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) ，透過REST風格的API呼叫來管理存取和刪除請求。 如需逐步 [指示，請參閱Privacy Service API教學課程](../../privacy-service/api/getting-started.md) 。

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## 後續步驟

本文檔簡要介紹了即時CDP的隱私權功能。 如需提交存取／刪除要求之最佳實務和步驟的詳細資訊，請參閱隱私權服 [務檔案](../../privacy-service/home.md)。