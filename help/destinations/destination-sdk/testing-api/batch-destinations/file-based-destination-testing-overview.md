---
description: 了解如何使用檔案式目的地測試API，驗證透過Destination SDK建置的檔案式目的地組態。
title: 檔案式目的地測試API
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# 檔案式目的地測試API概觀

檔案式目的地測試API是一組端點，可用來驗證透過Destination SDK建置的檔案式目的地組態。

建議您先使用這些工具來驗證您的設定 [提交](../../guides/submit-destination.md) 您要審核的目的地Adobe。

為獲得最佳測試結果，建議您根據下列流程圖使用此API。

![顯示建議目的地測試流程的圖表](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

請參閱以下各節，概略了解每個端點的功能。

## 產生範例設定檔 {#generate-sample-profiles}

使用 `/sample-profiles` API端點，根據您現有的來源架構產生範例設定檔。

範例設定檔可協助您了解設定檔的JSON結構。 此外，它們也提供您預設值，您可以使用自己的設定檔資料加以自訂，以進一步進行目的地測試。

請參閱 [專屬檔案](file-based-sample-profile-generation-api.md) 了解如何產生範例設定檔。

## 測試目標配置 {#test-destination-configuration}

使用 `/testing/destinationInstance` API端點，以測試您的檔案式目的地是否已正確設定，以及驗證資料流至您已設定目的地的完整性。

您可以使用或不新增，向測試端點提出請求 [範例設定檔](file-based-sample-profile-generation-api.md) 呼叫。 如果您未在請求上傳送任何設定檔，API會自動產生範例設定檔，並將其新增至請求。

請參閱 [專屬檔案](file-based-destination-testing-api.md) 了解如何使用範例設定檔測試您的目的地設定。

## 查看詳細的激活結果 {#view-detailed-activation-results}

使用 `/testing/destinationInstance` API端點，供您檢視檔案式目的地測試結果的完整詳細資訊。

此API端點會傳回與使用 [流量服務API](../../../api/update-destination-dataflows.md) 監視資料流。

請參閱 [專屬檔案](file-based-destination-results-api.md) 了解如何檢視詳細的啟動結果。

## 呈現客戶資料欄位 {#render-customer-data-fields}

使用 `/authoring/testing/template/render` API端點，將範本化方式視覺化 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 在目的地設定中定義的結果會類似。

API端點會為您的客戶資料欄位產生隨機值，並在回應中傳回這些值。 這可協助您驗證客戶資料欄位（例如貯體名稱或資料夾路徑）的語義結構。

請參閱 [專屬檔案](file-based-render-template-api.md) 了解如何為客戶資料欄位產生和視覺化值。
