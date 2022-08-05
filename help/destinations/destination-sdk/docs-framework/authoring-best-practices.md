---
title: 編寫最佳做法
description: 瞭解在編寫目標文檔頁面時應遵循的規則和提示，以確保它符合Adobe Experience Platform文檔質量標準。
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: 0b9b724c2530e43ce681011d12fc1341148ddbf5
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 編寫最佳做法

## 總覽 {#overview}

本頁介紹了您在 [編寫目標文檔](./documentation-instructions.md) 確保符合Adobe Experience Platform文檔質量標準。

## 一般指導 {#general-guidance}

* 填寫 [模板](./self-service-template.md) 有關目標文檔，請參閱「Adobe貢獻者指南」以獲取有關 [連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en)。 [表](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables)，也請參見Wiki頁。 [支援的markdown語法](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en)。 [書寫指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)。
* 產品文檔中不包括觀察和估計。
* 在Experience Platform文檔中，Adobe編寫器使用 **粗體格式** 請參閱用戶介面控制項，如：
   * 轉到 **[!UICONTROL 連接]** > **[!UICONTROL 目標]**，然後選擇 **[!UICONTROL 目錄]** 頁籤。 查看用戶介面控制項在 [目標教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination)。

## 書寫樣式

>[!IMPORTANT]
>
>閱讀 [編寫Adobe文檔指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 開始創作目標文檔頁面。

* 把句子短一點，快點說清楚。 如果您的句子超過20個單詞或使用多個逗號，請考慮將其分成單獨的句子。 長度超過20字的句子對讀者來說尤其具有挑戰性。
* 別太客氣。 避免使用「please」或「wase do ...」 在技術文檔中。

## 連結 {#linking}

按照提供的文檔模板操作，不要編輯模板中的現有連結。 包括新連結時，請閱讀 [使用文檔中的連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) 的上界。

## 品牌推廣指南 {#branding}

* AEP不是一個經過批准的面向公眾的術語。 請先使用Adobe Experience Platform，然後Experience Platform，然後使用平台。
   * **不使用**:在將資料從AEP導出到YourDestination之前，請確保閱讀並完成這些先決條件。
   * **使用**:在將資料從Adobe Experience Platform導出到YourDestination之前，請確保閱讀並完成這些先決條件。

## 影像和螢幕截圖 {#images-and-screenshots}

* 有關 [如何連結到影像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images)，請參閱《貢獻者指南》。
* 使用螢幕截圖時，請確保您的螢幕截圖捕獲整個平台UI螢幕。
* 在標籤影像以突出顯示頁面上的某個控制項或標籤時，嘗試遵循Experience Platform文檔團隊使用的標籤樣式。 注意在中如何加亮基於輪廓的 [此螢幕截圖](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency)。
* 請使用 `png` 格式化影像。
* 請不要將編號的螢幕截圖用作檔案名。 影像檔案名應是描述性的。
   * **不使用**: `1.png`。 `2.png`。 `3.png`
   * **使用**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 請對添加到文檔的任何影像使用Alt文本，並在Alt文本中使用正確的語法。
   * **不使用**:目標連接詳細資訊
   * **使用**:平台UI的影像，顯示已填入的目標連接詳細資訊。

## 程序 {#process}

* 的 [文檔模板](./self-service-template.md) 根據合作夥伴的反饋不經常更新。 在開始為目標創作文檔之前，請確保已下載 [模板的最新版本](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip)。
* 編寫文檔並從分叉中的分支建立文檔拉取請求(PR) *除了主分支*。 在中創作時，請參閱提交目標以供審閱部分 [GitHub介面](./use-github-interface-to-create-documentation.md#submit-review) 或 [您的本地環境](./work-in-local-environment.md#submit-review)。
