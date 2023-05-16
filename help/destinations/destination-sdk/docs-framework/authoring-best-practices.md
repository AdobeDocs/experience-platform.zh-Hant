---
title: 製作最佳實務
description: 了解編寫目的地檔案頁面時，您應遵循哪些規則和秘訣，以確保符合Adobe Experience Platform檔案品質標準。
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 製作最佳實務

## 總覽 {#overview}

本頁面說明您應遵循的規則，當 [編寫您的目的地檔案](./documentation-instructions.md) 頁面，以確保符合Adobe Experience Platform檔案品質標準。

## 一般指導 {#general-guidance}

* 填入 [範本](./self-service-template.md) 如需目的地檔案，請參閱Adobe貢獻者指南，取得相關資訊 [連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [表](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), [支援的markdown語法](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [撰寫指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)、等。
* 請勿在產品檔案中納入觀察與估計。
* 在Experience Platform檔案中，Adobe撰寫器使用 **粗體格式** 若要參考使用者介面控制項，如下所示：
   * 前往 **[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。 檢視以下範例： [目的地教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## 書寫樣式

>[!IMPORTANT]
>
>閱讀 [Adobe檔案撰寫指引](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 開始編寫目標檔案頁面之前。

* 把句子短一點，快點說清楚。 如果您的句子長度超過20個字詞，或使用多個逗號，請考慮將其分成不同的句子。 長度超過20個字的句子對讀者來說尤其具有挑戰性。
* 別太禮貌。 請避免使用「請」或「請……」 中。

## 連結 {#linking}

請依照提供的檔案範本操作，不要編輯範本中的現有連結。 包括新連結時，請閱讀 [在檔案中使用連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) （在貢獻者指南中）。

## 品牌推廣准則 {#branding}

* AEP不是經核准的公開辭彙。 請先使用Adobe Experience Platform，然後Experience Platform，再使用Platform。
   * **請勿使用**:請務必閱讀並完成這些必要條件，才能將資料從AEP匯出至YourDestination。
   * **使用**:請務必閱讀並完成這些必要條件，才能將資料從Adobe Experience Platform匯出至YourDestination。

## 影像和螢幕擷取畫面 {#images-and-screenshots}

* 如需 [如何連結至影像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images)，請參閱貢獻者指南。
* 使用螢幕擷取畫面時，請確定您的螢幕擷取畫面會擷取整個Platform UI畫面。
* 在標籤影像以突出顯示頁面上的特定控制項或標籤時，請嘗試遵循Experience Platform文檔小組使用的標籤樣式。 請注意，以下中會如何強調顯示「設定檔」： [此螢幕截圖](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* 請使用 `png` 格式化影像。
* 請勿將編號的螢幕截圖用作檔案名。 影像檔案名稱應是描述性的。
   * **請勿使用**: `1.png`, `2.png`, `3.png`
   * **使用**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 請對您新增至檔案的任何影像使用alt文字，並在alt文字中使用正確的文法。
   * **請勿使用**:目標連接詳細資訊
   * **使用**:Platform UI的影像，顯示已填入的目的地連線詳細資料。

## 程序 {#process}

* 此 [檔案範本](./self-service-template.md) 會根據合作夥伴的意見而不常更新。 開始編寫目的地的檔案之前，請確定您已下載 [最新版範本](../assets/docs-framework/yourdestination-template.zip).
* 撰寫檔案，並從分支的分支建立檔案提取請求(PR) *除主分支外*. 在 [GitHub介面](./use-github-interface-to-create-documentation.md#submit-review) 或 [您的本地環境](./work-in-local-environment.md#submit-review).
