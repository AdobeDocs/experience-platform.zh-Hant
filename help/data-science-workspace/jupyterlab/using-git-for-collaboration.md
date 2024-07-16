---
keywords: Experience Platform；JupyterLab；筆記本；資料科學Workspace；熱門主題；Git；Github
solution: Experience Platform
title: 使用Git在JupyterLab中共同作業
type: Tutorial
description: Git是分散式版本控制系統，用於在軟體開發期間追蹤原始程式碼中的變更。 Git已預先安裝在資料科學Workspace JupyterLab環境中。
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---

# 使用[!DNL Git]在[!DNL JupyterLab]中共同作業

[!DNL Git]是分散式版本控制系統，用於在軟體開發期間追蹤原始程式碼中的變更。 已在[!DNL Data Science Workspace JupyterLab]環境中預先安裝Git。

## 先決條件

>[!NOTE]
>
> 您打算使用的Git伺服器必須可透過網際網路存取。

[!DNL Data Science Workspace JupyterLab]環境是託管環境，未部署在您的公司防火牆內，因此您連線的Git伺服器必須可從公用網際網路存取。 這可以是[GitHub](https://github.com/)上的公開或私人存放庫，或您已決定自行託管的[!DNL Git]伺服器的另一個執行個體。

## 將[!DNL Git]連線至[!DNL Data Science Workspace JupyterLab Notebooks]環境

從啟動[!DNL Adobe Experience Platform]並瀏覽至[[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab)環境開始。

在[!DNL JupyterLab]內，選取&#x200B;**[!UICONTROL 檔案]**，然後將滑鼠游標停留在&#x200B;**[!UICONTROL 新增]**&#x200B;上。 從出現的下拉式清單中，選取&#x200B;**[!UICONTROL 終端機]**。

![JupyterLab導覽](../images/jupyterlab/tutorials/open-terminal.png)

接下來，在&#x200B;*終端機*&#x200B;內，使用以下命令導覽至您的工作區： `cd my-workspace`。

![cd工作區](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 若要檢視可用的Git命令清單，請在您的終端機中發出命令： `git -help`。

接下來，使用`git clone`命令複製您要使用的存放庫。 使用`https://` URL而非`ssh://`複製專案。

**範例**：

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![複製](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 若要執行任何寫入作業（例如`git push`），必須對每個新工作階段執行下列組態命令。 另請注意，任何推送命令都會提示您輸入使用者名稱和密碼。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 後續步驟

完成複製存放庫後，您可以像在本機電腦上一樣使用Git，與他人在Notebooks上共同作業。 如需在[!DNL JupyterLab]內可以執行之作業的詳細資訊，請參閱[[!DNL JupyterLab user guide]](./overview.md)。
