---
keywords: Experience Platform;JupyterLab；筆記型電腦；Data Science Workspace；熱門主題；Git;Github
solution: Experience Platform
title: 使用Git在JupyterLab中協作
type: Tutorial
description: Git是分散式版本控制系統，可追蹤軟體開發期間原始碼的變更。 Data Science Workspace JupyterLab環境中已預先安裝Git。
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# 協作 [!DNL JupyterLab] 使用 [!DNL Git]

[!DNL Git] 是一種分佈式版本控制系統，用於跟蹤軟體開發過程中原始碼的變化。 Git已預先安裝於 [!DNL Data Science Workspace JupyterLab] 環境。

## 先決條件

>[!NOTE]
>
> 您要使用的Git伺服器必須可透過網際網路存取。

此 [!DNL Data Science Workspace JupyterLab] 環境是托管環境，且未部署在公司防火牆內，因此您所連線的Git伺服器必須可從公用網際網路存取。 這可以是上的公用或私人存放庫 [GitHub](https://github.com/) 或 [!DNL Git] 伺服器。

## Connect [!DNL Git] 到 [!DNL Data Science Workspace JupyterLab Notebooks] 環境

從啟動開始 [!DNL Adobe Experience Platform] 並導覽至 [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 環境。

內 [!DNL JupyterLab]，選取 **[!UICONTROL 檔案]** 然後暫留 **[!UICONTROL 新增]**. 從顯示的下拉式清單中，選取 **[!UICONTROL 終端]**.

![JupyterLab導覽](../images/jupyterlab/tutorials/open-terminal.png)

接下來，在內 *終端* 使用下列命令導覽至您的工作區： `cd my-workspace`.

![cd workspace](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 若要查看可用git命令清單，請發出命令： `git -help` 在您的終端機內。

接下來，使用複製 `git clone` 命令。 使用 `https://` URL而非 `ssh://`.

**範例**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 為了執行任何寫操作(`git push` 例如，需要為每個新會話運行以下配置命令。 另請注意，任何推送命令都會提示輸入使用者名稱和密碼。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 後續步驟

複製完存放庫後，您就可以像在本機電腦上一般使用Git，與筆記型電腦上的其他人共同作業。 如需詳細資訊，請參閱 [!DNL JupyterLab]，請參閱 [[!DNL JupyterLab user guide]](./overview.md).
