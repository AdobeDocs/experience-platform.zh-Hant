---
keywords: Experience Platform；首頁；熱門主題；沙箱疑難排解
solution: Experience Platform
title: 沙箱疑難排解指南
topic-legacy: troubleshooting guide
description: 本檔案提供Adobe Experience Platform中沙箱常見問題的解答。
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 沙箱疑難排解指南

本檔案提供Adobe Experience Platform中沙箱常見問題的解答。 如需其他Platform服務的相關問題和疑難排解，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

沙箱會將單一Platform例項分割成個別的虛擬環境，以協助開發及改進數位體驗應用程式。 請參閱 [沙箱概述](home.md) 以取得更多資訊。

## 什麼是沙箱？

沙箱是單一Experience Platform例項中的虛擬分區。 每個沙箱會維護各自獨立的Platform資源程式庫（包括結構描述、資料集、設定檔等）。 在沙箱內採取的所有內容和動作都只會限於該沙箱，不會影響任何其他沙箱。 請參閱 [沙箱概述](home.md) 以取得更多資訊。

## 可用的沙箱類型為何，其差異為何？ {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="沙箱類型"
>abstract="沙箱類型會指出這是生產沙箱還是開發沙箱。 生產沙箱包含即時資料，而開發沙箱則用於測試和開發。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="在UI中建立沙箱"

Experience Platform中提供兩種沙箱類型：

* **生產沙箱**:生產沙箱可用於生產環境中的設定檔。 Platform可讓您建立多個生產沙箱，以便為資料提供適當的功能，同時仍維持運作的隔離。 此功能可讓您將特定的生產沙箱專用於不同的業務、品牌、專案或地區。 生產沙箱支援大量生產設定檔，直到您取得授權為止 [!DNL Profile] 承諾量（累計測量所有授權生產沙箱）。 您有權使用每個授權的授權平均設定檔 [!DNL Profile] （累計測量所有授權生產沙箱）。
* **開發沙箱**:開發沙箱是沙箱，可專門用於開發和測試非生產設定檔。 開發沙箱可支援大量非生產設定檔，高達授權使用的10% [!DNL Profile] 承諾量（累計測量所有授權開發沙箱）。 您有權：
   * 每個授權非生產設定檔的平均非生產設定檔豐富度為75 KB（累計測量於所有授權開發沙箱）;
   * 每日根據開發沙箱執行一次批次分段工作；
   * 平均120 [!DNL Profile] API呼叫次數，根據 [!DNL Profile]，每年（累計計算所有授權開發沙箱的值）。

請參閱 [沙箱概述](./home.md) 以取得更多資訊。

## 我可以從多個沙箱存取資源嗎？

沙箱是單一Platform例項的獨立分區，每個沙箱都會維護各自的獨立資源庫。 存在於一個沙箱中的資源無法從任何其他沙箱存取，無論沙箱類型（生產或非生產）為何。

## 預設的生產沙箱為何？

預設的生產沙箱是首次布建IMS組織時建立的第一個生產沙箱。 預設的生產沙箱可讓您從Platform擷取或使用資料，以及接受不包含沙箱名稱或沙箱ID值的要求。 可重設預設生產沙箱，但不可刪除。

## 我可以有多少個生產沙箱？

Experience Platform例項支援多個生產與開發沙箱，每個沙箱都維護其獨立的Platform資源資料庫（包括結構、資料集和設定檔）。

預設Experience Platform授權共授予您五個沙箱，您可將其分類為生產或開發。 您可以授權額外的10個沙箱套件，最多總共75個沙箱。

生產沙箱可重設或刪除，但生產沙箱也由Adobe Analytics用於 [跨裝置分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 功能，或內部托管的身分圖表也正由Adobe Audience Manager用於 [以人物為基礎的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) 功能。

您可以更新生產沙箱的標題。 但無法重新命名生產沙箱。

>[!NOTE]
>
>沙箱名稱會用於API呼叫中的查詢用途，而沙箱標題會作為顯示名稱。

## 我可以有多少個開發沙箱？

Experience Platform目前最多可在單一IMS組織內啟用總共75個沙箱（生產與開發）。

開發沙箱支援重設和刪除功能。

## 我剛建立了一個沙箱。 如何為將使用此沙箱的使用者設定權限？

Adobe Admin Console會透過使用產品設定檔，將使用者連結至沙箱和權限。 建立新沙箱後，導覽至 **權限** 標籤，然後按一下 **沙箱**. 從這裡，您可以以與其他權限相同的方式新增或移除對新沙箱的存取。

如果您想要將唯一權限新增至特定沙箱的使用者，您可能需要建立新的產品設定檔並套用適當的沙箱和權限，並將這些使用者指派給該設定檔。

請參閱 [存取控制使用手冊](../access-control/ui/overview.md) 以取得管理沙箱和Admin Console權限的詳細資訊。
