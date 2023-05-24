---
title: 在Identity Service中刪除
description: 本文檔概述了可用於刪除Experience Platform中的身份資料的各種機制，並明確了身份圖可能如何受到影響。
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 0%

---

# 在Identity Service中刪除

Adobe Experience Platform身份服務通過確定性地為個人在設備和系統之間連結身份來生成身份圖。 當在同一資料行中接收到兩個或多個標籤標識時，建立標識圖連結。

即時客戶配置檔案利用身份圖形建立客戶屬性和行為的全面、單一視圖，使您能夠即時地向人員而不是設備提供有影響的個人數字型驗。

本文檔概述了可用於刪除Experience Platform中的身份資料的各種機制，並明確了身份圖可能如何受到影響。

## 快速入門

下面的文檔引用了以下Experience Platform功能：

* [身份服務](home.md):通過跨設備和系統橋接身份，更好地瞭解單個客戶及其行為。
   * [標識圖](./ui/identity-graph-viewer.md):身份圖是特定客戶不同身份之間關係的映射，它為您提供了客戶如何通過不同渠道與您的品牌進行交互的直觀表示。
   * [標識命名空間](namespaces.md):標識名稱空間是標識服務的一個元件，用作標識與之相關的上下文的指示符。 例如，它們會區分「 name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數字CRM ID。
* [目錄服務](../catalog/home.md):瀏覽資料湖中的資料沿襲、元資料、檔案說明、目錄和資料集。
* [資料衛生](../hygiene/home.md):通過計畫自動資料集過期或從一個資料集或所有資料集中刪除單個記錄來管理儲存的消費者資料。
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md):管理客戶訪問、選擇退出銷售或刪除其跨Adobe Experience Cloud應用程式的個人資料的請求。
* [即時客戶配置檔案](../profile/home.md):根據來自多個來源的聚合資料即時提供統一的客戶配置檔案。

## 單一身份刪除

單個標識刪除請求允許您刪除圖形中的標識，從而刪除與與標識命名空間關聯的單個用戶標識關聯的連結。 Uou可以使用由 [Privacy Service](../privacy-service/home.md) 例如，客戶請求刪除資料並遵守隱私法規(如一般資料保護法規(GDPR))等。

以下各節概述了在Experience Platform中可用於單個身份刪除請求的機制。

### Privacy Service中的單個標識刪除

Privacy Service處理客戶訪問請求、選擇退出銷售或刪除其個人資料的請求，這些資料由隱私法規(如一般資料保護法規(GDPR)和加利福尼亞消費者隱私法(CCPA))規定。 使用Privacy Service，可以使用API或UI提交作業請求。 當Experience Platform從Privacy Service接收到刪除請求時，平台會向Privacy Service發送確認，確認該請求已被接收，並且受影響的資料已被標籤為刪除。 單個標識的刪除基於所提供的命名空間和/或ID值。 此外，刪除與給定組織關聯的所有沙箱。 有關詳細資訊，請閱讀上的指南 [隱私請求在Identity Service中處理](privacy.md)。

下表提供了Privacy Service中單個身份刪除的細目：

| 單一身份刪除 | Privacy Service |
| --- | --- |
| 接受的使用案例 | 僅資料隱私請求(GDPR、CCPA)。 |
| 估計延遲 | 天至周 |
| 受影響的服務 | Privacy Service中的單個身份刪除允許您選擇是從Identity Service、Real-Time Customer Profile還是資料湖中刪除資料。 |
| 刪除模式 | 從Identity Service中刪除標識。 |

{style="table-layout:auto"}

## 資料集刪除

以下各節概述了可用於刪除Experience Platform中資料集和相關身份連結的機制。

### 目錄服務中的資料集刪除

您可以使用目錄服務提交資料集刪除請求。 有關如何使用目錄服務刪除資料集的詳細資訊，請閱讀上的指南 [使用目錄服務API刪除對象](../catalog/api/delete-object.md)。 或者，您可以使用平台UI提交資料集刪除請求。 有關詳細資訊，請閱讀 [資料集使用手冊](../catalog/datasets/user-guide.md#delete-a-dataset)。

### 資料衛生中的資料集過期

的 [[!UICONTROL 資料衛生] 工作區](../hygiene/ui/overview.md) 在Adobe Experience PlatformUI中，可以為資料集安排到期時間。 當資料集到達其到期日期時，資料湖、身份服務和即時客戶配置檔案將開始單獨的進程，以從各自的服務中刪除資料集的內容。 有關詳細資訊，請閱讀上的指南 [使用管理資料集過期 [!UICONTROL 資料衛生] 工作區](../hygiene/ui/dataset-expiration.md)。

下表列出了目錄服務中刪除資料集與資料衛生性之間的差異：

| 資料集刪除 | 目錄服務 | 資料衛生 |
| --- | --- | --- |
| 接受的使用案例 | 刪除平台中的完整資料集及其關聯的標識資訊。 | 管理儲存在Experience Platform中的資料。 |
| 估計延遲 | 日 | 日 |
| 受影響的服務 | 通過目錄服務刪除資料集會從Identity Service、Real-Time Customer Profile和資料湖中刪除資料。 | 通過資料衛生刪除資料集會從Identity Service 、 Real-Time Customer Profile和資料湖中刪除資料。 |
| 刪除模式 | 從特定資料集建立的Identity Service中刪除連結的標識。 | 根據過期計畫從特定資料集建立的標識服務中刪除連結的標識。 |

{style="table-layout:auto"}

## 刪除後標識圖的不同狀態

所有標識圖形刪除都會導致刪除兩個或兩個以上標識之間的連結，如刪除請求所指定的那樣。 對於資料集刪除請求，由指定資料集建立的所有標識連結都會被刪除，並且可能或不會從圖形中刪除標識。 對於單個身份刪除請求，為指定身份刪除身份連結，從而從所有身份圖中刪除身份值本身。 沒有與另一個身份的單個連結的身份不會儲存在Identity Service中。

以下是刪除可能對身份圖狀態產生的潛在影響的概要。

| 標識圖狀態 | 說明 |
| --- | --- |
| 部分更新 | 在成功處理刪除請求後，當圖形內至少兩個標識保持連結時，會發生圖形的部分更新。 刪除後，剩餘的標識連結可以保持彼此連接，或者根據刪除的標識可以將它們分割成兩個或多個單獨的圖形。 |
| 完全刪除 | 圖形必須至少具有兩個連結的標識才能存在。 因此，如果刪除請求導致刪除圖形中的所有現有連結，則圖形將被完全刪除。 |
| 無更改 | 如果某個特定刪除請求包含與該圖形的任何成員沒有關聯的標識或資料集，則不會影響圖形。 此外，即使刪除請求確實刪除了資料集或身份資料集組合之間的連結，也不會更新圖表，因為該連結是由另一個未刪除的連結建立的。 這意味著，如果兩個不同的資料集中存在連結，將不會更新圖表，因為只刪除了其中一個資料集。 |

{style="table-layout:auto"}

## 後續步驟

本文檔涵蓋可用於刪除Experience Platform上的標識和資料集的各種機制。 本文檔還概述了身份和資料集刪除如何影響身份圖形。 有關Identity Service的詳細資訊，請閱讀 [Identity Service概述](home.md)。

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
