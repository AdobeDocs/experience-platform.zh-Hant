---
keywords: Experience Platform；包源檔案；資料科學工作區；熱門主題；Docker;docker影像
solution: Experience Platform
title: 將來源檔案封裝至配方
topic-legacy: tutorial
type: Tutorial
description: 本教學課程提供如何將提供的零售銷售範例來源檔案封裝成封存檔案的指示，此檔案可依照UI或API中的方式匯入工作流程，用於在Adobe Experience Platform資料科學工作區中建立方式。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# 將來源檔案封裝至配方

本教學課程提供如何將提供的零售銷售範例來源檔案封裝成封存檔案的指示，此檔案可依照UI或API中的方式匯入工作流程，用於在Adobe Experience Platform[!DNL Data Science Workspace]中建立方式。

要瞭解的概念：

- **方式**:配方是「模型」規格的Adobe術語，是表示特定機器學習、人工智慧演算法或整合演算法、處理邏輯和組態的頂層容器，以建立並執行已訓練的模型，進而協助解決特定商業問題。
- **來源檔案**:專案中包含方式邏輯的個別檔案。

## 先決條件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 方式建立

方式建立從封裝來源檔案開始，以建立封存檔案。 來源檔案定義機器學習邏輯和演算法，用於解決手邊的特定問題，並以[!DNL Python]、R、PySpark或Scala編寫。 構建的存檔檔案採用Docker映像的形式。 建立後，封裝的封存檔案會匯入至[!DNL Data Science Workspace]，以使用API](./import-packaged-recipe-api.md)在UI中建立配方[。](./import-packaged-recipe-ui.md)[

### 基於Docker的模型編寫{#docker-based-model-authoring}

Docker映像允許開發人員將應用程式與其所需的所有部件（如庫和其他依賴項）打包，然後以一個包的形式發佈。

內建的Docker影像會使用在方式建立工作流程期間提供給您的認證，推送至Azure容器註冊表。

若要取得Azure容器註冊表憑證，請登入[Adobe Experience Platform](https://platform.adobe.com)。 在左邊導覽欄上，導覽至&#x200B;**[!UICONTROL Workflows]**。 選擇&#x200B;**[!UICONTROL Import Recipe]** ，然後選擇&#x200B;**[!UICONTROL Launch]**。 請參閱下方的螢幕擷取畫面以供參考。

![](../images/models-recipes/package-source-files/import.png)

**[!UICONTROL Configure]**&#x200B;頁面隨即開啟。 提供適當的&#x200B;**[!UICONTROL Recipe Name]**，例如「零售銷售方式」，並選擇性地提供說明或檔案URL。 完成後，按一下&#x200B;**[!UICONTROL Next]**。

![](../images/models-recipes/package-source-files/configure.png)

選擇適當的&#x200B;*Runtime*，然後為&#x200B;*Type*&#x200B;選擇&#x200B;**[!UICONTROL Classification]**。 您的Azure容器註冊表認證會在完成後產生。

>[!NOTE]
>
>*Type是* 專為機器學習類別設計的問題，在訓練後會使用它，以協助量身打造評估訓練執行。

>[!TIP]
>
>- 對於[!DNL Python]配方，請選擇&#x200B;**[!UICONTROL Python]**&#x200B;執行階段。
>- 對於R方式，請選擇&#x200B;**[!UICONTROL R]**&#x200B;執行階段。
>- 對於PySpark配方，請選取&#x200B;**[!UICONTROL PySpark]**&#x200B;執行時期。 對象類型自動填充。
>- 對於Scala配方，請選擇&#x200B;**[!UICONTROL Spark]**&#x200B;運行時。 對象類型自動填充。


![](../images/models-recipes/package-source-files/docker-creds.png)

請注意Docker主機、用戶名和密碼的值。 這些功能可用來在下列工作流程中建立和推播您的[!DNL Docker]影像。

>[!NOTE]
>
>完成下列步驟後，即會提供來源URL。 在[後續步驟](#next-steps)中的後續教學課程中，將說明此設定檔案。

### 封裝來源檔案

首先，獲取<a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform資料科學工作區參考</a>儲存庫中的示例代碼庫。

- [建立Python Docker影像](#python-docker)
- [構建R Docker映像](#r-docker)
- [建立PySpark Docker影像](#pyspark-docker)
- [建立Scala(Spark)Docker影像](#scala-docker)

### 構建[!DNL Python] Docker映像{#python-docker}

如果您尚未這樣做，請使用以下命令將[!DNL GitHub]儲存庫克隆到本地系統上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導航至`experience-platform-dsw-reference/recipes/python/retail`目錄。 在這裡，您將找到用於登錄到Docker和構建[!DNL Python Docker]映像的指令碼`login.sh`和`build.sh`。 如果您的[Docker憑據](#docker-based-model-authoring)已就緒，請按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，在執行登錄指令碼時，您需要提供Docker主機、用戶名和密碼。 建立時，您必須提供Docker主機和版本標籤以用於建立。

建置指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定範例，其外觀會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

複製此URL並移至[後續步驟](#next-steps)。

### 構建R [!DNL Docker]映像{#r-docker}

如果您尚未這樣做，請使用以下命令將[!DNL GitHub]儲存庫克隆到本地系統上：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導航到克隆的儲存庫內的`experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting`目錄。 在這裡，您將找到用於登錄Docker和生成R Docker映像的`login.sh`和`build.sh`檔案。 如果您的[Docker憑據](#docker-based-model-authoring)已就緒，請按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

請注意，在執行登錄指令碼時，您需要提供Docker主機、用戶名和密碼。 建立時，您必須提供Docker主機和版本標籤以用於建立。

建置指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定範例，其外觀會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

複製此URL並移至[後續步驟](#next-steps)。

### 建立PySpark Docker影像{#pyspark-docker}

首先，使用以下命令將[!DNL GitHub]儲存庫克隆到本地系統上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導航至`experience-platform-dsw-reference/recipes/pyspark/retail`目錄。 指令碼`login.sh`和`build.sh`位於此處，用於登錄到Docker和生成Docker映像。 如果您的[Docker憑據](#docker-based-model-authoring)已就緒，請按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，在執行登錄指令碼時，您需要提供Docker主機、用戶名和密碼。 建立時，您必須提供Docker主機和版本標籤以用於建立。

建置指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定範例，其外觀會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

複製此URL並移至[後續步驟](#next-steps)。

### 建立Scala Docker影像{#scala-docker}

首先，在終端機中使用以下命令將[!DNL GitHub]儲存庫克隆到本地系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接著，導覽至目錄`experience-platform-dsw-reference/recipes/scala`，您可在其中找到指令碼`login.sh`和`build.sh`。 這些指令碼用於登錄到Docker並生成Docker映像。 如果您的[Docker憑據](#docker-based-model-authoring)已就緒，請按順序向終端輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在嘗試使用`login.sh`指令碼登入Docker時收到權限錯誤，請嘗試使用命令`bash login.sh`。

執行登錄指令碼時，需要提供Docker主機、用戶名和密碼。 建立時，您必須提供Docker主機和版本標籤以用於建立。

建置指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定範例，其外觀會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

複製此URL並移至[後續步驟](#next-steps)。

## 下一步 {#next-steps}

本教學課程將來源檔案封裝成配方，這是將配方匯入[!DNL Data Science Workspace]的先決條件步驟。 您現在應該在Azure容器註冊表中有Docker影像，以及對應的影像URL。 您現在已準備好開始將封裝配方匯入[!DNL Data Science Workspace]的教學課程。 請選取下列其中一個教學課程連結以開始使用：

- [在UI中匯入封裝的方式](./import-packaged-recipe-ui.md)
- [使用API匯入封裝的方式](./import-packaged-recipe-api.md)
