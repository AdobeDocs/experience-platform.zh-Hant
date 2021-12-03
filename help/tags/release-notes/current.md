---
title: 版本注意事項
description: Adobe Experience Platform中標籤的最新發行說明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 2056f7f6e7372fa1dee2e975a75e7ba3b8dfe518
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 6%

---

# 發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../term-updates.md)。

## 2021 年 11 月 15 日

**在標籤中接受ES6程式碼**  — 包含ES6程式碼的擴充功能和自訂程式碼現在可用於標籤中。 在擴充功能目錄中，每個包含ES6程式碼擴充功能的卡片內會顯示ES6+標籤。 IE10和IE11不支援ES6代碼。 在「標籤」程式庫中使用ES6程式碼之前，請適度延遲。

**使用字元作為JavaScript壓縮程式** - Terser替換了Uglifier。 自此版本開始，所有標籤程式庫皆由Terser縮制。

## 2021 年 10 月 21 日

**在事件轉送中將資料傳送至已驗證的端點**  — 使用機密，您可以將資料發送到需要下列身份驗證協定的端點：

* **[!UICONTROL 代號]**:代表驗證Token值的單一字元字串。
* **[!UICONTROL 簡單HTTP]**:包含用戶名和密碼的兩個字串屬性。
* **[!UICONTROL OAuth2]**:包含數個要支援的屬性 [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) 規格。

如需詳細資訊，請參閱 [在資料收集UI中管理機密](../ui/event-forwarding/secrets.md) 或 [在Reactor API中管理機密](../api/guides/secrets.md).

## 2021 年 7 月 19 日

**對「管理屬性」權利的調整**  — 「管理屬性」權限遇到以下問題：用戶有權建立新屬性，但在建立後無法查看（如社區線程中所述） [此處](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176))。 修正現在會如文章所述，與正在執行的權限一起上線。

>[!NOTE]
>
>如果您將新的「編輯屬性」指派給使用者群組，UI將不會更新以啟用屬性設定畫面中的欄位。 此問題的修正將在即將發行的版本中實施。

## 2021 年 5 月 17 日

**更妥善處理未儲存的變更**  — 過去，每當您離開設定檢視（擴充功能、資料元素和規則元件）導覽至其他位置時，系統就會提示您是否要捨棄變更。 但判斷這個邏輯並不好，因此大多數時候，即使沒有變更，您還是會被提示儲存變更。  已經修好了。  從現在開始，您應該只有在實際進行變更時才會看到該提示。

## 2021 年 5 月 10 日

**簡化發佈作業**  — 不再需要建置至測試環境。  如果您有適當的權限，只要您已成功建立，且上游沒有其他程式庫，就可以完全略過「已提交」狀態，並直接從開發發佈。

## 2021年4月22日

**Adobe Experience Platform中的資料收集**  — 將資料傳送至Adobe不僅是要將標籤部署至您的網站，或配置至您的應用程式。  使用Experience PlatformSDK和邊緣網路時，需要存取其他平台功能。  這過去需要登入幾種不同的工具，但現在它們在一起。

Platform中的資料收集包含6項功能，而您新簡化的導覽只會包含您公司和使用者帳戶有權存取的項目。  部分功能名稱也已更新，以符合Experience Platform的命名模式。

* 用戶端（先前以用戶端存取）
* 資料流（先前以Edge Configurations存取）
* 伺服器（先前以伺服器端存取）
* 應用程式設定
* 方案
* 身分

隨著Experience Platform和資料收集功能的不斷演化，期待更多更新。

## 2021年2月18日

* 將資料收集UI更新為react-spectrum v3
* 將擴充卡更新為最新的頻譜模式
* 增加應用程式中名稱欄位的大小

## 2021 年 1 月 13 日

**正式發行：事件轉送** 將事件層級資料傳送至Adobe Experience Platform邊緣網路，然後使用事件轉送，利用Adobe的伺服器（而非用戶端）低延遲轉換、擴充及傳送該資料至非Adobe端點。

請參閱 [事件轉送概觀](../ui/event-forwarding/overview.md) 和 [快速入門手冊](../ui/event-forwarding/getting-started.md) 以取得更多資訊。
