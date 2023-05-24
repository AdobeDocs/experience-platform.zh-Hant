---
keywords: Experience Platform；包源檔案；資料科學工作區；熱門主題；Docker;docker影像
solution: Experience Platform
title: 將源檔案打包到處方
type: Tutorial
description: 本教程提供有關如何將提供的零售銷售示例源檔案打包到存檔檔案中的說明，該存檔檔案可通過遵循UI中的處方導入工作流或使用API在Adobe Experience Platform資料科學工作區中建立處方。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# 將源檔案打包到處方

本教程提供了有關如何將提供的零售銷售示例源檔案打包到存檔檔案中的說明，該檔案可用於在Adobe Experience Platform建立處方 [!DNL Data Science Workspace] 在UI中或使用API執行處方導入工作流。

要瞭解的概念：

- **食譜**:配方是「模型」規範的Adobe術語，是代表特定機器學習、人工智慧算法或整合算法、處理邏輯和配置的頂級容器，用於構建和執行經過訓練的模型，從而幫助解決特定的業務問題。
- **源檔案**:項目中包含處方邏輯的單個檔案。

## 先決條件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 處方建立

處方建立從打包源檔案開始，以生成存檔檔案。 源檔案定義用於解決當前特定問題的機器學習邏輯和算法，並寫入 [!DNL Python]、R、PySpark或Scala。 生成的存檔檔案採用Docker映像的形式。 生成後，打包的存檔檔案將導入到 [!DNL Data Science Workspace] 建立處方 [在UI中](./import-packaged-recipe-ui.md) 或 [使用API](./import-packaged-recipe-api.md)。

### 基於Docker的模型創作 {#docker-based-model-authoring}

Docker映像允許開發人員將應用程式與其需要的所有部件（如庫和其他依賴項）打包，然後將其作為一個包發出。

生成的Docker映像將在處方建立工作流期間使用提供給您的憑據推送到Azure容器註冊表。

要獲取Azure容器註冊表憑據，請登錄 [Adobe Experience Platform](https://platform.adobe.com)。 在左導航列上，導航到 **[!UICONTROL 工作流]**。 選擇 **[!UICONTROL 導入處方]** 然後選擇 **[!UICONTROL 啟動]**。 請參閱下面的螢幕抓圖以供參考。

![](../images/models-recipes/package-source-files/import.png)

的 **[!UICONTROL 配置]** 的上界。 提供適當 **[!UICONTROL 處方名稱]**&#x200B;例如，「零售銷售處方」，並根據需要提供說明或文檔URL。 完成後，按一下 **[!UICONTROL 下一個]**。

![](../images/models-recipes/package-source-files/configure.png)

選擇相應的 *運行時*，然後選擇 **[!UICONTROL 分類]** 為 *類型*。 完成後將生成Azure容器註冊表憑據。

>[!NOTE]
>
>*類型* 是機器學習的類問題，該配方是為之設計的，在訓練後用於幫助定制評估訓練運行。

>[!TIP]
>
>- 對於 [!DNL Python] 處方選擇 **[!UICONTROL 蟒]** 運行時。
>- 對於R配方，選擇 **[!UICONTROL R]** 運行時。
>- 對於PySpark配方，請選擇 **[!UICONTROL PySpark]** 運行時。 自動填充對象類型。
>- 對於Scala配方，選擇 **[!UICONTROL 火花]** 運行時。 自動填充對象類型。


![](../images/models-recipes/package-source-files/docker-creds.png)

請注意Docker主機、用戶名和密碼的值。 這些用於構建和推送 [!DNL Docker] 影像。

>[!NOTE]
>
>在完成以下步驟後提供源URL。 配置檔案將在以下教程中介紹，這些教程位於 [後續步驟](#next-steps)。

### 將源檔案打包

首先獲取在 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform資料科學工作區參考</a> 儲存庫。

- [生成Python Docker映像](#python-docker)
- [生成R Docker映像](#r-docker)
- [生成PySpark Docker映像](#pyspark-docker)
- [生成Scala(Spark)Docker影像](#scala-docker)

### 生成 [!DNL Python] Docker影像 {#python-docker}

如果尚未複製，請克隆 [!DNL GitHub] 將儲存庫連接到您的本地系統，並使用以下命令：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導航到目錄 `experience-platform-dsw-reference/recipes/python/retail`。 在這裡，您將找到 `login.sh` 和 `build.sh` 用於登錄到Docker並生成 [!DNL Python Docker] 影像。 如果你 [Docker憑據](#docker-based-model-authoring) 就緒，按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，執行登錄指令碼時，需要提供Docker主機、用戶名和密碼。 在生成時，需要為生成提供Docker主機和版本標籤。

生成指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定示例，它將類似於：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

複製此URL並轉到 [後續步驟](#next-steps)。

### 生成R [!DNL Docker] 影像 {#r-docker}

如果尚未複製，請克隆 [!DNL GitHub] 將儲存庫連接到您的本地系統，並使用以下命令：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導航到目錄 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 在克隆的儲存庫中。 在這裡，你會找到 `login.sh` 和 `build.sh` 用於登錄到Docker和生成R Docker映像。 如果你 [Docker憑據](#docker-based-model-authoring) 就緒，按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

請注意，執行登錄指令碼時，需要提供Docker主機、用戶名和密碼。 在生成時，需要為生成提供Docker主機和版本標籤。

生成指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定示例，它將類似於：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

複製此URL並轉到 [後續步驟](#next-steps)。

### 生成PySpark Docker映像 {#pyspark-docker}

從克隆開始 [!DNL GitHub] 將儲存庫連接到您的本地系統，並使用以下命令：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導航到目錄 `experience-platform-dsw-reference/recipes/pyspark/retail`。 指令碼 `login.sh` 和 `build.sh` 位於此處，用於登錄到Docker和生成Docker映像。 如果你 [Docker憑據](#docker-based-model-authoring) 就緒，按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，執行登錄指令碼時，需要提供Docker主機、用戶名和密碼。 在生成時，需要為生成提供Docker主機和版本標籤。

生成指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定示例，它將類似於：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

複製此URL並轉到 [後續步驟](#next-steps)。

### 生成Scala Docker映像 {#scala-docker}

從克隆開始 [!DNL GitHub] 在終端中使用以下命令將儲存庫儲存到本地系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接下來，導航到目錄 `experience-platform-dsw-reference/recipes/scala` 可以在其中找到指令碼 `login.sh` 和 `build.sh`。 這些指令碼用於登錄到Docker並生成Docker映像。 如果你 [Docker憑據](#docker-based-model-authoring) 就緒，按順序向終端輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在嘗試使用 `login.sh` 指令碼，嘗試使用命令 `bash login.sh`。

執行登錄指令碼時，需要提供Docker主機、用戶名和密碼。 在生成時，需要為生成提供Docker主機和版本標籤。

生成指令碼完成後，控制台輸出中會給您一個Docker源檔案URL。 對於此特定示例，它將類似於：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

複製此URL並轉到 [後續步驟](#next-steps)。

## 後續步驟 {#next-steps}

本教程將源檔案打包到配方中，這是將配方導入的先決條件步驟 [!DNL Data Science Workspace]。 您現在應在Azure Container Registry中擁有Docker映像以及相應的映像URL。 您現在已準備好開始將打包的配方導入到 [!DNL Data Science Workspace]。 選擇以下教程連結之一以開始：

- [在UI中導入打包的處方](./import-packaged-recipe-ui.md)
- [使用API導入打包的處方](./import-packaged-recipe-api.md)
