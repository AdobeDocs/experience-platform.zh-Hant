---
keywords: Experience Platform;home；熱門主題；沙盒；沙盒；測試；測試
solution: Experience Platform
title: 沙盒概觀
topic-legacy: overview
description: 沙盒是單一Experience Platform例項中的虛擬分區，可讓您與數位體驗應用程式的開發流程順暢整合。
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# 沙盒總覽

Adobe Experience Platform的設計宗旨是在全球範圍豐富數位體驗應用程式。 公司通常並行執行多種數位體驗應用程式，並需要滿足這些應用程式的開發、測試和部署需求，同時確保運作符合規範。

為瞭解決此需求，Experience Platform提供沙盒，可將單一平台執行個體分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

本檔案提供Experience Platform沙盒的高階概觀。

## 瞭解沙盒

沙盒是單一Experience Platform例項中的虛擬分區，可讓您與數位體驗應用程式的開發流程順暢整合。 一個Experience Platform例項支援一個生產沙盒和多個非生產沙盒，每個沙盒會維護其獨立的平台資源庫（包括架構、資料集、設定檔等）。  在沙盒中執行的所有內容和動作都僅限於該沙盒，不會影響任何其他沙盒。

非生產沙盒可讓您測試功能、執行實驗並建立自訂組態，而不會影響生產沙盒。 此外，非生產沙盒具有重設功能，可從沙盒移除所有客戶建立的資源。 非生產沙盒無法轉換為生產沙盒。 預設的Experience Platform授權會授與您五個沙盒（一個製作與四個非製作）。 您可新增10個非生產沙盒，最多可新增75個沙盒。 如需詳細資訊，請連絡您的IMS組織管理員或Adobe銷售代表。

>[!NOTE]
>
>第一次建立沙盒時，沙盒不包含任何資料。 由於每個沙盒都會維護其獨立的資料儲存，因此它們也必須個別收錄資料。

總之，沙盒提供下列優點：

* **應用程式生命週期管理**:建立個別的虛擬環境，以開發和發展數位體驗應用程式。
* **專案與品牌管理**:允許多個專案在相同的IMS組織內並行執行，同時提供隔離和存取控制。未來版本將支援在多個地區部署。
* **有彈性的開發生態系統**:以順暢、可擴充且具成本效益的方式提供沙盒，以利探索、啟用和展示。

## 沙盒的存取控制

依預設，組織的所有使用者都可存取生產沙盒。 系統管理員、產品管理員或產品設定檔管理員必須透過[Adobe Admin Console](https://adminconsole.adobe.com)授與非生產沙盒的存取權。

為了檢視、建立、更新或刪除非生產沙盒，使用者也必須獲得沙盒管理權限。

有關管理沙盒角色和權限的詳細資訊，請參閱[訪問控制概述](../access-control/home.md)。

## Experience PlatformUI中的沙盒

在[Experience Platform使用者介面](https://platform.adobe.com)中，使用者可使用畫面左上角的&#x200B;**沙盒切換器**&#x200B;控制項，在他們可存取的沙盒之間切換。  具有「沙盒管理」權限的使用者也可存取左側導覽中的&#x200B;**[!UICONTROL Sandboxes]**&#x200B;標籤，以檢視和管理組織的沙盒。 如需如何在UI中使用沙盒的詳細資訊，請參閱[沙盒使用指南](ui/overview.md)。

## Experience PlatformAPI中的沙盒

呼叫Experience PlatformAPI時，必須在標題`x-sandbox-name`下提供沙盒名稱。 例如，當呼叫[[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)以檢視「生產」沙盒內的所有資料集時，沙盒的名稱(&quot;prod&quot;)會以標題的形式提供在API請求中：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

如果API呼叫中未包含`x-sandbox-name`，系統將改用預設沙盒。 不過，最佳實務是一律將此標題納入所有API呼叫中，即使使用預設沙盒亦然。 因此，Experience Platform的API檔案會將`x-sandbox-name`視為必要的標題。

### 沙盒API

「沙盒API」可讓您使用REST風格的API作業來管理沙盒。 請參閱[沙盒開發人員指南](api/getting-started.md)以取得如何使用API的詳細資訊，包括正確格式化的請求和範例回應。

## 後續步驟

閱讀本檔案，您便瞭解了Experience Platform中沙盒的基本概念。 如需如何管理沙盒的詳細步驟，請參閱UI的[使用指南](ui/overview.md)或API的[開發人員指南](./api/getting-started.md)。

沙盒雖然是您開發團隊隔離平台環境的重要工具，但您也可以使用Adobe Admin Console管理更精細的存取控制。 有關詳細資訊，請參閱[訪問控制概述](../access-control/home.md)。
