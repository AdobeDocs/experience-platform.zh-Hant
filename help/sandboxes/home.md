---
keywords: Experience Platform；首頁；熱門主題；沙盒；測試；測試；測試
solution: Experience Platform
title: 沙箱概述
description: 沙箱是單個Experience Platform實例中的虛擬分區，它允許與數字型驗應用程式的開發過程無縫整合。
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# 沙箱概述

Adobe Experience Platform的建設旨在在全球範圍內豐富數字型驗應用。 公司通常並行運行多個數字型驗應用程式，需要滿足這些應用程式的開發、測試和部署需要，同時確保操作合規性。

為了滿足這一需要，Experience Platform提供了沙箱，可將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

本文檔提供了Experience Platform中沙箱的高級概述。

## 瞭解沙箱

沙箱是單個Experience Platform實例中的虛擬分區，它允許與數字型驗應用程式的開發過程無縫整合。 沙盒內執行的所有內容和操作僅限於該沙盒，不影響任何其他沙盒。 Experience Platform上支援兩種沙箱：

* **生產沙盒**:生產沙盒應用於生產環境中的配置檔案。 平台允許您建立多個生產沙箱，以便在保持操作隔離的同時為資料提供適當的功能。 此功能允許您將特定的生產沙箱專用於不同的業務線、品牌、項目或地區。 生產沙箱支援大量生產配置檔案，直至您獲得許可 [!DNL Profile] 承諾（累計計算在所有授權生產沙箱中）。 您有權按授權使用許可的平均配置檔案 [!DNL Profile] （累計計算在所有授權生產沙箱中）。
* **開發沙盒**:開發沙盒是一個沙盒，可專門用於使用非生產配置檔案進行開發和測試。 開發沙箱支援大量非生產配置檔案，其中最多10%是您的許可檔案 [!DNL Profile] 承諾（累計計算在所有授權開發沙箱中）。 您有權：
   * 每個授權非生產配置檔案的平均非生產配置檔案豐富度為75 KB（累計計算在所有授權開發沙箱中）;
   * 每天，每個開發沙箱一個批分段作業；
   * 平均120 [!DNL Profile] API調用，每個 [!DNL Profile]，每年（累計計算在所有授權開發沙箱中）。

一個Experience Platform實例支援多個生產和開發沙箱，每個沙箱都維護其獨立的平台資源庫（包括架構、資料集、配置檔案等）。 此外，生產和開發沙箱都具有重置功能，可從沙箱中刪除所有客戶建立的資源。 開發沙箱不能轉換為生產沙箱。

預設Experience Platform許可證授予您總共五個沙箱，您可以將其分類為生產或開發。 您最多可以許可10個沙箱的附加包，最多可以合計75個沙箱。 這些附加沙箱可用於建立生產和開發沙箱。 有關詳細資訊，請與組織管理員或Adobe銷售代表聯繫。

最後，預設生產沙盒是首次建立組織時建立的第一個生產沙盒。 預設的生產沙盒允許您從平台中接收或使用資料，並接受不包括沙盒名稱或沙盒ID值的請求。

>[!NOTE]
>
>首次建立沙盒時，它不包含任何資料。 由於每個沙盒都維護其自己的隔離資料儲存，因此它們還必須獨立地接收其資料。

總之，沙箱提供了以下好處：

* **應用程式生命週期管理**:建立獨立的虛擬環境以開發和發展數字型驗應用程式。
* **項目和品牌管理**:允許多個項目在同一組織內並行運行，同時提供隔離和訪問控制。 未來版本將支援在多個區域部署。
* **靈活發展生態系統**:以無縫、可擴展且經濟高效的方式提供沙箱，以用於探索、支援和演示。

## 沙箱的訪問控制

預設情況下，組織的所有用戶都可以訪問生產沙箱。 必須由系統管理員、產品管理員或產品配置檔案管理員通過 [Adobe Admin Console](https://adminconsole.adobe.com)。

為了查看、建立、更新或刪除非生產沙箱，還必須向用戶授予沙箱管理權限。

有關管理沙箱角色和權限的詳細資訊，請參見 [訪問控制概述](../access-control/home.md)。

## Experience PlatformUI中的沙箱

在 [Experience Platform用戶介面](https://platform.adobe.com)，用戶可以使用 **沙盒切換器** 控制項。  具有沙盒管理權限的用戶也可以訪問 **[!UICONTROL 沙箱]** 的子菜單。 有關如何在UI中使用沙盒的詳細資訊，請參見 [沙盒使用手冊](ui/overview.md)。

## Experience PlatformAPI中的沙箱

調用Experience PlatformAPI時，必須在標頭下提供沙盒名稱 `x-sandbox-name`。 例如，在調用 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 要查看「生產」沙盒中的所有資料集，沙盒的名稱(「prod」)將作為API請求中的標頭提供：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

如果 `x-sandbox-name` API調用中未包含，系統將改用預設沙盒。 但是，最佳做法是始終將此標頭包含在所有API調用中，即使在使用預設沙箱時也是如此。 因此，用於Experience Platform的API文檔會處理 `x-sandbox-name` 作為必需的標題。

### 沙盒API

沙盒API允許您使用REST風格的API操作來管理沙盒。 查看 [沙盒開發人員指南](api/overview.md) 有關如何使用API的詳細資訊，包括正確格式化的請求和示例響應。

## 後續步驟

通過閱讀本文檔，您已經瞭解了關於Experience Platform中沙箱的基本概念。 有關如何管理沙箱的詳細步驟，請參見 [使用手冊](ui/overview.md) 或 [開發者指南](./api/getting-started.md) 的下界。

沙箱是您開發團隊隔離平台環境的重要工具，您還可以使用Adobe Admin Console管理更精細的訪問控制。 查看 [訪問控制概述](../access-control/home.md) 的子菜單。
