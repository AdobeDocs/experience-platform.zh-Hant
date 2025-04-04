---
keywords: Experience Platform；首頁；熱門主題；沙箱；沙箱；測試；測試
solution: Experience Platform
title: 沙箱總覽
description: 沙箱是單一Experience Platform執行個體中的虛擬分割區，可與數位體驗應用程式的開發流程無縫整合。
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 2%

---

# 沙箱概觀

Adobe Experience Platform 是為了在全球規模上使數位體驗應用程式更加豐富而打造。公司通常會同時執行多個數位體驗應用程式，而且需要滿足這些應用程式的開發、測試和部署需求，同時確保營運合規性。

為了滿足此需求，Experience Platform提供可將單一Experience Platform執行個體分割成個別虛擬環境的沙箱，以利開發及改進數位體驗應用程式。

本檔案提供Experience Platform中沙箱的整體概觀。

## 了解沙箱

沙箱是單一Experience Platform執行個體中的虛擬分割區，可與數位體驗應用程式的開發流程無縫整合。 在沙箱內採取的所有內容和動作都僅限於該沙箱，不會影響任何其他沙箱。 Experience Platform支援兩種沙箱：

* **生產沙箱**：生產沙箱應該用於您生產環境中的設定檔。 Experience Platform可讓您建立多個生產沙箱，以提供適當的資料功能，同時仍維持作業隔離。 此功能可讓您為不同的業務線、品牌、專案或區域指定特定的生產沙箱。 生產沙箱支援大量生產設定檔，最多可達您授權的[!DNL Profile]承諾（在所有授權的生產沙箱中累積測量）。 您有權使用整個授權的總資料量（在所有授權的生產沙箱中累積測量）。

* **開發沙箱**：開發沙箱是一種沙箱，只能用於開發及測試非生產設定檔。 開發沙箱支援大量非生產設定檔，最多可達您授權的[!DNL Profile]承諾的10% （在所有授權開發沙箱中累積測量）。 您有權享有：
   * 每個開發沙箱每天一個批次分段工作；
   * 每年[!DNL Profile]平均有120個[!DNL Profile] API呼叫（在所有授權開發沙箱中累積測量）。

Experience Platform執行個體支援多個生產及開發沙箱，每個沙箱都會維護自己的Experience Platform資源資料庫（包括結構描述、資料集、設定檔等）。 此外，生產沙箱和開發沙箱都有重設功能，可從沙箱中移除所有客戶建立的資源。 無法將開發沙箱轉換為生產沙箱。

預設Experience Platform授權共授予您5個沙箱，您可將其分類為生產或開發。 您可以額外授權10個沙箱，最多總共75個沙箱。 這些額外的沙箱可用來建立生產及開發沙箱。 如需詳細資訊，請聯絡您的組織管理員或Adobe銷售代表。

最後，預設的生產沙箱是首次建立組織時建立的第一個生產沙箱。 預設的生產沙箱可讓您從Experience Platform擷取或使用資料，以及接受不包含沙箱名稱或沙箱ID值的請求。

>[!NOTE]
>
>沙箱首次建立時，不含任何資料。 由於每個沙箱會維護自己的隔離資料存放區，因此他們也必須獨立擷取其資料。

總而言之，沙箱提供下列優點：

* **應用程式生命週期管理**：建立個別的虛擬環境，以開發及改進數位體驗應用程式。
* **專案與品牌管理**：允許多個專案在同一個組織內平行執行，同時提供隔離與存取控制。
* **彈性開發生態系統**：以順暢、可擴充且符合成本效益的方式，提供沙箱，以用於探索、啟用和示範用途。

## 沙箱的存取控制

依預設，組織的所有使用者都可存取生產沙箱。 非生產沙箱的存取權必須由系統管理員、產品管理員或產品設定檔管理員透過[Adobe Admin Console](https://adminconsole.adobe.com)授予。

若要檢視、建立、更新或刪除非生產沙箱，使用者也必須被授與沙箱管理許可權。

如需管理沙箱角色和許可權的詳細資訊，請參閱[存取控制總覽](../access-control/home.md)。

## Experience Platform UI中的沙箱

在[Experience Platform使用者介面](https://platform.adobe.com)中，使用者可以使用熒幕左上方的&#x200B;**沙箱切換器**&#x200B;控制項，在他們有權存取的沙箱之間切換。  具有沙箱管理許可權的使用者還可以存取左側導覽中的&#x200B;**[!UICONTROL 沙箱]**&#x200B;索引標籤，他們可以在其中檢視和管理其組織的沙箱。 如需如何在UI中使用沙箱的詳細資訊，請參閱[沙箱使用手冊](ui/overview.md)。

## Experience Platform API中的沙箱

呼叫Experience Platform API時，必須在標頭`x-sandbox-name`下方提供沙箱名稱。 例如，呼叫[[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/)以檢視生產沙箱內的所有資料集時，沙箱名稱(「prod」)會作為API請求中的標頭提供：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

如果`x-sandbox-name`未包含在API呼叫中，系統將改用預設沙箱。 不過，最佳做法是在所有API呼叫中一律包含此標題，即使使用預設沙箱亦然。 因此，Experience Platform的API檔案會將`x-sandbox-name`視為必要的標頭。

### Sandbox API

沙箱API可讓您使用RESTful API操作來管理沙箱。 請參閱[沙箱開發人員指南](api/overview.md)，以取得有關如何使用API的詳細資訊，包括正確格式化的請求和範例回應。

## 後續步驟

閱讀本檔案後，您將瞭解Experience Platform中沙箱的基本概念。 如需有關如何管理沙箱的詳細步驟，請參閱UI的[使用者指南](ui/overview.md)或API的[開發人員指南](./api/getting-started.md)。

雖然沙箱是隔離開發團隊Experience Platform環境的寶貴工具，但您也可以使用Adobe Admin Console管理更精細的存取控制。 如需詳細資訊，請參閱[存取控制總覽](../access-control/home.md)。
