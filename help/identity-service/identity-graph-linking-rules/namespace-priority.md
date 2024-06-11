---
title: 名稱空間優先順序
description: 瞭解Identity Service中的名稱空間優先順序。
badge: Beta
source-git-commit: 85da193f422a1708999fb59b7ea095f4447d6bdf
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 1%

---

# 名稱空間優先順序

>[!AVAILABILITY]
>
>此功能尚未推出；身分圖表連結規則的Beta版計畫預計於7月在開發沙箱上開始。 如需參與率條件的詳細資訊，請聯絡您的Adobe客戶團隊。

每個客戶實作都是獨一無二，並根據特定組織的目標量身打造，因此，特定名稱空間的重要性因客戶而異。 現實世界的範例包括：

* 一方面，您可能會將電子郵件名稱空間視為代表個人實體，因此每個人均是唯一的。 另一方面，其他客戶可能會將電子郵件名稱空間視為不可靠的識別碼，因此他們可能會允許單一CRM ID與電子郵件名稱空間有多個身分識別相關聯。
* 您可以使用「登入ID」名稱空間收集線上行為。 此登入ID可能與CRM ID維持1:1關係，而CRM ID會儲存CRM系統的屬性，且可能被視為最重要的名稱空間。 在此案例中，您會判定CRM ID名稱空間能更精確地代表人員，而登入ID名稱空間則是第二重要的名稱空間。

您必須在Identity Service中進行反映名稱空間重要性的設定，因為這會影響設定檔的形成和分段方式。

## 決定您的優先順序

名稱空間優先順序的判斷會依據下列因素：

### 身分圖表結構

如果貴組織的圖表為階層式，則名稱空間優先順序應反映這一點，以便在圖表摺疊時移除正確的連結。

>[!TIP]
>
>* 「圖表摺疊」是指多個不同的設定檔不慎合併到單一身分圖表中的情況。
>
>* 分層圖表是指具有多重連結層級的身分圖表。 檢視下方影像以取得含有三個圖層的圖形範例。

![圖表層圖表](../images/namespace-priority/graph-layers.png)

### 名稱空間的語意意義

身分代表真實世界的物件。 身分圖中有三個物件代表。 按照重要性順序，它們是：

* 人員（跨裝置、電子郵件、電話號碼）
* 硬體裝置
* 網頁瀏覽器(Cookie)

與硬體裝置（例如IDFA、GAID）相比，人員名稱空間相對不可變，而硬體裝置相對於網頁瀏覽器則相對不可變。 基本上，您（人員）永遠是單一實體，擁有多部硬體裝置（手機、筆記型電腦、平板電腦等），並使用多部瀏覽器(Google Chrome、Safari、FireFox等)

處理此主題的另一種方法是使用基數。 對於指定的人員實體，將會建立多少身分？ 在大多數情況下，人員會有一個CRM ID、數個硬體裝置識別碼（IDFA/GAID重設不應該經常發生），以及更多的Cookie （可以想見，個人可以在多個裝置上瀏覽、使用無痕模式，或在任何指定時間重設Cookie）。 一般而言， **較低基數表示名稱空間具有較高值**.

<!-- ## Step 2: Validate your namespace priority settings

Once you have an idea of how you will prioritize your namespaces, you can use the Graph Simulation tool to test out various graph collapse scenarios and ensure that your priority configurations are returning the expected graph results. For more information, read the guide on using the [Graph Simulation tool](./graph-simulation.md). -->

## 設定名稱空間優先順序

可以使用設定名稱空間優先順序 [!UICONTROL 身分設定]. 在 [!UICONTROL 身分設定] 介面，您可以拖放名稱空間以判斷其相對重要性。

>[!IMPORTANT]
>
>裝置/Cookie名稱空間優先順序無法高於人員名稱空間。 此限制可確保不會發生錯誤設定。

## 名稱空間優先順序使用方式

