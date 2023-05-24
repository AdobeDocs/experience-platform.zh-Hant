---
keywords: Experience Platform;JupyterLab；筆記本；資料科學工作區；熱門主題；Git;Github
solution: Experience Platform
title: 使用Git在JupyterLab中協作
type: Tutorial
description: Git是一種分佈式版本控制系統，用於跟蹤軟體開發過程中原始碼的變化。 Git預安裝在Data Science Workspace JupyterLab環境中。
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# 協作 [!DNL JupyterLab] 使用 [!DNL Git]

[!DNL Git] 是一種分佈式版本控制系統，用於跟蹤軟體開發過程中原始碼的變化。 Git預裝在 [!DNL Data Science Workspace JupyterLab] 環境。

## 先決條件

>[!NOTE]
>
> 您要使用的Git伺服器需要通過Internet訪問。

的 [!DNL Data Science Workspace JupyterLab] 環境是托管環境，未部署在公司防火牆內，因此您連接到的Git伺服器必須可從公共Internet訪問。 這可以是上的公共或專用儲存庫 [GitHub](https://github.com/) 或另一個實例 [!DNL Git] 您決定自己托管的伺服器。

## 連接 [!DNL Git] 到 [!DNL Data Science Workspace JupyterLab Notebooks] 環境

從啟動開始 [!DNL Adobe Experience Platform] 導航到 [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 環境。

在 [!DNL JupyterLab]選中 **[!UICONTROL 檔案]** 然後懸停 **[!UICONTROL 新建]**。 從顯示的下拉清單中，選擇 **[!UICONTROL 終端]**。

![朱佩特實驗室導航](../images/jupyterlab/tutorials/open-terminal.png)

下一步，在 *終端* 使用以下命令導航到工作區： `cd my-workspace`。

![cd工作區](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 要查看可用git命令的清單，請發出以下命令： `git -help` 在終端內。

接下來，使用 `git clone` 的子菜單。 使用 `https://` URL而不是 `ssh://`。

**範例**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 為了執行任何寫操作(`git push` 例如，需要為每個新會話運行以下配置命令。 另請注意，任何推式命令都會提示輸入用戶名和密碼。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 後續步驟

克隆完儲存庫後，您可以像在本地電腦上通常那樣使用Git與筆記本上的其他電腦協作。 有關您在中可以執行的操作的詳細資訊 [!DNL JupyterLab]，請參見 [[!DNL JupyterLab user guide]](./overview.md)。
