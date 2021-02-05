---
keywords: Experience Platform;JupyterLab；筆記型電腦；資料科學工作區；熱門主題；Git;Github
solution: Experience Platform
title: 使用Git在JupyterLab中協作
topic: tutorial
type: Tutorial
description: Git是一種分佈式版本控制系統，用於跟蹤軟體開發過程中原始碼的更改。 Git已預先安裝在Data Science Workspace JupyterLab環境中。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---


# 使用[!DNL Git]在[!DNL JupyterLab]中協作

[!DNL Git] 是一種分佈式版本控制系統，用於跟蹤軟體開發過程中原始碼的更改。Git已預安裝在[!DNL Data Science Workspace JupyterLab]環境中。

## 必要條件

>[!NOTE]
>
> 您要使用的Git伺服器必須可透過網際網路存取。

[!DNL Data Science Workspace JupyterLab]環境是托管環境，未部署在公司防火牆內，因此您所連接的Git伺服器必須可從公共網際網路存取。 這可以是[GitHub](https://github.com/)上的公用或專用儲存庫，也可以是您決定自行托管的[!DNL Git]伺服器的另一實例。

## 將[!DNL Git]連接到[!DNL Data Science Workspace JupyterLab Notebooks]環境

首先，啟動[!DNL Adobe Experience Platform]並導航到[[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab)環境。

在[!DNL JupyterLab]中，選擇&#x200B;**[!UICONTROL 檔案]** ，然後將滑鼠暫留在&#x200B;**[!UICONTROL 新建]**&#x200B;上。 從出現的下拉式清單中，選擇&#x200B;**[!UICONTROL 終端]**。

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

接著，在&#x200B;*Terminal*&#x200B;中，使用下列命令導覽至您的工作區：`cd my-workspace`。

![cd工作區](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 要查看可用的git命令清單，請發出以下命令：`git -help`。

接下來，使用`git clone`命令克隆要使用的儲存庫。 使用`https://` URL而非`ssh://`複製專案。

**範例**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 為了執行任何寫操作（例如`git push`），需要為每個新會話運行以下配置命令。 另請注意，任何推播命令都會提示輸入使用者名稱和密碼。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 後續步驟

克隆完儲存庫後，您可以像在本地電腦上一樣使用Git，以便與其他人在筆記本上協作。 有關在[!DNL JupyterLab]中可以執行的操作的詳細資訊，請參見[[!DNL JupyterLab user guide]](./overview.md)。
