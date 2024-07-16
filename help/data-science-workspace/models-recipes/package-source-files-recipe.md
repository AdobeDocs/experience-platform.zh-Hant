---
keywords: Experience Platform；封裝來源檔案；資料科學Workspace；熱門主題；Docker；Docker影像
solution: Experience Platform
title: 將Source檔案封裝到配方中
type: Tutorial
description: 本教學課程說明如何將提供的零售銷售範例來源檔案封裝到封存檔案中，您可以在UI中或使用API遵循配方匯入工作流程，藉此在Adobe Experience Platform Data Science Workspace中建立配方。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# 將來源檔案封裝到配方中

本教學課程提供如何將提供的零售銷售範例來源檔案封裝到封存檔案中的指示，透過在UI中或使用API中遵循配方匯入工作流程，可用來在Adobe Experience Platform [!DNL Data Science Workspace]中建立配方。

要瞭解的概念：

- **配方**：配方是模型規格的Adobe術語，是代表特定機器學習、人工智慧演演算法或演演算法組合、處理邏輯，以及建置和執行已訓練的模型所需的組態（因此有助於解決特定業務問題）的頂層容器。
- **Source檔案**：專案中包含配方邏輯的個別檔案。

## 先決條件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 配方建立

配方建立從封裝來源檔案開始，以建置封存檔案。 Source檔案定義用來解決手頭特定問題的機器學習邏輯和演演算法，且以[!DNL Python]、R、PySpark或Scala撰寫。 構建的封存檔案採取Docker映像的形式。 建置後，封裝封存檔案會匯入至[!DNL Data Science Workspace]，以使用API](./import-packaged-recipe-api.md)在UI](./import-packaged-recipe-ui.md)或[中建立配方[。

### 基於Docker的模型編寫 {#docker-based-model-authoring}

Docker映像可讓開發人員將應用計畫與其所需的所有部分（例如程式庫和其他依賴項）一起封裝，然後作為一個封裝發出。

使用配方建立工作流程期間提供給您的認證，將建置的Docker映像推送到Azure容器登入。

若要取得您的Azure容器登入認證，請登入[Adobe Experience Platform](https://platform.adobe.com)。 在左側導覽欄中，導覽至&#x200B;**[!UICONTROL 工作流程]**。 選取&#x200B;**[!UICONTROL 匯入配方]**，然後選取&#x200B;**[!UICONTROL 啟動]**。 如需參考資訊，請參閱下面的熒幕擷圖。

![](../images/models-recipes/package-source-files/import.png)

**[!UICONTROL 設定]**&#x200B;頁面隨即開啟。 提供適當的&#x200B;**[!UICONTROL 配方名稱]**，例如「零售銷售配方」，並選擇性地提供說明或檔案URL。 完成後，按一下&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/package-source-files/configure.png)

選取適當的&#x200B;*執行階段*，然後為&#x200B;*型別*&#x200B;選擇&#x200B;**[!UICONTROL 分類]**。 您的Azure Container Registry認證會在完成後產生。

>[!NOTE]
>
>*Type*&#x200B;是設計配方所針對的機器學習問題類別，在訓練後用來協助量身打造評估訓練回合。

>[!TIP]
>
>- 針對[!DNL Python]配方，請選取&#x200B;**[!UICONTROL Python]**&#x200B;執行階段。
>- 針對R配方，請選取&#x200B;**[!UICONTROL R]**&#x200B;執行階段。
>- 針對PySpark配方，請選取&#x200B;**[!UICONTROL PySpark]**&#x200B;執行階段。 成品型別會自動填入。
>- 對於Scala配方，請選取&#x200B;**[!UICONTROL Spark]**&#x200B;執行階段。 成品型別會自動填入。

![](../images/models-recipes/package-source-files/docker-creds.png)

記下Docker主機、使用者名稱和密碼的值。 這些用於在下面概述的工作流程中建置和推播您的[!DNL Docker]影像。

>[!NOTE]
>
>Source URL會在完成下列步驟後提供。 在[後續步驟](#next-steps)中找到的後續教學課程中說明組態檔。

### 封裝來源檔案

首先，取得<a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform資料科學Workspace參考</a>存放庫中的範常式式碼基底。

- [建立Python Docker映像](#python-docker)
- [構建R Docker映像](#r-docker)
- [建置PySpark Docker影像](#pyspark-docker)
- [建立Scala (Spark) Docker影像](#scala-docker)

### 建置[!DNL Python] Docker映像 {#python-docker}

如果您尚未這樣做，請使用下列命令將[!DNL GitHub]存放庫複製到本機系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至目錄`experience-platform-dsw-reference/recipes/python/retail`。 在這裡，您會找到用來登入Docker及建置[!DNL Python Docker]影像的指令碼`login.sh`和`build.sh`。 如果您已準備好[Docker認證](#docker-based-model-authoring)，請依序輸入下列命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 構建時，您需要提供構建的Docker主機和版本標籤。

構建指令碼完成後，控制檯輸出中會為您提供Docker來源檔案URL。 在此特定範例中，看起來會像這樣：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

複製此URL並移至[後續步驟](#next-steps)。

### 建置R [!DNL Docker]映像 {#r-docker}

如果您尚未這樣做，請使用下列命令將[!DNL GitHub]存放庫複製到本機系統：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至複製存放庫內的目錄`experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting`。 在這裡您將找到用於登入Docker和構建R Docker映像的檔案`login.sh`和`build.sh`。 如果您已準備好[Docker認證](#docker-based-model-authoring)，請依序輸入下列命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 構建時，您需要提供構建的Docker主機和版本標籤。

構建指令碼完成後，控制檯輸出中會為您提供Docker來源檔案URL。 在此特定範例中，看起來會像這樣：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

複製此URL並移至[後續步驟](#next-steps)。

### 建置PySpark Docker影像 {#pyspark-docker}

使用以下命令將[!DNL GitHub]存放庫複製到本機系統以開始：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至目錄`experience-platform-dsw-reference/recipes/pyspark/retail`。 指令碼`login.sh`和`build.sh`位於此處，用於登入Docker和建置Docker映像。 如果您已準備好[Docker認證](#docker-based-model-authoring)，請依序輸入下列命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 構建時，您需要提供構建的Docker主機和版本標籤。

構建指令碼完成後，控制檯輸出中會為您提供Docker來源檔案URL。 在此特定範例中，看起來會像這樣：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

複製此URL並移至[後續步驟](#next-steps)。

### 構建Scala Docker映像 {#scala-docker}

首先，在終端機中使用下列命令將[!DNL GitHub]存放庫複製到您的本機系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接著，導覽至目錄`experience-platform-dsw-reference/recipes/scala`，您可以在其中找到指令碼`login.sh`和`build.sh`。 這些指令碼用於登入Docker和構建Docker映像。 如果您已準備好[Docker認證](#docker-based-model-authoring)，請依序輸入下列命令到終端機：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在嘗試使用`login.sh`指令碼登入Docker時遇到許可權錯誤，請嘗試使用命令`bash login.sh`。

執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 構建時，您需要提供構建的Docker主機和版本標籤。

構建指令碼完成後，控制檯輸出中會為您提供Docker來源檔案URL。 在此特定範例中，看起來會像這樣：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

複製此URL並移至[後續步驟](#next-steps)。

## 後續步驟 {#next-steps}

本教學課程將來源檔案封裝到配方中，這是將配方匯入[!DNL Data Science Workspace]的先決條件步驟。 您現在應該在Azure容器登入中擁有Docker影像以及對應的影像URL。 您現在已準備好開始有關將封裝配方匯入[!DNL Data Science Workspace]的教學課程。 選取下列其中一個教學課程連結以開始：

- [在UI中匯入封裝的配方](./import-packaged-recipe-ui.md)
- [使用API匯入封裝的配方](./import-packaged-recipe-api.md)
