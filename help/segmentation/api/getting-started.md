---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 區段服務開發人員指南
topic: developer guide
translation-type: tm+mt
source-git-commit: 38762fa57188ed018c4347c07765f3d09daef2e6

---


# 區段服務開發人員指南

細分功能可讓您在Adobe Experience Platform中，根據即時客戶個人檔案資料建立細分並產生受眾。

## 快速入門

本指南需要有效瞭解使用區段所涉及的各種Adobe Experience Platform服務。

- [區段](../home.md):可讓您從即時客戶個人檔案資料建立受眾細分。
- [體驗資料模型(XDM)系統](../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
- [即時客戶個人檔案](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [沙盒](../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用API成功使用區段。

### 讀取範例API呼叫

區段服務API檔案提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 必要的標題

API檔案也要求您完成驗證教學課 [程](../../tutorials/authentication.md) ，才能成功呼叫平台端點。 完成驗證教學課程時，會針對Experience Platform API呼叫中的每個必要標題提供值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定執行操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>**注意：** 如需在Experience Platform中使用沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md).

## Segment definitions

Segment definitions define which profiles will be part of which audience segments. You can use the `/segment/definitions` endpoint to retrieve a list of segment definitions, create a new segment definition, retrieve details of a specific segment definition, delete a specific segment definition, or overwrite details of a specific segment definition.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md). -->

## 區段工作

區段工作會處理先前建立的區段定義，以產生觀眾區段。 您可以使用端 `/segment/jobs` 點來擷取區段工作的清單、建立新的區段工作、擷取特定區段工作的詳細資料或刪除特定區段工作。

如需使用此端點的詳細資訊，請閱讀區段工 [作開發人員指南](./segment-jobs.md)。

## 後續步驟

若要開始使用分段API進行呼叫，請選取其中一個子指南，以瞭解如何使用特定的分段相關端點。 若要進一步瞭解如何使用平台UI的區段，請參閱區 [段使用指南](../ui/overview.md)。