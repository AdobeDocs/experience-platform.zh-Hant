---
keywords: Experience Platform；套件來源檔案；Data Science Workspace；熱門主題；Docker;Docker影像
solution: Experience Platform
title: 將源檔案打包到配方中
type: Tutorial
description: 本教學課程提供相關指示，說明如何將提供的零售銷售範例來源檔案封裝至封存檔案，而封存檔案可遵循UI或API中的方式匯入工作流程，用於在Adobe Experience Platform Data Science Workspace中建立方式。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# 將源檔案打包到配方中

本教學課程提供相關指示，說明如何將提供的零售銷售範例來源檔案封裝至封存檔案，以便在Adobe Experience Platform中建立方式 [!DNL Data Science Workspace] 在UI中或使用API遵循方式匯入工作流程。

要了解的概念：

- **訣竅**:配方是「模型」規範的Adobe術語，是代表特定機器學習、人工智慧演算法或整合演算法、處理邏輯和配置的頂級容器，用於建立和執行經過訓練的模型，從而幫助解決特定的業務問題。
- **源檔案**:專案中包含方式邏輯的個別檔案。

## 先決條件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 方式建立

方式建立從打包源檔案開始，以生成歸檔檔案。 源檔案定義用於解決手頭特定問題的機器學習邏輯和算法，並以下列任一種形式寫入 [!DNL Python]、R、PySpark或Scala。 構建的歸檔檔案採用Docker映像的形式。 構建後，打包的存檔檔案將導入 [!DNL Data Science Workspace] 建立方式 [在UI中](./import-packaged-recipe-ui.md) 或 [使用API](./import-packaged-recipe-api.md).

### 基於Docker的模型創作 {#docker-based-model-authoring}

Docker映像允許開發人員將應用程式打包為所需的所有部件（如庫和其他依賴項），然後將其作為一個包發出。

內建的Docker映像將使用在處方建立工作流程期間提供給您的憑據推送到Azure容器註冊表。

要獲取Azure容器註冊表憑據，請登錄 [Adobe Experience Platform](https://platform.adobe.com). 在左側導覽欄中，導覽至 **[!UICONTROL 工作流程]**. 選擇 **[!UICONTROL 導入方式]** 後續選取 **[!UICONTROL Launch]**. 請參閱下方的螢幕擷取畫面以供參考。

![](../images/models-recipes/package-source-files/import.png)

此 **[!UICONTROL 設定]** 頁面開啟。 提供適當 **[!UICONTROL 方式名稱]**，例如「零售銷售方式」，並選擇性地提供說明或檔案URL。 完成後，按一下 **[!UICONTROL 下一個]**.

![](../images/models-recipes/package-source-files/configure.png)

選取適當的 *執行階段*，然後選擇 **[!UICONTROL 分類]** for *類型*. 完成後將生成Azure容器註冊表憑據。

>[!NOTE]
>
>*類型* 是機器學習類問題的配方設計，用於訓練後幫助定制評估訓練運行。

>[!TIP]
>
>- 針對 [!DNL Python] 方式選擇 **[!UICONTROL Python]** 執行階段。
>- 對於R方式，請選取 **[!UICONTROL R]** 執行階段。
>- PySpark菜譜選擇 **[!UICONTROL PySpark]** 執行階段。 工件類型會自動填入。
>- Scala訣竅請選取 **[!UICONTROL 火花]** 執行階段。 工件類型會自動填入。


![](../images/models-recipes/package-source-files/docker-creds.png)

請注意Docker主機、使用者名稱和密碼的值。 這些用於建立和推送您的 [!DNL Docker] 以下概述的工作流程中的影像。

>[!NOTE]
>
>完成下列步驟後，會提供來源URL。 設定檔案會在下列後續教學課程中說明： [後續步驟](#next-steps).

### 封裝源檔案

首先，取得 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience PlatformData Science Workspace參考</a> 存放庫。

- [生成Python Docker映像](#python-docker)
- [生成R Docker映像](#r-docker)
- [建立PySpark Docker影像](#pyspark-docker)
- [生成縮放(Spark)Docker影像](#scala-docker)

### 建置 [!DNL Python] Docker影像 {#python-docker}

如果您尚未這麼做，請複製 [!DNL GitHub] 儲存庫，使用以下命令到本地系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至目錄 `experience-platform-dsw-reference/recipes/python/retail`. 在此，您會找到指令碼 `login.sh` 和 `build.sh` 用於登入Docker和建置 [!DNL Python Docker] 影像。 如果您有 [Docker憑據](#docker-based-model-authoring) 就緒，請按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 建置時，您必須提供Docker主機和版本標籤供組建使用。

建置指令碼完成後，主控台輸出中會為您指定Docker來源檔案URL。 對於此特定範例，看起來會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

複製此URL並移至 [後續步驟](#next-steps).

### 建置R [!DNL Docker] 影像 {#r-docker}

如果您尚未這麼做，請複製 [!DNL GitHub] 儲存庫，使用以下命令到本地系統：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至目錄 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 複製的存放庫。 在這裡，你會找到檔案 `login.sh` 和 `build.sh` 用於登錄到Docker並生成R Docker映像。 如果您有 [Docker憑據](#docker-based-model-authoring) 就緒，請按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 建置時，您必須提供Docker主機和版本標籤供組建使用。

建置指令碼完成後，主控台輸出中會為您指定Docker來源檔案URL。 對於此特定範例，看起來會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

複製此URL並移至 [後續步驟](#next-steps).

### 建立PySpark Docker影像 {#pyspark-docker}

從複製開始 [!DNL GitHub] 儲存庫，使用以下命令到本地系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

導覽至目錄 `experience-platform-dsw-reference/recipes/pyspark/retail`. 指令碼 `login.sh` 和 `build.sh` 位於此處，用於登入Docker和建立Docker映像。 如果您有 [Docker憑據](#docker-based-model-authoring) 就緒，請按順序輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

請注意，執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 建置時，您必須提供Docker主機和版本標籤供組建使用。

建置指令碼完成後，主控台輸出中會為您指定Docker來源檔案URL。 對於此特定範例，看起來會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

複製此URL並移至 [後續步驟](#next-steps).

### 建立Scala Docker映像 {#scala-docker}

從複製開始 [!DNL GitHub] 在終端機中使用下列命令將存放庫存放至您的本機系統：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接下來，導覽至目錄 `experience-platform-dsw-reference/recipes/scala` 可在此找到指令碼 `login.sh` 和 `build.sh`. 這些指令碼用於登入Docker並建置Docker映像。 如果您有 [Docker憑據](#docker-based-model-authoring) 就緒，請按順序向終端輸入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在嘗試使用 `login.sh` 指令碼，嘗試使用命令 `bash login.sh`.

執行登入指令碼時，您需要提供Docker主機、使用者名稱和密碼。 建置時，您必須提供Docker主機和版本標籤供組建使用。

建置指令碼完成後，主控台輸出中會為您指定Docker來源檔案URL。 對於此特定範例，看起來會類似：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

複製此URL並移至 [後續步驟](#next-steps).

## 後續步驟 {#next-steps}

本教學課程將來源檔案封裝至方式，這是將方式匯入至的先決條件步驟 [!DNL Data Science Workspace]. 您現在應在Azure容器註冊表中擁有Docker影像，以及對應的影像URL。 您現在已準備好開始教學課程，了解如何將封裝方式匯入 [!DNL Data Science Workspace]. 選取下列其中一個教學課程連結以開始使用：

- [在UI中匯入封裝配方](./import-packaged-recipe-ui.md)
- [使用API匯入封裝方式](./import-packaged-recipe-api.md)
