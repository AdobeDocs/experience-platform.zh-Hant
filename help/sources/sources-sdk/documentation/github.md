---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
solution: Experience Platform
title: 使用GitHub網頁介面建立來源檔案頁面
description: 本檔案提供如何使用GitHub網頁介面來撰寫檔案及提交提取請求(PR)的步驟。
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---

# 使用GitHub網頁介面建立來源檔案頁面

本檔案提供如何使用GitHub網頁介面來撰寫檔案及提交提取請求(PR)的步驟。

>[!TIP]
>
>以下是Adobe貢獻指南中的檔案，可進一步支援您的說明檔案程式： <ul><li>[安裝Git與Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[在本機設定供文件使用的 Git 存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[適用於重大變更的 GitHub 貢獻工作流程](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## 設定您的GitHub環境

設定GitHub環境的第一步，就是導覽至 [Adobe Experience Platform GitHub存放庫](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

下一步，選擇 **分支**.

![分叉](../assets/fork.png)

復本完成後，選取 **主版** 並在顯示的下拉式功能表中輸入新分支的名稱。 請確定您為分支提供描述性名稱，因為此名稱將用於包含您的工作，然後選取 **建立分支**.

![建立分支](../assets/create-branch.png)

在您所取用存放庫的GitHub資料夾結構中，導覽至 [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) 然後從清單中為源選擇適當的類別。 例如，如果您要建立新CRM來源的檔案，請選取 **crm**.

>[!TIP]
>
>如果您要建立UI的檔案，請導覽至 [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) 並為源選擇適當的類別。 若要新增影像，請導覽至 [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) 然後將螢幕截圖添加到 `sdk` 檔案夾。

![crm](../assets/crm.png)

將顯示現有CRM源的資料夾。 要為新源添加文檔，請選擇 **新增檔案** 然後選取 **建立新檔案** 從顯示的下拉式功能表。

![create-new-file](../assets/create-new-file.png)

為源檔案命名 `YOURSOURCE.md` 其中YOURSOURCE是Platform中的來源名稱。 例如，如果您的公司是ACME CRM，則您的檔案名稱應為 `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## 編寫來源的檔案頁面

若要開始記錄新來源，請貼上 [來源檔案範本](./template.md) 匯入GitHub網頁編輯器。 您也可以下載範本 [此處](../assets/api-template.zip).

將範本複製到GitHub網頁編輯器介面時，請依照範本上概述的指示操作，並編輯包含您來源相關資訊的值。

![貼上範本](../assets/paste-template.png)

完成後，在分支中提交檔案。

![提交](../assets/commit.png)

## 提交您的檔案以供審核

提交檔案後，您可以開啟提取請求(PR)，將工作分支合併至Adobe檔案存放庫的主分支。 確定已選取您正在使用的分支，然後選取 **比較和提取請求**.

![compare-pr](../assets/compare-pr.png)

確保基分支和比較分支正確。 新增附註至PR，說明您的更新，然後選取 **建立提取請求**. 這會開啟PR，將工作分支合併至Adobe存放庫的主分支。

>[!TIP]
>
>保留 **允許維護者編輯** 核取方塊已選取，以確保Adobe檔案團隊可以編輯PR。

![create-pr](../assets/create-pr.png)

此時會出現通知，提示您簽署Adobe貢獻者授權合約(CLA)。 這是必要步驟。 簽署CLA後，請重新整理PR頁面並提交提取請求。

您可以檢查https://github.com/AdobeDocs/experience-platform.en中的提取請求索引標籤，以確認提取請求已提交。

![confirm-pr](../assets/confirm-pr.png)
