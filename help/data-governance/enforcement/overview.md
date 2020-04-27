---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略實施概述
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc

---


# 策略實施概述

一旦資料使用標籤套用至平台資料集，並且已針對這些標籤定義資料使用原則以執行行銷動作，資料治理功能可讓您強制執行這些原則並防止構成違反原則的資料作業。

平台上的Data Governance功能提供兩種策略實施方法：以 **API為基礎的強制****與自動強制**。

## 以API為基礎的強制

策略服務API提供端點，允許您針對資料集或資料使用標籤的任意組合測試行銷操作，以檢查是否發生任何策略違規。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制符合資料使用原則。

如需如何使用API [評估策略](api-enforcement.md) ，請參閱策略實施教學課程。

## 自動強制

以Experience Platform為基礎的某些應用程式（例如即時客戶資料平台）可自動強制執行資料使用政策。 每個應用程式都維護自己的方法來呈現違反策略的情況並提供解決問題的步驟。

如需自動資料使用原則實施的詳細資訊，請參閱您所使用之平台應用程式的檔案。 有關即時CDP中自動執行策略的資訊，請參閱即時CDP [資料治理概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。