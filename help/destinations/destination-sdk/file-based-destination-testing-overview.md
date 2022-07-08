---
description: 基於檔案的目標測試API是端點的集合，您可以使用它來驗證通過Destination SDK構建的基於檔案的目標的配置。
title: 基於檔案的目標測試API
source-git-commit: d2d362f4b61e04fc2fa4d9cd9db70ed94a850642
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# 基於檔案的目標測試API

## 總覽 {#overview}

基於檔案的目標測試API是一組端點，您可以使用這些端點來驗證通過Destination SDK構建的基於檔案的目標的配置。

我們建議先使用這些工具驗證您的配置 [提交](submit-destination.md) 您的目的地，以便查看Adobe。

為獲得最佳測試結果，我們建議根據下面的流程圖使用此API。

![顯示建議的目標測試流的圖表](assets/file-based-testing-flow.png)

有關每個端點可以執行的操作的簡要概述，請參閱以下各節。

## 示例生成終結點 {#sample-generation-endpoint}

此終結點幫助您基於現有源架構生成示例配置檔案。

示例配置檔案旨在幫助您瞭解配置檔案的JSON結構。 此外，它們還為您提供了一個骨幹，您可以使用自己的配置檔案資料進行自定義，以便進行進一步的目標測試。

查看 [專用文檔](file-based-sample-profile-generation-api.md) 瞭解如何生成示例配置檔案。

## 目標配置測試終結點 {#destination-configuration-testing-endpoint}

此終結點可幫助您在正確配置基於檔案的目標時進行test，並驗證到已配置目標的資料流的完整性。

可以在添加或不添加的情況下向測試端點發出請求 [示例配置檔案](file-based-sample-profile-generation-api.md) 電話。 如果您未在請求上發送任何配置檔案，則API將自動生成示例配置檔案並將其添加到請求中。

查看 [專用文檔](file-based-destination-testing-api.md) 瞭解如何使用示例配置檔案test目標配置。

## 激活結果終結點 {#activation-results}

此終結點可幫助您查看基於檔案的目標測試結果的完整詳細資訊。

此API終結點返回的結果與使用 [流服務API](../api/update-destination-dataflows.md) 監視資料流。

查看 [專用文檔](file-based-destination-results-api.md) 瞭解如何查看詳細的激活結果。

## 客戶欄位呈現終結點 {#customer-fields-rendering-endpoint}

此終結點可幫助您直觀地顯示模板化方式 [客戶資料欄位](file-based-destination-configuration.md#customer-data-fields) 在目標配置中定義。

終結點為客戶資料欄位生成隨機值，並在響應中返回這些值。 這有助於驗證客戶資料欄位的語義結構，如儲存段名稱或資料夾路徑。

查看 [專用文檔](file-based-render-template-api.md) 瞭解如何查看詳細的激活結果。