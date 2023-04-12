---
keywords: Experience Platform；首頁；熱門主題；沙箱；沙箱；測試；測試
solution: Experience Platform
title: 沙箱概述
description: 沙箱是單一Experience Platform例項中的虛擬分區，可與數位體驗應用程式的開發程式順暢整合。
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# 沙箱概述

Adobe Experience Platform的建置宗旨是在全球範圍豐富數位體驗應用程式。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署，同時確保操作合規性。

為了滿足這項需求，Experience Platform提供沙箱，可將單一Platform執行個體分割成個別的虛擬環境，以協助開發及改進數位體驗應用程式。

本檔案提供Experience Platform中沙箱的概觀。

## 了解沙箱

沙箱是單一Experience Platform例項中的虛擬分區，可與數位體驗應用程式的開發程式順暢整合。 在沙箱內採取的所有內容和動作都只會限於該沙箱，不會影響任何其他沙箱。 Experience Platform支援兩種沙箱：

* **生產沙箱**:生產沙箱可用於生產環境中的設定檔。 Platform可讓您建立多個生產沙箱，以便為資料提供適當的功能，同時仍維持運作的隔離。 此功能可讓您將特定的生產沙箱專用於不同的業務、品牌、專案或地區。 生產沙箱支援大量生產設定檔，直到您取得授權為止 [!DNL Profile] 承諾量（累計測量所有授權生產沙箱）。 您有權使用每個授權的授權平均設定檔 [!DNL Profile] （累計測量所有授權生產沙箱）。
* **開發沙箱**:開發沙箱是沙箱，可專門用於開發和測試非生產設定檔。 開發沙箱可支援大量非生產設定檔，高達授權使用的10% [!DNL Profile] 承諾量（累計測量所有授權開發沙箱）。 您有權：
   * 每個授權非生產設定檔的平均非生產設定檔豐富度為75 KB（累計測量於所有授權開發沙箱）;
   * 每日根據開發沙箱執行一次批次分段工作；
   * 平均120 [!DNL Profile] API呼叫次數，根據 [!DNL Profile]，每年（累計計算所有授權開發沙箱的值）。

Experience Platform例項支援多個生產與開發沙箱，每個沙箱都維護各自獨立的Platform資源資料庫（包括結構、資料集、設定檔等）。 此外，生產與開發沙箱都有重設功能，會從沙箱中移除所有客戶建立的資源。 開發沙箱無法轉換為生產沙箱。

預設Experience Platform授權共授予您五個沙箱，您可將其分類為生產或開發。 您可以授權額外的10個沙箱套件，最多總共75個沙箱。 這些額外的沙箱可用來建立生產和開發沙箱。 如需詳細資訊，請連絡您的組織管理員或Adobe銷售代表。

最後，預設的生產沙箱是初次建立組織時建立的第一個生產沙箱。 預設的生產沙箱可讓您從Platform擷取或使用資料，以及接受不包含沙箱名稱或沙箱ID值的要求。

>[!NOTE]
>
>第一次建立沙箱時，不會包含任何資料。 由於每個沙箱會維護各自的獨立資料存放區，因此它們也必須獨立擷取其資料。

總之，沙箱提供下列優點：

* **應用程式生命週期管理**:建立獨立的虛擬環境，以開發和改進數位體驗應用程式。
* **專案和品牌管理**:允許多個項目在同一組織內並行運行，同時提供隔離和訪問控制。 未來版本將提供在多個地區部署的支援。
* **靈活的開發生態系統**:以順暢、可擴充且具成本效益的方式提供沙箱，以利探索、啟用和示範。

## 沙箱的存取控制

依預設，組織的所有使用者都可存取生產沙箱。 系統管理員、產品管理員或產品設定檔管理員必須透過 [Adobe Admin Console](https://adminconsole.adobe.com).

若要檢視、建立、更新或刪除非生產沙箱，使用者也必須獲得沙箱管理權限。

如需管理沙箱角色和權限的詳細資訊，請參閱 [存取控制概觀](../access-control/home.md).

## Experience PlatformUI中的沙箱

在 [Experience Platform使用者介面](https://platform.adobe.com)，使用者可使用 **沙箱切換器** 控制項。  具有沙箱管理權限的使用者也可以存取 **[!UICONTROL 沙箱]** 標籤，以便檢視和管理組織的沙箱。 如需如何在UI中使用沙箱的詳細資訊，請參閱 [沙盒使用手冊](ui/overview.md).

## Experience PlatformAPI中的沙箱

呼叫Experience PlatformAPI時，必須在標題下提供沙箱名稱 `x-sandbox-name`. 例如，當呼叫 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 若要檢視「生產」沙箱內的所有資料集，沙箱的名稱(&quot;prod&quot;)會以API請求的標題形式提供：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

若 `x-sandbox-name` 未包含在API呼叫中，系統會改用預設沙箱。 不過，最佳實務是一律將此標題納入所有API呼叫，即使使用預設沙箱亦然。 因此，Experience Platform的API檔案會加以處理 `x-sandbox-name` 作為必要的標題。

### 沙箱API

沙箱API可讓您使用RESTful API操作來管理沙箱。 請參閱 [沙箱開發人員指南](api/overview.md) 以取得如何使用API的詳細資訊，包括格式正確的請求和範例回應。

## 後續步驟

閱讀本檔案後，您便了解Experience Platform中沙箱的基本概念。 如需如何管理沙箱的詳細步驟，請參閱 [使用手冊](ui/overview.md) (適用於UI或 [開發人員指南](./api/getting-started.md) 的API。

雖然沙箱是隔離Platform環境給開發團隊的寶貴工具，您也可以使用Adobe Admin Console管理更精細的存取控制。 請參閱 [存取控制概觀](../access-control/home.md) 以取得更多資訊。
