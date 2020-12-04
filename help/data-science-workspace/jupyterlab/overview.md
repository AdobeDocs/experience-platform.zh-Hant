---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: JupyterLab使用指南
topic: Overview
description: JupyterLab是Project Jupyter的網路使用者介面，並與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與Jupyter筆記型電腦、程式碼和資料搭配使用。 本文檔概述了JupyterLab及其功能，以及執行常見操作的說明。
translation-type: tm+mt
source-git-commit: d5e7679ac41fd476c77a98920d7f7aeaefacec6d
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 9%

---


# [!DNL JupyterLab] 使用者指南

[!DNL JupyterLab] 是Project Jupyter的網路型使用者介 [面](https://jupyter.org/) ，並與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與Jupyter筆記型電腦、程式碼和資料搭配使用。

本檔案提供執行常 [!DNL JupyterLab] 見動作的概觀及功能說明。

## [!DNL JupyterLab] on [!DNL Experience Platform]

Experience Platform的JupyterLab整合隨附架構變更、設計考量、自訂的筆記型電腦擴充功能、預先安裝的程式庫和Adobe主題介面。

下列清單概述JupyterLab在Platform上獨有的一些功能：

| 功能 | 說明 |
| --- | --- |
| **內核** | 內核提供筆記型電腦和 [!DNL JupyterLab] 其他前端，能夠以不同的寫程式語言執行和查看代碼。 [!DNL Experience Platform] 提供額外的內核，以支 [!DNL Python]援R、PySpark和的開發 [!DNL Spark]。 有關詳細 [資訊](#kernels) ，請參閱內核部分。 |
| **資料存取** | 直接從內部存取現有資料集， [!DNL JupyterLab] 並具備完整的讀取和寫入功能支援。 |
| **[!DNL Platform]服務整合** | 內建整合可讓您直接從內部運用 [!DNL Platform] 其他服務 [!DNL JupyterLab]。 「與其他平台服務整合」一節提供支援整合 [的完整清單](#service-integration)。 |
| **驗證** | 除了 <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab的內建安全性模型外</a>，您的應用程式與Experience Platform（包括平台服務對服務通訊）之間的每次互動都會透過 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)加密和驗證</a>。 |
| **開發程式庫** | 在中 [!DNL Experience Platform], [!DNL JupyterLab] 提供預先安裝的 [!DNL Python]、R和PySpark程式庫。 如需支援 [的程式庫](#supported-libraries) ，請參閱附錄。 |
| **程式庫控制器** | 當預先安裝的程式庫不符合您的需求時，可為Python和R安裝其他程式庫，並暫時儲存在隔離的容器中，以維持資料的完整性並保 [!DNL Platform] 持資料的安全。 有關詳細 [資訊](#kernels) ，請參閱內核部分。 |

>[!NOTE]
>
>其他程式庫僅適用於安裝程式庫的作業階段。 啟動新會話時，必須重新安裝所需的任何其他庫。

## 與其他服務整 [!DNL Platform] 合 {#service-integration}

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 將on整 [!DNL JupyterLab] 合為 [!DNL Platform] 內嵌IDE，可讓它與其他服務互動， [!DNL Platform] 讓您充份運用 [!DNL Platform] 其潛能。 下列服 [!DNL Platform] 務可在下列網站取得 [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** 使用讀寫功能存取和探索資料集。
* **[!DNL Query Service]:** 使用SQL訪問和探索資料集，在處理大量資料時提供較低的資料存取開銷。
* **[!DNL Sensei ML Framework]:** 模型開發具備訓練和評分資料的能力，而且只要按一下，就能建立配方。
* **[!DNL Experience Data Model (XDM)]:** 標準化和互操作性是Adobe Experience Platform的主要概念。 [Adobe推動的Experience Data Model(XDM)](https://www.adobe.com/go/xdm-home-en)，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

>[!NOTE]
>
>上的 [!DNL Platform] 某些服務整合 [!DNL JupyterLab] 僅限於特定內核。 有關詳細資訊，請參 [閱](#kernels) 「內核」部分。

## 主要功能與常用作業

以下各節提供有關執 [!DNL JupyterLab] 行常見操作的主要功能和說明的資訊：

* [存取JupyterLab](#access-jupyterlab)
* [JupyterLab介面](#jupyterlab-interface)
* [程式碼儲存格](#code-cells)
* [內核](#kernels)
* [內核會話](#kernel-sessions)
* [啟動程式](#launcher)

### 存取 [!DNL JupyterLab] {#access-jupyterlab}

在 [Adobe Experience Platform](https://platform.adobe.com)，從左側導覽欄選 **取「筆記型電腦** 」。 請等待一些時 [!DNL JupyterLab] 間以完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 介面 {#jupyterlab-interface}

介面 [!DNL JupyterLab] 由功能表列、可折疊的左側邊欄，以及包含檔案與活動標籤的主要工作區組成。

**選單列**

介面頂端的選單列有頂層選單，可顯示使用鍵盤快速鍵的 [!DNL JupyterLab] 動作：

* **檔案：** 與檔案和目錄相關的操作
* **編輯：** 與編輯檔案和其他活動相關的動作
* **檢視：** 改變外觀的動作 [!DNL JupyterLab]
* **執行：** 在不同活動（如筆記型電腦和代碼控制台）中運行代碼的操作
* **內核：** 用於管理內核的操作
* **標籤：** 開啟的檔案與活動清單
* **設定：** 常用設定和進階設定編輯器
* **說明：** 內核幫助 [!DNL JupyterLab] 連結清單

**左側欄**

左側邊欄包含可點選的標籤，可存取下列功能：

* **檔案瀏覽器：** 已保存的筆記本文檔和目錄清單
* **資料總管：** 瀏覽、存取和探索資料集和結構
* **運行內核和終端：** 具有終止能力的活動內核和終端會話清單
* **命令：** 有用命令的清單
* **儲存格偵測器：** 一種單元格編輯器，它提供對工具和元資料的訪問，這些工具和元資料對於設定用於演示的筆記本有用
* **頁籤：** 開啟的標籤清單

按一下標籤以顯示其功能，或按一下展開的標籤以收合左側邊欄，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作區**

中的主要工作區 [!DNL JupyterLab] 域可讓您將檔案和其他活動排列成標籤面板，這些標籤可以調整大小或細分。 將標籤拖曳至標籤面板的中央，以移轉標籤。 將標籤拖曳至面板的左、右、上或下方，以劃分面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 程式碼儲存格 {#code-cells}

代碼單元格是筆記型電腦的主要內容。 它們包含的原始碼為筆記型電腦相關內核的語言，以及執行代碼單元格後的輸出。 每個代碼單元格的右側顯示一個執行計數，該代碼單元格表示其執行順序。

![](../images/jupyterlab/user-guide/code_cell.png)

常見的儲存格動作說明如下：

* **新增儲存格：** 按一下筆記本菜單中的加&#x200B;**號(+**)可添加空單元格。 新儲存格會置於目前正在互動的儲存格下方，或在筆記型電腦的結尾處（如果沒有特定儲存格在焦點中）。

* **移動儲存格：** 將游標置於您要移動的儲存格右側，然後按一下並拖曳儲存格至新位置。 此外，將一個單元格從一個筆記本移動到另一個筆記本會複製該單元格及其內容。

* **執行儲存格：** 按一下要執行的單元格的主體，然後按一下筆記本菜 **單中的****** play表徵圖()。 當內核處理執行時，單元格的執行計數器中會顯示星號(**\***)，並在完成時被整數替換。

* **刪除儲存格：** 按一下要刪除的單元格的主體，然後按一下剪 **式** 表徵圖。

### 內核 {#kernels}

筆記型電腦內核是用於處理筆記型電腦單元的語言專用計算引擎。 除了R、 [!DNL Python]PySpark和 [!DNL JupyterLab] (Scala)中提供其他語 [!DNL Spark] 言支援。 開啟筆記本文檔時，將啟動關聯內核。 當執行筆記本單元時，內核執行計算並產生可能消耗大量CPU和記憶體資源的結果。 請注意，在內核關閉之前，不會釋放已分配的記憶體。

某些特性和功能限於下表所述的特定內核：

| 內核 | 資料庫安裝支援 | [!DNL Platform] 整合 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 無 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 內核會話 {#kernel-sessions}

每個活動的筆記本或活動都 [!DNL JupyterLab] 使用內核會話。 從左側邊欄展開「運行終端和內核」 **頁籤，可找到所有活動會話** 。 通過觀察筆記本介面的右上角，可以確定筆記本內核的類型和狀態。 在下圖中，筆記本的關聯內核為 **[!DNL Python]3** ，其當前狀態由右側的灰色圓圈表示。 空心圓表示空閒內核，實心圓表示忙碌內核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果內核長時間處於關閉或非活動狀態，則無 **內核！** 顯示實心圓。 通過按一下內核狀態並選擇相應的內核類型激活內核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 啟動程式 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定義的 *Launcher* （啟動器）為您提供了實用的筆記本模板，用於支援的內核，可幫助您啟動任務，包括：

| 範本 | 說明 |
| --- | --- |
| 空白 | 空的筆記本檔案。 |
| 入門者 | 預填充的筆記型電腦演示使用樣本資料進行資料探索。 |
| 零售銷售 | 預裝的筆記型電腦採用 [樣本資料](https://adobe.ly/2wOgO3L) ，提供零售配方。 |
| 方式產生器 | 在中建立配方的筆記本模板 [!DNL JupyterLab]。 它預先填入程式碼和評註，以示範並說明方式建立程式。 請參閱筆記 [本至配方教學課程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) ，以取得詳細的逐步說明。 |
| [!DNL Query Service] | 預先填入的筆記型電腦，可直接在提供的范 [!DNL Query Service] 例工作流程 [!DNL JupyterLab] 中展示其使用方式，可進行大規模資料分析。 |
| XDM事件 | 預先填入的筆記型電腦，展示後值Experience Event資料的資料探索，著重於資料結構中常見的功能。 |
| XDM查詢 | 預先填入的筆記型電腦，展示Experience Event資料的範例商業查詢。 |
| 彙總 | 預先填充的筆記本演示了將大量資料匯總到較小、可管理的塊中的示例工作流。 |
| 集群 | 預填充的筆記型電腦，演示使用群集算法的端到端機器學習建模過程。 |

某些筆記型電腦模板僅限於某些內核。 每個內核的模板可用性在下表中映射：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>入門者</strong></th>
        <th><strong>零售銷售</strong></th>
        <th><strong>方式產生器</strong></th>
        <th><strong>[!DNL查詢服務]</strong></th>
        <th><strong>XDM事件</strong></th>
        <th><strong>XDM查詢</strong></th>
        <th><strong>彙總</strong></th>
        <th><strong>集群</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3([!DNL Spark] 2.4)</strong></th>
        <td >no</td>
        <td >是</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >是</td>
        <td >是</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>斯卡拉</strong></th>
        <td >是</td>
        <td >是</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >是</td>
    </tr>
</table>

若要開啟新的啟動 *器*，請按一 **下「檔案>新增啟動器」**。 或者，從左側邊 **欄展開** 「檔案」瀏覽器，然後按一下加號(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

### [!DNL Python]/R中的GPU和記憶體伺服器配置

在 [!DNL JupyterLab] 中，選擇右上角的齒輪表徵圖以開啟「筆記本」( *Notebook)伺服器配置*。 您可以使用滑桿來切換GPU並分配所需的記憶體量。 可分配的記憶體量取決於您的組織已布建的記憶體量。 選擇 **[!UICONTROL 更新要保存]** 的配置。

>[!NOTE]
>
>每個組織只為筆記型電腦配置一個GPU。 如果GPU正在使用中，您需要等待目前已保留GPU的使用者釋放它。 若要這麼做，請登出或讓GPU處於閒置狀態達4小時以上。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## 後續步驟

若要進一步瞭解每個支援的筆記型電腦以及如何使用它們，請造訪 [Jupyterlab筆記型電腦資料存取開發人員指南](./access-notebook-data.md) 。 本指南著重說明如何使用JupyterLab筆記型電腦存取您的資料，包括讀取、寫入和查詢資料。 資料存取指南還包含每個支援的筆記型電腦可以讀取的最大資料量的資訊。

## 支援的程式庫 {#supported-libraries}

### [!DNL Python] / R

| 資料庫 | 版本 |
| :------ | :------ |
| 筆記本 | 6.0.0 |
| 請求 | 2.22.0 |
| 隱晦 | 4.0.0 |
| 青葉 | 0.10.0 |
| ipywidget | 7.5.1 |
| bokeh | 1.3.1 |
| gensim | 3.7.3 |
| ipyparallel | 0.5.2 |
| jq | 1.6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| 熊貓 | 0.22.0 |
| 潘達斯 | 0.7.3 |
| 枕 | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| 接骨 | 1.3.0 |
| 發癢 | 1.3.0 |
| 西伯恩 | 0.9.0 |
| statmodels | 0.10.1 |
| 彈性 | 5.1.0.17 |
| gplot | 0.11.5 |
| py-xgboost | 0.90 |
| opencv | 3.4.1 |
| 皮什帕克 | 2.4.3 |
| 火炬 | 1.0.1 |
| wxpython | 4.0.6 |
| colorlover | 0.3.0 |
| geopandas | 0.5.1 |
| 地源 | 2.1.0 |
| 風格 | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3.6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-ggthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-lapes | 3.0 |
| r-操縱 | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-存活 | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r弦長 | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-forecast | 8.7 |
| r-rsolnp | 1.16 |
| r-網狀 | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corplot | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-隨機森林 | 4.6_14 |
| 逆向 | 1.2.1 |
| r樹 | 1.0_39 |
| 皮蒙戈 | 3.8.0 |
| pyarrow | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fast鑲木地板 | 0.3.2 |
| python-snappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure儲存 | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| 熊貓-ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| 模擬 | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| 鼻子 | 1.3.7 |
| autovizwidget | 0.12.9 |
| 阿爾塔 | 3.1.0 |
| vega_datasets | 0.7.0 |
| 平磨機 | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimporter | 0.3.1 |

### PySpark

| 資料庫 | 版本 |
| :------ | :------ |
| 請求 | 2.18.4 |
| gensim | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| 熊貓 | 0.20.1 |
| 潘達斯 | 0.7.3 |
| 枕 | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| 接骨 | 0.19.1 |
| 發癢 | 1.3.3 |
| statmodels | 0.8.0 |
| 彈性 | 4.0.30.44 |
| py-xgboost | 0.60 |
| opencv | 3.1.0 |
| pyarrow | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |