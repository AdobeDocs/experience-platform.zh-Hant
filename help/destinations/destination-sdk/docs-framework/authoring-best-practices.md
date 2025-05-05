---
title: 製作最佳實務
description: 瞭解您在編寫目的地檔案頁面時應遵循的規則和秘訣，以確保其符合Adobe Experience Platform檔案品質標準。
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 製作最佳實務

## 概觀 {#overview}

此頁面說明在[編寫目的地檔案](./documentation-instructions.md)頁面時應遵循的規則，以確保其符合Adobe Experience Platform檔案品質標準。

## 一般指引 {#general-guidance}

* 填寫目的地檔案的[範本](./self-service-template.md)時，請參閱Adobe貢獻者指南，以取得有關[連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=zh-Hant)、[表格](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=zh-Hant#tables)、[支援的Markdown語法](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=zh-Hant)、[撰寫指引](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=zh-Hant)等專案的資訊。
* 請勿在產品檔案中包含觀察和估計。
* 在Experience Platform檔案中，Adobe作者會使用&#x200B;**粗體格式**&#x200B;來參照使用者介面控制項，如下所示：
   * 移至&#x200B;**[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。 檢視在[目的地教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=zh-Hant#select-destination)中如何記錄使用者介面控制項的範例。

## 寫作風格

>[!IMPORTANT]
>
>開始編寫目的地檔案頁面之前，請先閱讀[Adobe檔案的撰寫指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=zh-Hant)。

* 讓您的句子保持簡短，並快速切入正題。 如果您的句子超過20個字或使用了多個逗號，請考慮將其分成個別的句子。 長度超過20個字的句子對讀者來說特別具有挑戰性。
* 不要過於客氣。 避免在技術檔案中使用「請」或「請……」。

## 連結 {#linking}

請依照提供的檔案範本操作，不要編輯範本中現有的連結。 加入新連結時，請閱讀[在貢獻者指南的檔案](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=zh-Hant)中使用連結。

## 品牌指南 {#branding}

* AEP不是經核准的公開術語。 請先使用Adobe Experience Platform，然後再使用Experience Platform和Experience Platform。
   * **請勿使用**：在您將資料從AEP匯出到YourDestination之前，請確定您已閱讀並完成這些必要條件。
   * **使用**：在您將資料從Adobe Experience Platform匯出到YourDestination之前，請確定您已閱讀並完成這些必要條件。

## 影像和熒幕擷取畫面 {#images-and-screenshots}

* 如需[如何連結至影像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=zh-Hant#images)的相關資訊，請參閱貢獻者指南。
* 使用熒幕擷取畫面時，請確定您的熒幕擷取畫面足以擷取整個Experience Platform UI畫面。
* 標示影像以反白顯示頁面上的特定控制項或標籤時，請嘗試遵循Experience Platform檔案團隊使用的標示樣式。 請注意[此熒幕擷圖](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency)中以設定檔為基礎如何反白顯示。
* 請使用`png`格式影像。
* 請勿使用編號熒幕擷取畫面作為檔案名稱。 影像檔案名稱應為描述性。
   * **不使用**： `1.png`，`2.png`，`3.png`
   * **使用**： `yourdestination-authentication-details.png`，`yourdestination-destination-details.png`
* 請針對您新增至檔案的任何影像使用替代文字，並在替代文字中使用適當的文法。
   * **不使用**：目的地連線詳細資料
   * **使用**： Experience Platform UI的影像，顯示已填入的目的地連線詳細資料。

## 程式 {#process}

* [檔案範本](./self-service-template.md)很少根據合作夥伴意見更新。 在您開始編寫目的地的檔案之前，請確定您已下載範本的[最新版本](../assets/docs-framework/yourdestination-template.zip)。
* 撰寫檔案並從分支&#x200B;*中除主要分支*&#x200B;以外的分支建立檔案提取請求(PR)。 在[GitHub介面](./use-github-interface-to-create-documentation.md#submit-review)或[您的本機環境](./work-in-local-environment.md#submit-review)中進行製作時，請參閱送出目的地以供檢閱區段。
