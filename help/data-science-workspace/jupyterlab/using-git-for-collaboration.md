---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: 使用Git在JupyterLab中協作
topic: Tutorial
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# 使用 [!DNL JupyterLab] [!DNL Git]

[!DNL Git] 是一種分佈式版本控制系統，用於跟蹤軟體開發過程中原始碼的更改。 Git已預先安裝在環境 [!DNL Data Science Workspace JupyterLab] 中。

## 必要條件

>[!NOTE]
> 您要使用的Git伺服器必須可透過網際網路存取。

此環 [!DNL Data Science Workspace JupyterLab] 境是代管環境，並未部署在公司防火牆內，因此您所連接的Git伺服器必須可從公共網際網路存取。 這可以是 [GitHub上的公用或專用儲存庫](https://github.com/) ，也可以是您決定自 [!DNL Git] 己托管的另一個伺服器實例。

## 連接 [!DNL Git] 到環 [!DNL Data Science Workspace JupyterLab Notebooks] 境

首先，啟動 [!DNL Adobe Experience Platform] 並導覽至環 [!DNL JupyterLabs Notebooks](https://platform.adobe.com/notebooks/jupyterLab) 境。

在中 [!DNL JupyterLab]，選擇「 **[!UICONTROL File]** （檔案）」 ，然後將滑鼠暫留在「 **[!UICONTROL New（新建）]**」上。 從出現的下拉式清單中，選取「 **[!UICONTROL 終端機]**」。

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

接著，在「終 *端機* 」內，使用下列命令導覽至您的工作區： `cd my-workspace`.

![cd工作區](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
> 要查看可用的git命令清單，請發出以下命令： `git -help` 在您的終端機中。

接著，使用命令克隆要使用的儲存 `git clone` 庫。 使用 `https://` URL而非URL複製專案 `ssh://`。

**範例**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
> 為了執行任何寫操作(`git push` 例如)，需要為每個新會話運行以下配置命令。 另請注意，任何推播命令都會提示輸入使用者名稱和密碼。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 後續步驟

克隆完儲存庫後，您可以像在本地電腦上一樣使用Git，以便與其他人在筆記本上協作。 有關您可在其中執行的操作的詳細 [!DNL JupyterLab]資訊，請參見 [!DNL JupyterLab user guide](./overview.md)。
