---
keywords: Experience Platform；首頁；熱門主題；沙盒故障排除
solution: Experience Platform
title: 砂箱故障排除指南
description: 本文檔提供有關Adobe Experience Platform沙箱的常見問題的答案。
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 9%

---

# 沙箱故障排除指南

本文檔提供有關Adobe Experience Platform沙箱的常見問題的答案。 有關其他平台服務的問題和故障排除，請參閱 [Experience Platform故障排除指南](../landing/troubleshooting.md)。

Sandbox將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。 如需詳細資訊，請參閱[沙箱概觀](home.md)。

## 什麼是沙盒？

沙箱是單個Experience Platform實例中的虛擬分區。 每個沙盒都維護其獨立的平台資源庫（包括架構、資料集、配置檔案等）。 沙盒內執行的所有內容和操作僅限於該沙盒，不影響任何其他沙盒。 如需詳細資訊，請參閱[沙箱概觀](home.md)。

## 有哪些類型的沙箱，它們有何不同？ {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="沙箱類型"
>abstract="沙箱類型會說明這是生產沙箱或是開發沙箱。生產沙箱包括即時資料，而開發沙箱則用於測試和開發。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="在 UI 中建立沙箱"

Experience Platform中有兩種沙盒類型：

* **生產沙盒**:生產沙盒應用於生產環境中的配置檔案。 平台允許您建立多個生產沙箱，以便在保持操作隔離的同時為資料提供適當的功能。 此功能允許您將特定的生產沙箱專用於不同的業務線、品牌、項目或地區。 生產沙箱支援大量生產配置檔案，直至您獲得許可 [!DNL Profile] 承諾（累計計算在所有授權生產沙箱中）。 您有權按授權使用許可的平均配置檔案 [!DNL Profile] （累計計算在所有授權生產沙箱中）。
* **開發沙盒**:開發沙盒是一個沙盒，可專門用於使用非生產配置檔案進行開發和測試。 開發沙箱支援大量非生產配置檔案，其中最多10%是您的許可檔案 [!DNL Profile] 承諾（累計計算在所有授權開發沙箱中）。 您有權：
   * 每個授權非生產配置檔案的平均非生產配置檔案豐富度為75 KB（累計計算在所有授權開發沙箱中）;
   * 每天，每個開發沙箱一個批分段作業；
   * 平均120 [!DNL Profile] API調用，每個 [!DNL Profile]，每年（累計計算在所有授權開發沙箱中）。

如需詳細資訊，請參閱[沙箱概觀](./home.md)。

## 是否可以從多個沙箱訪問資源？

沙箱是單個平台實例的隔離分區，每個沙箱都維護其獨立的資源庫。 無論沙盒類型（生產或非生產）如何，都無法從任何其他沙盒訪問一個沙盒中存在的資源。

## 預設的生產沙箱是什麼？

預設生產沙盒是首次設定組織時建立的第一個生產沙盒。 預設的生產沙盒允許您從平台中接收或使用資料，並接受不包括沙盒名稱或沙盒ID值的請求。 可以重置預設生產沙盒，但不能刪除。

## 我能有多少個生產沙盒？

一個Experience Platform實例支援多個生產和開發沙盒，每個沙盒維護其獨立的平台資源庫（包括架構、資料集和配置檔案）。

預設Experience Platform許可證授予您總共五個沙箱，您可以將其分類為生產或開發。 您最多可以許可10個沙箱的附加包，最多可以合計75個沙箱。

可以重置或刪除生產沙箱，但生產沙箱也由Adobe Analytics用於 [跨設備分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 功能，或者，如果其中承載的標識圖也由Adobe Audience Manager用於 [基於人員的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) 的子菜單。

您可以更新生產沙盒的標題。 但是，無法更名生產沙盒。

>[!NOTE]
>
>沙盒名稱用於API調用中的查找目的，而沙盒標題則用作顯示名稱。

## 我能有多少個沙箱？

Experience Platform目前允許在單個組織內最多活動75個沙箱（生產和開發）。

開發沙箱支援重置和刪除功能。

## 我剛建了一個沙盒。 如何為將要使用此沙盒的用戶設定權限？

Adobe Admin Console通過使用產品配置檔案將用戶連結到沙箱和權限。 建立新沙箱後，導航到 **權限** 頁籤，然後按一下 **沙箱**。 在此處，您可以以與其他權限相同的方式添加或刪除對新沙盒的訪問權限。

如果希望向特定沙盒的用戶添加唯一權限，則可能需要建立具有相應沙盒和權限的新產品配置檔案，並將這些用戶分配給該配置檔案。

查看 [訪問控制使用手冊](../access-control/ui/overview.md) 的子菜單。
