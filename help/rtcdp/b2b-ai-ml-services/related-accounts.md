---
title: Real-Time CDP B2B版本中的相關帳戶
type: Documentation
description: 有關Experience PlatformReal-Time CDP B2B中相關帳戶功能的概觀和詳細資訊。
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 6%

---

# Real-Time CDP B2B版本中的相關帳戶

## 概觀 {#overview}

B2B企業通常將其客戶資訊儲存在多個系統中，每個系統僅包含相同真實世界商業實體的部分或甚至衝突資料。 這帶來了巨大的挑戰，難以準確瞭解客戶，因此會降低B2B行銷和銷售工作的效率和成效。

| ID | 名稱 | 網站 | 產業 | 狀態 | 電話 | 有開啟的商機，金額為> `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | 軟體 | CA | (408)536-6000 |   |
| 2 | Acme | acm.com | 軟體 | CA | 4085366000 | x |
| 3 | Acme Inc |   |   | CA | (408)5366000 |   |
| 4 | Acme諮詢服務 | `http://www.acme.com/consulting` | 技術諮詢 | NY | (212)471-0904 | x |
| 5 | Acme IT |   |   | CA |   |   |

{style="table-layout:auto"}

透過相關帳戶， [!DNL Real-Time CDP B2B] 現在會顯示與您瀏覽的帳戶類似的帳戶清單。

![在Experience Platform UI中顯示「相關」帳戶的畫面。](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

使用此功能在Experience PlatformUI中檢視帳戶設定檔的相關帳戶設定檔，然後將相關帳戶加入您的區段定義中，以擴大您的觸及面或在您的區段中套用更廣的標準。

## 啟用相關的帳戶服務 {#enable}

若要啟用服務，請選取 **[!UICONTROL 設定檔]** 在側邊欄中，後面接著 **[!UICONTROL 設定]**.

![Experience Platform UI醒目提示設定檔和設定。](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

選取旁的切換 [!UICONTROL 啟用相關帳戶] 以啟用服務，然後選取 **[!UICONTROL 儲存]**.

![帳戶設定畫面會反白切換並儲存。](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## 運作方式 {#how-it-works}

每日執行的機器學習作業會使用階層式演演算法，根據三個因素將類似的帳戶設定檔叢集到群組中：

* 父帳戶連結
* 網頁網域
* 帳戶名稱

成功處理工作後，帳戶設定檔群組的每個成員都會標籤為「相關帳戶」清單。 您可以在下列位置檢視清單： **相關帳戶** 「科目設定檔」頁面的頁標，並使用區段定義中的相關科目。

請參閱檔案以瞭解更多關於 [設定檔擴充相關帳戶工作](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## 如何檢視相關帳戶 {#how-to-view}

您可以在Experience PlatformUI中檢視正在瀏覽之帳戶的相關帳戶。

請參閱檔案以瞭解更多關於 [如何在UI中尋找相關帳戶](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## 如何使用相關帳戶 {#how-to-use}

您可以在細分中使用帳戶和相關帳戶。 是否要在區段定義中使用相關帳戶，取決於您的行銷使用案例。 例如，您可以將相關帳戶用於電子郵件行銷或廣告行銷活動，這樣您就可以接受較低的準確性，以換取更廣泛的觸及率。

檢視 [分段範例](/help/rtcdp/segmentation/b2b.md#related-accounts) 會使用相關帳號的使用者。
