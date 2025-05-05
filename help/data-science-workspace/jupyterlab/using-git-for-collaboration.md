---
keywords: Experience Platform;JupyterLab;筆記本;數據科學工作環境;熱門話題;Git;Github
solution: Experience Platform
title: 使用 Git 在 JupyterLab 中進行協作
type: Tutorial
description: Git是分散式版本控制系統，用於在軟體開發期間追蹤原始程式碼中的變更。 Git 預先安裝在 Data Science 工作環境 JupyterLab 環境 中。
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 共同使用[!DNL JupyterLab][!DNL Git]

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

[!DNL Git] 是一個分散式版本控制系統，用於在軟體開發過程中跟蹤原始碼中的更改。 Git 已預安裝在環境内 [!DNL Data Science Workspace JupyterLab] 。

## 先決條件

>[!NOTE]
>
> 您打算使用的 Git 伺服器需要可以通過互聯網訪問。

[!DNL Data Science Workspace JupyterLab]環境是託管環境，未部署在公司防火牆內，因此您連接到的 Git 伺服器必須可從公共互聯網訪問。這可以是 GitHub[&#128279;](https://github.com/) 上的公共或私有存放庫，也可以是您決定自行主機伺服器的其他[!DNL Git]執行個體。

## [!DNL Data Science Workspace JupyterLab Notebooks]連接到[!DNL Git]環境

從啟動[!DNL Adobe Experience Platform]並瀏覽至[[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab)環境開始。

在 內[!DNL JupyterLab]，選擇檔案&#x200B;**&#x200B;**&#x200B;[!UICONTROL &#x200B;然後將滑鼠懸停在新&#x200B;]&#x200B;**上**。從顯示的下拉清單中，選擇 **[!UICONTROL 終端]**。

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

下一個，在“終端”*中，使用*&#x200B;以下命令導航到工作環境：`cd my-workspace`。

![CD 工作環境](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 要查看可用的 git 命令清單，請在終端中發出命令： `git -help` 。

下一個，使用該命令克隆 `git clone` 要使用的存放庫。 原地複製您的 `https://` 專案使用 URL `ssh://`而不是 .

**範例**：

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 若要執行任何寫入作業（例如`git push`），必須對每個新工作階段執行下列組態命令。 另請注意，任何推送命令都會提示輸入使用者名和密碼。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 後續步驟

克隆完存放庫后，可以像往常一樣在本地計算機上使用 Git 與筆記本上的其他人協作。 如需在 中[!DNL JupyterLab]可執行之工作的詳細資訊，請參閱 。[[!DNL JupyterLab user guide]](./overview.md)