目前，名稱空間優先順序會影響即時客戶個人檔案的系統行為。 下圖說明了此概念。 如需詳細資訊，請閱讀以下指南： [Adobe Experience Platform和應用程式架構圖](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![名稱空間優先順序應用程式範圍的圖表](../images/namespace-priority/application-scope.png)

### Identity Service：身分最佳化演演算法

對於相對複雜的圖表結構，名稱空間優先順序在確保在圖表摺疊情況發生時移除正確連結方面扮演重要角色。 如需詳細資訊，請參閱 [[!DNL Identity Optimization Algorithm] 概述](../identity-graph-linking-rules/identity-optimization-algorithm.md).

### 即時客戶個人檔案：體驗事件的主要身分確定

* 對於體驗事件，當您為特定沙箱設定身分設定後，主要身分將由後續的最高名稱空間優先順序決定。
   * 這是因為體驗事件的本質是動態的。 身分對應可能包含三個或更多身分，而名稱空間優先順序可確保最重要的名稱空間與體驗事件相關聯。
* 因此，進行以下設定 **將不再由即時客戶個人檔案使用**：
   * WebSDK中資料元素型別的「主要」核取方塊。
   * 任何在XDM體驗事件類別結構描述上標示為主要身分的欄位。
   * Adobe Analytics來源聯結器（ECID或AAID）中的預設主要身分設定。
* 另一方面， **名稱空間優先順序不會決定設定檔記錄的主要身分**.
   * 對於設定檔記錄，您可以使用Experience PlatformUI中的結構描述工作區來定義您的身分欄位，包括主要身分。 閱讀指南： [在UI中定義身分欄位](../../xdm/ui/fields/identity.md) 以取得詳細資訊。

>[!NOTE]
>
>* 名稱空間優先順序為 **名稱空間的屬性**. 這是指派給名稱空間的數值，可指出其相對重要性。
>
>* 主要身分是儲存設定檔片段所針對的身分。 設定檔片段是資料記錄，用於儲存有關特定使用者的資訊：屬性（通常透過CRM記錄擷取）或事件（通常從體驗事件或線上資料擷取）。

### 範例圖表情境

本節提供優先順序設定如何影響資料的範例。

假設為給定沙箱建立了以下設定：

| 命名空間 | 名稱空間的實際應用程式 | 優先等級 |
| --- | --- | --- |
| CRMID | 使用者 | 1 |
| IDFA | Apple硬體裝置(iPhone、IPad等) | 2 |
| GAID | Google硬體裝置(Google Pixel、Pixelbook等) | 3 |
| ECID | 網頁瀏覽器(Firefox、Safari、Google Chrome等) | 4 |
| AAID | 網頁瀏覽器 | 5 |

{style="table-layout:auto"}

基於上述設定，使用者動作和主要身分的判定將依下列方式解析：

| 使用者動作（體驗事件） | 驗證狀態 | 資料來源 | 身分對應 | 主要身分（設定檔片段的主要索引鍵） |
| --- | --- | --- | --- | --- |
| 檢視信用卡優惠方案頁面 | 未驗證（匿名） | Web SDK | {ECID} | ECID |
| 檢視說明頁面 | 未驗證 | Mobile SDK | {ECID， IDFA} | IDFA |
| 檢視支票帳戶餘額 | 已驗證 | Web SDK | {CRM ID， ECID} | CRM ID |
| 註冊房屋貸款 | 已驗證 | Analytics來源聯結器 | {CRM ID， ECID， AAID} | CRM ID |
| 將$1,000從支票轉帳至節省金額 | 已驗證 | Mobile SDK | {CRM ID， GAID， ECID} | CRM ID |

{style="table-layout:auto"}

### 細分服務：區段會籍中繼資料儲存

![區塊會籍儲存空間圖](../images/namespace-priority/segment-membership-storage.png)

對於指定的合併設定檔，區段會籍會根據具有最高優先順序名稱空間的身分來儲存。

例如，假設有兩個設定檔：

* 第一個設定檔代表John。
* 第二個設定檔代表Jane。

如果John和Jane共用裝置，則ECID （網頁瀏覽器）會從一個人傳輸給另一個人。 不過，這不會影響針對John和Jane所儲存的區段會籍資訊。

如果區段資格標準完全以根據ECID儲存的匿名事件為基礎，則Jane將符合該區段的資格

## 對其他Experience Platform服務的影響 {#implications}

本節概述名稱空間優先順序如何影響其他Experience Platform服務。

### 進階資料生命週期管理

對於指定的身分，資料衛生記錄刪除請求會以下列方式運作：

* 即時客戶設定檔：刪除任何將指定身分識別為主要身分的設定檔片段。 **設定檔上的主要身分現在將根據名稱空間優先順序來決定。**
* 資料湖：刪除任何以指定身分作為主要身分的記錄。

如需詳細資訊，請閱讀 [進階生命週期管理概觀](../../hygiene/home.md).

### 資料湖

資料湖的資料擷取將繼續遵循上設定的主要身分設定 [Web SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) 和結構描述。

資料湖不會根據名稱空間優先順序來判斷主要身分。 例如，Adobe Customer Journey Analytics將繼續使用身分對應中的值，即使在啟用名稱空間優先順序後（例如，將資料集新增到新連線），因為Customer Journey Analytics會消耗其來自資料湖的資料。

### Experience Data Model (XDM)結構

任何不是XDM體驗事件的結構描述，例如XDM個別設定檔，將會繼續遵循任何 [您標籤為身分的欄位](../../xdm/ui/fields/identity.md).

如需XDM結構的詳細資訊，請參閱 [結構概觀](../../xdm/home.md).

### Intelligent services

選取資料時，您需要指定名稱空間，用於決定計算分數的事件，以及儲存計算分數的事件。 建議您選取代表個人的名稱空間。

* 如果您使用WebSDk收集Web行為資料，建議您在身分對應中選擇CRM ID名稱空間。
* 如果您使用Analytics來源聯結器收集網頁行為資料，則應該選取身分描述項(CRM ID)。

此設定導致僅使用已驗證的事件計算分數。

如需有關的詳細資訊，請閱讀以下檔案： [Attribution AI](../../intelligent-services/attribution-ai/overview.md) 和 [Customer AI](../../intelligent-services/customer-ai/overview.md).

### Privacy Service

[Privacy Service刪除請求](../privacy.md) 會以下列方式為指定身分執行功能：

* 即時客戶設定檔：刪除任何將指定身分值作為主要身分的設定檔片段。 **設定檔上的主要身分現在將根據名稱空間優先順序來決定。**
* 資料湖：刪除具有指定身分作為主要或次要身分的任何記錄。

如需詳細資訊，請閱讀 [Privacy Service概述](../../privacy-service/home.md).