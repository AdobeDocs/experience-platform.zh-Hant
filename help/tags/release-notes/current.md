---
title: 標籤發行說明
description: Adobe Experience Platform 標記的最新發行說明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: a15b5525d3a2fa034715803c83dc22a94915347e
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 7%

---

# 在Adobe Experience Platform發佈標籤說明

>[!NOTE]
>
>Adobe Experience Platform Launch正被重新打上Experience Platform資料收集技術的標籤。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../term-updates.md)。

## 2021 年 11 月 15 日

**接受標籤中的ES6代碼**  — 現在可以在標籤中使用包含ES6代碼的擴展和自定義代碼。 在擴展目錄中，您將在每個擴展的卡內看到一個包含ES6代碼的ES6+標籤。 IE10和IE11不支援ES6代碼。 在「標籤」庫中使用ES6代碼之前，請執行適當的延遲。

**將Terser用作JavaScript壓縮程式** - Uglifier被Terser替換。 從此版本開始，所有標籤庫都由Terser進行微縮。

## 2021 年 10 月 21 日

**在事件轉發時向經過驗證的端點發送資料**  — 使用機密，您可以將資料發送到需要以下身份驗證協定的端點：

* **[!UICONTROL 令牌]**:表示驗證令牌值的單個字串。
* **[!UICONTROL 簡單HTTP]**:包含用戶名和密碼的兩個字串屬性。
* **[!UICONTROL OAuth2]**:包含多個屬性以支援 [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) 規範

有關詳細資訊，請參閱上的指南 [管理資料收集UI中的機密](../ui/event-forwarding/secrets.md) 或 [管理Reactor API中的機密](../api/guides/secrets.md)。

## 2021 年 7 月 19 日

**對「管理屬性」權限的調整**  — 「管理屬性」權限遇到一個問題，即用戶有權建立新屬性，但在建立後無法看到它（如社區線程中所述） [這裡](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176))。 修復程式現在與正在強制執行的權限一起運行，如文章所述。

>[!NOTE]
>
>如果將新的「編輯屬性」權限分配給用戶組，則UI將不會更新以啟用屬性配置螢幕中的欄位。 此問題的解決方案將在即將發佈的版本中實施。

## 2021 年 5 月 17 日

**更好地處理未保存的更改**  — 過去，無論何時從設定視圖（擴展、資料元素和規則元件）中導航，您都會收到是否放棄更改的提示。 但是，確定這一點的邏輯並不好，因此大多數時候，您都會收到提示，要保存更改，即使沒有更改。  那個已經修好了。  從現在開始，您只應在實際進行更改時看到該提示。

## 2021 年 5 月 10 日

**簡化發佈**  — 不再需要構建到過渡環境。  如果您具有相應的權限，則只要生成成功且上游沒有其他庫，就可以完全跳過「已提交」狀態，直接從「開發」中發佈。

## 2021年4月22日

**Adobe Experience Platform資料收集**  — 向Adobe發送資料不僅僅是將標籤部署到您的站點或配置到您的應用程式。  使用Experience PlatformSDK和邊緣網路需要訪問其他平台功能。  這過去需要登錄到幾個不同的工具，但現在它們在一起。

平台中的資料收集包含六項功能，而您新近簡化的導航將只包含您的公司和用戶帳戶有權訪問的項目。  某些功能名稱也已更新，以匹配Experience Platform的命名模式。

* 客戶端（以前以客戶端形式訪問）
* 資料流（以前以邊緣配置形式訪問）
* 伺服器（以前以伺服器端形式訪問）
* 應用程式配置
* 結構描述
* 身分

隨著Experience Platform和資料收集的不斷發展，期待更多更新。

## 2021年2月18日

* 已將資料收集UI更新為反應頻譜v3
* 最新頻譜模式的擴展卡更新
* 增加整個應用中名稱欄位的大小

## 2021 年 1 月 13 日

**一般可用性：事件轉發** 將事件級資料發送到Adobe Experience Platform邊緣網路，然後使用事件轉發以低延遲將資料轉換、豐富和發送到非Adobe端點，使用Adobe的伺服器而不是客戶端。

查看 [事件轉發概述](../ui/event-forwarding/overview.md) 和 [入門指南](../ui/event-forwarding/getting-started.md) 的子菜單。
