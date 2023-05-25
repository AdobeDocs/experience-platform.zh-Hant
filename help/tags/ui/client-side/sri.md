---
title: 子資源完整性(SRI)支援
description: 瞭解Adobe Experience Platform如何支援子資源完整性(SRI)。
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 72%

---

# 子資源完整性(SRI)支援

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

本文介紹Adobe Experience Platform如何支援子資源完整性(SRI)。

現代化網站的建置方式，是參照網路上各種位置的影像、內容和指令碼。SRI可讓瀏覽器確認要求的檔案內容未意外修改。

雖然 SRI 與內容安全性原則 (CSP) 的用途互補，但兩者有所不同，後者可確保網站上的檔案一律來自信任的來源。SRI 則更進一步確保這些檔案的內容符合您的預期。

>[!NOTE]
>
>如需 SRI 的詳細資訊，請參閱 [MDN 網頁文件](https://developer.mozilla.org/zh-TW/docs/Web/Security/Subresource_Integrity)。

SRI 驗證程序的摘要如下：

1. 您針對要驗證的資產產生密碼編譯雜湊。
1. 在您的網站上，將雜湊放在載入檔案之 HTML 元素的 `integrity` 屬性中。
1. 瀏覽器偵測到 `integrity` 屬性時，會要求資源並獨立產生自有密碼編譯雜湊版本。
1. 瀏覽器會比較 `integrity` 雜湊與自行產生的雜湊。如果兩者相符，則允許資產。如果兩者不符，資產會遭到封鎖。

## 標記管理系統的限制

作為標籤管理系統(TMS)，Adobe Experience Platform中的標籤提供編譯的JavaScript程式庫組建，讓您透過單一載入到頁面上 `<script>` 元素（內嵌程式碼）。 TMS 提供的動態功能是透過動態替換該指令碼的內容來完成，不需要您變更其他任何內容。

不過，指令碼內容變更時，這些內容的密碼編譯雜湊也會變更。因此，讓 SRI 與 TMS 搭配運作的唯一方法是在您發佈新組建的同時更新內嵌程式碼。對許多人來說，這首先否定了使用 TMS 的主要目的。

下一個最佳標籤安全性選項是實作內容安全性原則。 如需詳細資訊，請參閱以下指南： [CSP和標籤](./content-security-policy.md).

## 將 SRI 整合至組建部署中

如果您仍要將 SRI 用於程式庫組建，則必須使用自行託管。如果您使用 Adobe 代管託管，則必須經過一段時間才能使用 SRI，因為新組建內容與內嵌程式碼的 `integrity` 屬性不符。

內嵌程式碼更新程序自動化的複雜度會因網站結構而異，但一般步驟的摘要如下：

1. 透過 SFTP 傳送或從使用者介面下載封存，擷取生產程式庫組建。
1. 產生主要組建的密碼編譯雜湊。
1. 確定內嵌代碼的 `integrity` 屬性已更新為新雜湊，且參照的組建已更新為相同部署的一部分。

>[!IMPORTANT]
>
>此方法僅涵蓋主要組建，不包含任何可能存在的較小檔案。

## 後續步驟

本檔案說明搭配標籤使用SRI的限制，以及將SRI整合至程式庫組建部署（儘管有這些限制）所需的步驟。 如果您尚未閱讀指南，強烈建議您參閱 [CSP和標籤](./content-security-policy.md) 以取得替代安全性選項。
