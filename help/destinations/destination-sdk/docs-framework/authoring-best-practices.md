---
title: 製作最佳實務
description: 瞭解您在編寫目的地檔案頁面時應遵循的規則和秘訣，以確保其符合Adobe Experience Platform檔案品質標準。
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 製作最佳實務

## 概觀 {#overview}

本頁面說明您應在下列情況下遵循的規則： [編寫您的目的地檔案](./documentation-instructions.md) 頁面，確保其符合Adobe Experience Platform檔案品質標準。

## 一般指引 {#general-guidance}

* 填寫時 [範本](./self-service-template.md) 如需目的地檔案，請參閱Adobe貢獻者指南，以瞭解有關 [連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html)， [表格](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables)，則 [支援的Markdown語法](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html)， [撰寫指引](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html)、等等。
* 請勿在產品檔案中包含觀察和估計。
* 在Experience Platform檔案中，Adobe作者會使用 **粗體格式** 若要參照使用者介面控制項，如下所示：
   * 前往 **[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。 檢視如何在中記錄使用者介面控制項的範例 [目的地教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination).

## 寫入樣式

>[!IMPORTANT]
>
>讀取 [Adobe檔案撰寫指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) 開始編寫目的地檔案頁面之前。

* 讓您的句子保持簡短，並快速切入正題。 如果您的句子超過20個字或使用了多個逗號，請考慮將其分成個別的句子。 長度超過20個字的句子對讀者來說特別具有挑戰性。
* 不要過於客氣。 避免在技術檔案中使用「請」或「請……」。

## 連結 {#linking}

請依照提供的檔案範本操作，不要編輯範本中現有的連結。 包含新連結時，請閱讀 [在檔案中使用連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html) 投稿人指南中的。

## 品牌指南 {#branding}

* AEP不是經核准的公開術語。 請先使用Adobe Experience Platform，再使用Experience Platform，最後再使用平台。
   * **不要使用**：將資料從AEP匯出至目的地之前，請務必閱讀並完成這些必要條件。
   * **使用**：將資料從Adobe Experience Platform匯出至目的地之前，請務必閱讀並完成這些必備條件。

## 影像和熒幕擷取畫面 {#images-and-screenshots}

* 有關的資訊 [如何連結至影像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images)，請參閱貢獻者指南。
* 使用熒幕擷取畫面時，請確保您的熒幕擷取畫面能擷取整個Platform UI畫面。
* 標示影像以反白顯示頁面上的特定控制項或標籤時，請嘗試遵循Experience Platform檔案團隊使用的標示樣式。 請注意，在中如何強調設定檔型 [此熒幕擷圖](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* 請使用 `png` 格式化影像。
* 請勿使用編號熒幕擷取畫面作為檔案名稱。 影像檔案名稱應為描述性。
   * **不要使用**： `1.png`， `2.png`， `3.png`
   * **使用**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 請針對您新增至檔案的任何影像使用替代文字，並在替代文字中使用適當的文法。
   * **不要使用**：目的地連線詳細資料
   * **使用**：Platform UI影像，顯示已填入的目的地連線詳細資料。

## 程序 {#process}

* 此 [檔案範本](./self-service-template.md) 不常根據合作夥伴意見更新。 開始編寫目的地的檔案之前，請確定您已下載 [最新版本的範本](../assets/docs-framework/yourdestination-template.zip).
* 撰寫檔案，並從復本中的分支建立檔案提取請求(PR) *除了主要分支*. 在中製作時，請參閱提交目的地以供檢閱區段 [GitHub介面](./use-github-interface-to-create-documentation.md#submit-review) 或 [您的本機環境](./work-in-local-environment.md#submit-review).
