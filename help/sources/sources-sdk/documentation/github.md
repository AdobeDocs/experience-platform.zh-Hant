---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
solution: Experience Platform
title: 使用GitHub網頁介面建立來原始檔頁面
description: 本檔案提供如何使用GitHub網頁介面來撰寫檔案及提交提取請求(PR)的步驟。
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 使用GitHub網頁介面建立來原始檔頁面

本檔案提供如何使用GitHub網頁介面來撰寫檔案及提交提取請求(PR)的步驟。

>[!TIP]
>
>Adobe的投稿指南中的下列檔案可用來進一步支援您的說明檔案程式： <ul><li>[安裝Git與Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[在本機設定檔案的Git存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[重大變更的GitHub貢獻工作流程](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## 設定您的GitHub環境

設定GitHub環境的第一個步驟是導覽至[Adobe Experience Platform GitHub存放庫](https://github.com/AdobeDocs/experience-platform.en)。

![平台存放庫](../assets/platform-repo.png)

接著，選取&#x200B;**分支**。

![分支](../assets/fork.png)

復本完成後，請選取&#x200B;**master**，然後在出現的下拉式功能表中輸入新分支的名稱。 請確定您為分支提供描述性名稱，因為這將用來包含您的工作，然後選取&#x200B;**建立分支**。

![create-branch](../assets/create-branch.png)

在您取用的存放庫的GitHub資料夾結構中，導覽至[`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create)，然後從清單中為您的來源選取適當的類別。 例如，如果您正在建立新CRM來源的檔案，請選取&#x200B;**crm**。

>[!TIP]
>
>如果您正在建立UI的檔案，請導覽至[`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create)並為您的來源選取適當的類別。 若要新增影像，請導覽至[`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create)，然後將熒幕擷取畫面新增至`sdk`資料夾。

![crm](../assets/crm.png)

現有CRM來源的資料夾隨即顯示。 若要新增新來源的檔案，請選取[新增檔案] ****，然後從出現的下拉式功能表中選取[建立新檔案] **。**

![create-new-file](../assets/create-new-file.png)

將您的來源檔案命名為`YOURSOURCE.md`，其中YOURSOURCE是您在Experience Platform中的來源名稱。 例如，如果您的公司是ACME CRM，則您的檔案名稱應該是`acme-crm.md`。

![git-interface](../assets/git-interface.png)

## 為您的來源編寫檔案頁面

若要開始記錄您的新來源，請將[來原始檔範本](./template.md)的內容貼到GitHub網頁編輯器中。 您也可以在[這裡](../assets/api-template.zip)下載範本。

將範本複製到GitHub網頁編輯器介面後，請依照範本上概述的指示操作，並編輯包含來源相關資訊的值。

![貼上範本](../assets/paste-template.png)

完成後，在您的分支中提交檔案。

![認可](../assets/commit.png)

## 提交您的檔案以供檢閱

在提交檔案後，您可以開啟提取請求(PR)，將您的工作分支合併至Adobe檔案存放庫的主分支。 確定已選取您正在處理的分支，然後選取&#x200B;**比較與提取請求**。

![比較 — pr](../assets/compare-pr.png)

請確認基礎分支和比較分支正確無誤。 將說明您更新的附註新增至PR，然後選取&#x200B;**建立提取請求**。 這會開啟PR，將您工作的工作分支合併至Adobe存放庫的主分支。

>[!TIP]
>
>保留&#x200B;**允許維護者進行編輯**&#x200B;核取方塊為已選取狀態，以確保Adobe檔案團隊可對PR進行編輯。

![create-pr](../assets/create-pr.png)

此時，系統會顯示通知，提示您簽署Adobe貢獻者授權合約(CLA)。 此為必要步驟。 簽署CLA後，請重新整理PR頁面並提交提取請求。

您可以檢查https://github.com/AdobeDocs/experience-platform.en中的「提取請求」標籤，確認提取請求已提交。

![confirm-pr](../assets/confirm-pr.png)
