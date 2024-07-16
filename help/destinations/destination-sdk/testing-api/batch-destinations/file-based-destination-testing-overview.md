---
description: 瞭解如何使用檔案型目的地測試API，驗證透過Destination SDK建立的檔案型目的地設定。
title: 檔案型目的地測試API
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# 檔案型目的地測試API概覽

檔案型目的地測試API是一組端點，可用於驗證透過Destination SDK建立的檔案型目的地設定。

我們建議在[將您的目的地提交](../../guides/submit-destination.md)給Adobe之前，使用這些工具來驗證您的設定。

為獲得最佳測試結果，建議您根據下列流程圖使用此API。

![顯示建議的目的地測試流程的圖表](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

請參閱以下各節，概略瞭解每個端點的功能。

## 產生範例設定檔 {#generate-sample-profiles}

使用`/sample-profiles` API端點根據您現有的來源結構描述產生範例設定檔。

設定檔範例可協助您瞭解設定檔的JSON結構。 此外，它們會提供預設值，您可以使用自己的設定檔資料來自訂，以進行進一步的目的地測試。

請參閱[專屬檔案](file-based-sample-profile-generation-api.md)以瞭解如何產生範例設定檔。

## 測試目的地設定 {#test-destination-configuration}

使用`/testing/destinationInstance` API端點來測試您的檔案型目的地是否已正確設定，以及驗證資料流至您設定之目的地的完整性。

您可以透過或不透過將[範例設定檔](file-based-sample-profile-generation-api.md)新增至呼叫來向測試端點提出要求。 如果您未在請求上傳送任何設定檔，API會自動產生範例設定檔，並將其新增至請求中。

請參閱[專屬檔案](file-based-destination-testing-api.md)，瞭解如何使用範例設定檔測試您的目的地組態。

## 檢視詳細的啟用結果 {#view-detailed-activation-results}

使用`/testing/destinationInstance` API端點可檢視檔案型目的地測試結果的完整詳細資料。

此API端點傳回的結果與使用[流程服務API](../../../api/update-destination-dataflows.md)監視資料流時所取得的結果相同。

請參閱[專屬檔案](file-based-destination-results-api.md)以瞭解如何檢視詳細的啟用結果。

## 呈現客戶資料欄位 {#render-customer-data-fields}

使用`/authoring/testing/template/render` API端點來視覺化目的地設定中定義的範本[客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)的外觀。

API端點會產生客戶資料欄位的隨機值，並在回應中傳回。 這可協助您驗證客戶資料欄位（例如儲存貯體名稱或檔案夾路徑）的語意結構。

請參閱[專屬檔案](file-based-render-template-api.md)，瞭解如何產生和視覺化客戶資料欄位的值。
