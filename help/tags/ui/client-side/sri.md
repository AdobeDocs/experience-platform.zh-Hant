---
title: 子資源完整性(SRI)支援
description: 瞭解子資源完整性(SRI)在Adobe Experience Platform如何得到支援。
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 72%

---

# 子資源完整性(SRI)支援

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

本檔案介紹了在Adobe Experience Platform如何支援子資源完整性。

現代化網站的建置方式，是參照網路上各種位置的影像、內容和指令碼。SRI允許瀏覽器驗證請求檔案的內容是否未意外修改。

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

作為標籤管理系統(TMS),Adobe Experience Platform的標籤提供了一個編譯的JavaScript庫構建，您只需使用一個標籤就可將其載入到頁面上 `<script>` 元素（嵌入代碼）。 TMS 提供的動態功能是透過動態替換該指令碼的內容來完成，不需要您變更其他任何內容。

不過，指令碼內容變更時，這些內容的密碼編譯雜湊也會變更。因此，讓 SRI 與 TMS 搭配運作的唯一方法是在您發佈新組建的同時更新內嵌程式碼。對許多人來說，這首先否定了使用 TMS 的主要目的。

標籤的下一個最佳安全選項是實施內容安全策略。 有關詳細資訊，請參閱上的指南 [CSP和標籤](./content-security-policy.md)。

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

本文檔介紹了將SRI與標籤一起使用的限制，以及將SRI與庫構建部署整合所需的步驟，儘管這些限制存在。 如果您尚未閱讀，強烈建議您閱讀 [CSP和標籤](./content-security-policy.md) 換個安全選項。
