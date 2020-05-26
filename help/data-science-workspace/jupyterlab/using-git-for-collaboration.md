---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: 使用Git在JupyterLab中協作
topic: Tutorial
translation-type: tm+mt
source-git-commit: 0134c21bc35c0cb1bde7f0201a33517a81addae3
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---


# 使用Git在JupyterLab中協作

Git是一種分佈式版本控制系統，用於跟蹤軟體開發過程中原始碼的更改。 Git已預先安裝在Data Science Workspace JupyterLab環境中。

## 必要條件

>[!NOTE]
> 您要使用的Git伺服器必須可透過網際網路存取。

Data Science Workspace JupyterLab環境是代管環境，不會部署在公司防火牆內，因此您所連接的Git伺服器必須可從公共網際網路存取。 這可以是 [GitHub上的公用或專用儲存庫](https://github.com/) ，也可以是您決定自行托管的Git伺服器的另一實例。

## 將Git連接到Data Science Workspace JupyterLab筆記型電腦環境

首先，啟動Adobe Experience Platform並導覽至 [JupyterLabs Notebooks](https://platform.adobe.com/notebooks/jupyterLab) Environment。

在JupyterLab中，選擇「 **[!UICONTROL File]** （檔案）」 ，然後將滑鼠暫留在「 **[!UICONTROL New（新建）」上]**。 從出現的下拉式清單中，選取「 **[!UICONTROL 終端機]**」。

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

克隆完儲存庫後，您可以像在本地電腦上一樣使用Git，以便與其他人在筆記本上協作。 有關在JupyterLab中可以做什麼的詳細資訊，請參閱 [JupyterLab使用手冊](./overview.md)。
