---
keywords: Experience Platform;home;popular topics;DULE;dule
solution: Experience Platform
title: 原則服務API快速入門
topic: developer guide
description: Policy Service API可讓您建立並管理與Adobe Experience Platform資料治理相關的各種資源。 本檔案提供您在嘗試呼叫Policy Service API之前，需要瞭解的核心概念的簡介。
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# API快速入 [!DNL Policy Service] 門

API [!DNL Policy Service] 可讓您建立和管理與Adobe Experience Platform相關的各種資源 [!DNL Data Governance]。 本檔案提供您在嘗試呼叫 [!DNL Policy Service] API之前，需要瞭解的核心概念。

## 必要條件

使用開發人員指南需要瞭解使用「資料管理」 [!DNL Experience Platform] 功能時涉及的各種服務。 在開始使用之前，請先 [!DNL Policy Service API]檢閱下列服務的檔案：

* [[!DNL 資料治理]](../home.md):強制執行資料使用 [!DNL Experience Platform] 合規性的框架。
* [[!DNL 體驗資料模型(XDM)系統]](../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
* [[!DNL 即時客戶基本資料]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

## 讀取範例API呼叫

API文 [!DNL Policy Service] 件提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

## 必要的標題

API檔案也要求您完成驗證教學 [課程](../../tutorials/authentication.md) ，才能成功呼叫端點 [!DNL Platform] 。 完成驗證教學課程可提供 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Data Governance])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 核心與自訂資源

在 [!DNL Policy Service] API中，所有原則和行銷動作皆稱為 `core` 或資 `custom` 源。

`core` 資源是由Adobe定義和維護的資源，而 `custom` 資源則是由您的組織建立和維護的資源，因此，資源是您IMS組織唯一可見的。 因此，清單和查閱作業(`GET`)是唯一允許對資源執行的作業 `core` ，而清單、查閱和更新作業(`POST`、 `PUT``PATCH`和 `DELETE`)則適用於資源 `custom` 。

## 後續步驟

若要開始使用Policy Service API進行呼叫，請選取其中一個可用的端點指南。