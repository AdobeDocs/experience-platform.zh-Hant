---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: 策略實施概述
topic: enforcement
description: 一旦資料使用標籤套用至Adobe Experience Platform資料集，並為針對這些標籤的行銷動作定義資料使用原則後，「資料治理」功能可讓您強制執行這些原則並防止構成違反原則的資料作業。 Data Governance功能在平台上提供兩種策略實施方法：基於API的實施和自動實施。
translation-type: tm+mt
source-git-commit: 2fdab7d984a7368df77110f8ba0e0ba687e96d7e
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 策略實施概述

一旦資料使用標籤套用至資料集 [!DNL Platform] ，並且已針對這些標籤定義資料使用策略以執行行銷動作， [!DNL Data Governance] 這些功能可讓您強制執行這些原則並防止構成違反原則的資料作業。

政策執行的方法有兩種： [!DNL Data Governance][!DNL Platform]**以API為基礎的強制** ，以及 **自動強制**。

## 以API為基礎的強制

API [!DNL Policy Service] 提供端點，可讓您針對資料集或資料使用標籤的任意組合來測試行銷動作，以檢查是否發生任何違反原則的情況。 然後，您可以根據API回應，在體驗應用程式中設定通訊協定，以適當強制符合資料使用原則。

如需如何使用API [評估策略](api-enforcement.md) ，請參閱策略實施教學課程。

## 自動強制

某些以（例如）為基礎的應用程 [!DNL Experience Platform] 式可自動強 [!DNL Real-time Customer Data Platform]制執行資料使用政策。 每個應用程式都維護自己的方法來呈現違反策略的情況並提供解決問題的步驟。

如需自動資料使用原則實 [!DNL Platform]施的詳細資訊，請參閱您所使用之應用程式的檔案。 有關即時CDP中自動執行策略的資訊，請參閱即時CDP [資料治理概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。