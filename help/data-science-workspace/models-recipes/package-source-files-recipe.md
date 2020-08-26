---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: 將來源檔案封裝至配方
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 0%

---


# 將來源檔案封裝至配方

本教學課程提供如何將提供的零售銷售範例來源檔案封裝成封存檔案的指示，此檔案可透過遵循UI或API中的方式匯入工作流程，在Adobe Experience Platform中用來建立方式。 [!DNL Data Science Workspace]

要瞭解的概念：

- **方式**:配方是Adobe的模型規格術語，是代表特定機器學習、人工智慧演算法或整合演算法、處理邏輯和設定的頂層容器，以建立並執行已訓練的模型，進而協助解決特定商業問題。
- **來源檔案**:專案中包含方式邏輯的個別檔案。

## 必要條件

- [!DNL Docker](https://docs.docker.com/install/#supported-platforms)
- [!DNL Python 3 and pip](https://docs.conda.io/en/latest/miniconda.html)
- [!DNL Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [!DNL Maven](https://maven.apache.org/install.html)

## 方式建立

方式建立從封裝來源檔案開始，以建立封存檔案。 來源檔案會定義機器學習邏輯和演算法，用於解決手邊的特定問題，並以 [!DNL Python]R、PySpark或Scala編寫。 構建的存檔檔案採用Docker映像的形式。 建立後，封裝的封存檔案會匯入至UI [!DNL Data Science Workspace] 中，以 [或使用](./import-packaged-recipe-ui.md) API [建立方式](./import-packaged-recipe-api.md)。

### 基於Docker的模型編寫 {#docker-based-model-authoring}

Docker映像允許開發人員將應用程式與其所需的所有部件（如庫和其他依賴項）打包，然後以一個包的形式發佈。

內建的Docker影像會使用在方式建立工作流程期間提供給您的認證，推送至Azure容器註冊表。

若要取得您的Azure容器註冊表認證，請登入 [Adobe Experience Platform](https://platform.adobe.com)。 在左邊導覽欄，導覽至「工 **[!UICONTROL 作流程」]**。 選擇「 **[!UICONTROL 匯入方式]** 」，然後選 **[!UICONTROL 取「啟動]**」。 請參閱下方的螢幕擷取畫面以供參考。

![](../images/models-recipes/package-source-files/import.png)

「設 *定* 」頁面隨即開啟。 提供適當的 *配方名稱*，例如「零售銷售配方」，並選擇性地提供說明或檔案URL。 完成後，按一下「 **[!UICONTROL Next（下一步）]**」。

![](../images/models-recipes/package-source-files/configure.png)

選取適當的 *執行階段*，然後選擇類 **[!UICONTROL 型的]** 「分 *類」*。 您的Azure容器註冊表認證會在完成後產生。

>[!NOTE]
>
>*Type* 是機器學習問題的類，它是為機器學習問題而設計的，在訓練後用於幫助定制評估訓練運行。

>[!TIP]
>
>- 對於方 [!DNL Python] 式，請選取 **[!UICONTROL Python]** 執行階段。
>- 對於R方式，請選擇 **[!UICONTROL R]** Runtime。
>- 對於PySpark配方，請選取 **[!UICONTROL PySpark執行時]** 期。 對象類型自動填充。
>- 對於Scala配方，請選取 **[!UICONTROL Spark執行]** 階段。 對象類型自動填充。


![](../images/models-recipes/package-source-files/docker-creds.png)

請注意Docker主 *機*、 *Username*&#x200B;和 *Password的值*。 這些功能可用來在下列工作流程中 [!DNL Docker] 建立和推播您的影像。

>[!NOTE]
>
>完成下列步驟後，即會提供來源URL。 後續的教學課程會說明設定檔案，這些教學課程可在後續 [步驟中找到](#next-steps)。

### 封裝來源檔案

首先，取得Experience Platform Data Science Workspace參考儲存庫 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">中的范常式式碼基底</a> 。

- [建立Python Docker影像](#python-docker)
- [構建R Docker映像](#r-docker)
- [建立PySpark Docker影像](#pyspark-docker)
- [建立Scala(Spark)Docker影像](#scala-docker)

### 建立 [!DNL Python] Docker影像 {#python-docker}

如果尚未執行此操作，請使用以下命 [!DNL GitHub] 令將儲存庫克隆到本地系統上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. 在這裡，您將找到用於登 `login.sh` 錄 `build.sh` 到Docker和構建映像的指令碼 [!DNL Python Docker] 。 如果您的 [Docker憑據已就緒](#docker-based-model-authoring) ，請按順序輸入以下命令：

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

複製此URL，並移至下 [一步](#next-steps)。

### Build R影 [!DNL Docker] 像 {#r-docker}

如果尚未執行此操作，請使用以下命 [!DNL GitHub] 令將儲存庫克隆到本地系統上：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導航到克隆的資 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 料庫內的目錄。 在這裡，您將找到用 `login.sh` 於 `build.sh` 登錄Docker和構建R Docker映像的檔案。 如果您的 [Docker憑據已就緒](#docker-based-model-authoring) ，請按順序輸入以下命令：

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

複製此URL，並移至下 [一步](#next-steps)。

### 建立PySpark Docker影像 {#pyspark-docker}

首先，使用以 [!DNL GitHub] 下命令將儲存庫克隆到本地系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/pyspark/retail`. 指令碼 `login.sh` 和 `build.sh` 位於此處，用於登錄到Docker和構建Docker映像。 如果您的 [Docker憑據已就緒](#docker-based-model-authoring) ，請按順序輸入以下命令：

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

複製此URL，並移至下 [一步](#next-steps)。

### 建立Scala Docker影像 {#scala-docker}

首先，在終端 [!DNL GitHub] 機中使用以下命令將儲存庫克隆到本地系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接著，導覽至您可 `experience-platform-dsw-reference/recipes/scala` 以找到指令碼和的 `login.sh` 目錄 `build.sh`。 這些指令碼用於登錄到Docker並生成Docker映像。 如果您的 [Docker認證已就緒](#docker-based-model-authoring) ，請按順序向終端輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在嘗試使用指令碼登錄Docker時收到權限錯誤，請 `login.sh` 嘗試使用命令 `bash login.sh`。

執行登錄指令碼時，需要提供Docker主機、用戶名和密碼。 建立時，您必須提供Docker主機和版本標籤以用於建立。

建置指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定範例，其外觀會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

複製此URL，並移至下 [一步](#next-steps)。

## 下一步 {#next-steps}

本教學課程將來源檔案封裝為「配方」，這是將「配方」匯入的先決條件步驟 [!DNL Data Science Workspace]。 您現在應該在Azure容器註冊表中有Docker影像，以及對應的影像URL。 您現在已準備好開始將封裝配方匯入的教學課程 [!DNL Data Science Workspace]。 請選取下列其中一個教學課程連結以開始使用：

- [在UI中匯入封裝的方式](./import-packaged-recipe-ui.md)
- [使用API匯入封裝的方式](./import-packaged-recipe-api.md)