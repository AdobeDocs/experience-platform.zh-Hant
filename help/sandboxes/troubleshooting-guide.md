---
keywords: Experience Platform；首頁；熱門主題；沙箱疑難排解
solution: Experience Platform
title: 沙箱疑難排解指南
description: 本檔案提供有關Adobe Experience Platform中沙箱的常見問題解答。
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 9%

---

# 沙箱疑難排解指南

本檔案提供有關Adobe Experience Platform中沙箱的常見問題解答。 有關其他Experience Platform服務的問題和疑難排解，請參閱[Experience Platform疑難排解指南](../landing/troubleshooting.md)。

沙箱會將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。 如需詳細資訊，請參閱[沙箱概觀](home.md)。

## 何謂沙箱？

沙箱是 Experience Platform 單一執行個體內的虛擬分割。每個沙箱都會維護其獨立的Experience Platform資源資料庫（包括結構描述、資料集、設定檔等）。 在沙箱內採取的所有內容和動作都僅限於該沙箱，不會影響任何其他沙箱。 如需詳細資訊，請參閱[沙箱概觀](home.md)。

## 有哪些類型的沙箱可用，它們有何區別? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="沙箱類型"
>abstract="沙箱類型會說明這是生產沙箱或是開發沙箱。生產沙箱包括即時資料，而開發沙箱則用於測試和開發。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=zh-Hant#create" text="在 UI 中建立沙箱"

Experience Platform提供兩種沙箱型別：

* **生產沙箱**：生產沙箱應該用於您生產環境中的設定檔。 Experience Platform可讓您建立多個生產沙箱，以提供適當的資料功能，同時仍維持作業隔離。 此功能可讓您為不同的業務線、品牌、專案或區域指定特定的生產沙箱。 生產沙箱支援大量生產設定檔，最多可達您授權的[!DNL Profile]承諾（在所有授權的生產沙箱中累積測量）。 您有權使用整個授權的總資料量（在所有授權的生產沙箱中累積測量）。

* **開發沙箱**：開發沙箱是一種沙箱，只能用於開發及測試非生產設定檔。 開發沙箱支援大量非生產設定檔，最多可達您授權的[!DNL Profile]承諾的10% （在所有授權開發沙箱中累積測量）。 您有權享有：
   * 每個開發沙箱每天一個批次分段工作；
   * 每年[!DNL Profile]平均有120個[!DNL Profile] API呼叫（在所有授權開發沙箱中累積測量）。

如需詳細資訊，請參閱[沙箱概觀](./home.md)。

## 我可以從多個沙箱存取資源嗎？

沙箱是單一Experience Platform執行個體的獨立分割區，每個沙箱都維護自己的獨立資源庫。 不論沙箱型別（生產或非生產）為何，您都無法從任何其他沙箱存取存在於一個沙箱中的資源。

## 什麼是預設的生產沙箱？

預設的生產沙箱是第一次布建組織時建立的第一個生產沙箱。 預設的生產沙箱可讓您從Experience Platform擷取或使用資料，以及接受不包含沙箱名稱或沙箱ID值的請求。 預設的生產沙箱可以重設，但不能刪除。

## 我可以擁有多少個生產沙箱？

Experience Platform執行個體支援多個生產及開發沙箱，每個沙箱都會維護自己的Experience Platform資源資料庫（包括結構描述、資料集和設定檔）。

預設Experience Platform授權共授予您5個沙箱，您可將其分類為生產或開發。 您可以額外授權10個沙箱，最多總共75個沙箱。

生產沙箱可重設或刪除，但Adobe Analytics也將其用於[跨裝置分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=zh-Hant)功能的生產沙箱，或其中代管的身分圖表也被Adobe Audience Manager用於[以人為基礎的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=zh-Hant)功能除外。

您可以更新生產沙箱的標題。 不過，無法重新命名生產沙箱。

>[!NOTE]
>
>沙箱名稱用於API呼叫中的查詢目的，而沙箱標題則用作顯示名稱。

## 我可以擁有多少個開發沙箱？

Experience Platform目前最多可在單一組織中啟用75個沙箱（生產及開發）。

開發沙箱支援重設和刪除功能。

## 我剛才建立了沙箱。 我該如何為將使用此沙箱的使用者設定許可權？

Adobe Admin Console透過使用產品設定檔將使用者連結至沙箱和許可權。 建立新沙箱後，請導覽至您要授與存取權的產品設定檔的&#x200B;**許可權**&#x200B;標籤，然後按一下&#x200B;**沙箱**。 在此，您可以按照與其他許可權相同的方式，新增或移除新沙箱的存取權。

如果您想要將唯一許可權新增到特定沙箱的使用者，您可能需要建立新的產品設定檔，並套用適當的沙箱和許可權，然後將這些使用者指派到該設定檔。

請參閱[存取控制使用手冊](../access-control/ui/overview.md)，以取得在Admin Console中管理沙箱和許可權的詳細資訊。
