---
title: Didomi Source概觀
description: 瞭解如何使用使用者介面將Didomi連線至Adobe Experience Platform。
last-substantial-update: 2025-07-29T00:00:00Z
badge: Beta
exl-id: c59bcfb8-e831-4a13-8b0e-4c6d538f1059
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# [!DNL Didomi]

>[!AVAILABILITY]
>
>[!DNL Didomi]來源是測試版。 閱讀來源概觀中的[條款與條件](../../home.md#terms-and-conditions)，以取得有關使用測試版標籤之來源的詳細資訊。

[!DNL Didomi]是同意和偏好設定管理平台，可協助組織跨網站、應用程式和內部工具收集、管理和強制執行使用者有關個人資料的選擇。

Adobe Experience Platform支援透過來源聯結器系統，從各種外部系統擷取資料，包括雲端儲存空間、資料庫和[!DNL Didomi]等應用程式。 使用來源驗證外部系統、管理流入Experience Platform的資料，並確保以一致的結構化方式擷取您的客戶資料。

使用[!DNL Didomi]來源將來自[!DNL Didomi]同意和偏好設定管理平台的即時使用者同意和偏好設定資料串流到Experience Platform。 透過[!DNL Didomi]來源，您可以在Experience Platform中集中並處理同意資料，藉此保持您的客戶設定檔和下游工作流程相容且為最新狀態。

![Didomi資料處理架構。](../../images/tutorials/create/didomi/flux.jpeg)

## 先決條件

完成下列先決條件步驟，成功將您的[!DNL Didomi]帳戶連線至Experience Platform。

### IP位址允許清單

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南以瞭解詳細資訊。

### 在Experience Platform上設定許可權

您必須同時為帳戶啟用&#x200B;**[!UICONTROL View Sources]**&#x200B;和&#x200B;**[!UICONTROL Manage Sources]**&#x200B;許可權，才能將您的[!DNL Didomi]帳戶連線至Experience Platform。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/ui/overview.md)。

### 收集Adobe API認證

若要安全地將[!DNL Didomi]連線到Experience Platform，您必須使用您的Adobe API認證進行驗證。 這些憑證對於設定webhook和設定資料擷取至關重要。

閱讀[Experience Platform API快速入門](../../../landing/api-authentication.md)的指南，瞭解如何成功呼叫Experience Platform API。

### 建立Experience Platform結構描述

>[!TIP]
>
>如果您已經有現有的XDM結構描述，可以略過此步驟。

**Experience Data Model (XDM)結構描述**&#x200B;定義了您將從[!DNL Didomi]傳送到Experience Platform的資料結構（例如使用者ID、同意目的）。

若要建立結構描述，請在Experience Platform UI的左側導覽中選取[!UICONTROL Schemas]，然後選取&#x200B;**[!UICONTROL Create schema]**。 接著，選取&#x200B;**[!UICONTROL Standard]**&#x200B;作為結構描述型別，然後選取&#x200B;**[!UICONTROL Manual]**&#x200B;以手動建立欄位。 選取結構描述的基底類別，並提供結構描述的名稱。

建立後，新增任何必填欄位以更新結構。 確保至少一個欄位是[!UICONTROL Identity]欄位，以通知Experience Platform您的主要身分值。 最後，請確定您已啟用[!UICONTROL Profile]切換功能，以便成功儲存您的資料。

![create-schema](../../images/tutorials/create/didomi/create-schema.png)

如需詳細資訊，請閱讀[在UI](../../../xdm/tutorials/create-schema-ui.md)中建立結構描述的指南。

### 建立資料集

>[!TIP]
>
>如果您已經有現有的資料集，可以略過此步驟。

Experience Platform中的&#x200B;**資料集**&#x200B;是用來根據您定義的結構描述儲存傳入的資料。

若要建立資料集，請在Experience Platform UI的左側導覽中選取「[!UICONTROL Datasets]」，然後選取「**[!UICONTROL Create dataset]**」。 接著，選取&#x200B;**[!UICONTROL Create dataset from schema]**，然後選取要與新資料集建立關聯的結構描述。

![建立資料集](../../images/tutorials/create/didomi/create-dataset.png)

## 在[!DNL Didomi]主控台上設定HTTP Webhook

[!DNL Webhooks]可讓您訂閱使用者與其同意偏好設定互動時，在[!DNL Didomi]平台上觸發的事件。 當發生相關事件時 — 例如，當使用者給予或撤銷同意時 — [!DNL Didomi]會傳送包含JSON裝載的即時HTTP POST要求至您設定的[!DNL webhook]端點。

![didomi-console](../../images/tutorials/create/didomi/didomi-console.png)

為確保與Experience Platform相容，您的webhook必須符合以下要求。

| 欄位 | 說明 | 範例 |
| --- | --- | --- | 
| 用戶端密碼 | 與您的Adobe API認證相關聯的秘密金鑰。 | `d8f3b2e1-4c9a-4a7f-9b2e-8f1c3d2a1b6e` |
| API金鑰 | 用於驗證Adobe服務請求的公開API金鑰。 |  |
| 授權型別 | 應用程式從授權伺服器取得存取權杖的方法。 將此值設定為`client_credentials`。 | `client_credentials` |
| 範圍 | 授權範圍會定義應用程式向API提供者請求的特定許可權或存取層級。 | `openid,AdobeID,read_organizations,additional_info.projectedProductContext,session` |
| 驗證標頭 | Adobe權杖請求所需的其他標頭。 | `{"Content-type": "application/x-www-form-urlencoded"}` |
| 權杖URL | 您的Adobe權杖端點。 | `https://ims-na1.adobelogin.com/ims/token/v3` |
| 端點 URL | 最終的Adobe聯結器URL （于設定結束時提供）。 | `https://dcs.adobedc.net/collection/your-adobe-endpoint-id` |

{style="table-layout:auto"}

接下來，為您的[!DNL webhook]設定下列選項。

| 欄位 | 說明 | 價值 |
| ---| --- | --- | 
| 請求標頭 | [!DNL webhook]的自訂標頭。 確定您包含`x-adobe-flow-id`。 您可以在建立[資料流後](../../tutorials/ui/create/consent-and-preferences/didomi.md#retrieve-the-streaming-endpoint-url)擷取此值。 | `{"Content-Type": "application/json", "Cache-Control": "no-cache", "x-adobe-flow-id": "{DATAFLOW_ID}"}` |
| Flatten | 必須檢查此屬性，因為它確保[!DNL webhook]資料會以一般物件傳送。 | 啟用 |
| 事件型別 | 選取應觸發[!DNL Didomi]的`event.*`事件特定群組（`user.*`或[!DNL webhook]）。 使用`event.*`追蹤同意或偏好設定變更，並使用`user.*`追蹤使用者設定檔更新。 需要選取此專案，才能確保只將相容的事件傳送至Adobe。 Adobe僅支援每個資料流一個結構描述，因此選取這兩種事件型別可能會導致擷取錯誤。 | 支援的事件型別清單包括： <ul><li>`Event.created`</li><li>`Event.updated`</li><li>`Event.deleted`</li><li>`User.created`</li><li>`User.updated`</li><li>`User.deleted`</li></ul> |

### 下載範例裝載檔案 {#download-the-sample-payload-file}

根據您選取的事件群組，直接從&#x200B;**主控台下載適當的**&#x200B;範例裝載檔案[!DNL Didomi]。 此檔案代表資料結構，並將在Adobe的結構描述和對應步驟中使用。

| **事件群組** | **要下載的範例檔案** | **篩選選項** |
| --- | ---| --- |
| `event.*` | 下載`event.created`的範例 | 僅篩選`event.*`個事件 |
| `user.*` | 下載`user.created`的範例 | 僅篩選`user.*`個事件 |

## 將您的[!DNL Didomi]帳戶連線至Experience Platform

閱讀[連線 [!DNL Didomi] 至Experience Platform](../../tutorials/ui/create/consent-and-preferences/didomi.md)的指南，瞭解如何建立來源連線，以及將[!DNL Didomi]的同意和偏好設定資料擷取至Experience Platform。
