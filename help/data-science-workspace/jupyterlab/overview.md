---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: JupyterLab使用指南
topic: Overview
description: JupyterLab是Project Jupyter的網路使用者介面，並與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與Jupyter筆記型電腦、程式碼和資料搭配使用。
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 11%

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
* [PySpark/Spark執行資源](#execution-resource)
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
| 零售銷售 | 預先填入的筆記型電腦，使用 <a href="https://adobe.ly/2wOgO3L" target="_blank">範例資料</a> ，提供零售銷售方式。 |
| 方式產生器 | 在中建立配方的筆記本模板 [!DNL JupyterLab]。 它預先填入程式碼和評註，以示範並說明方式建立程式。 請參閱筆記 <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">本至配方教學課程</a> ，以取得詳細的逐步說明。 |
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
>每個組織只為筆記型電腦配置一個GPU。 如果GPU正在使用中，您需要等待目前已保留GPU的使用者釋放它。 若要這麼做，請登出或讓GPU處於閒置狀態達4小時以上。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## 使用筆 [!DNL Platform] 記本訪問資料

每個支援的內核都提供內置功能，允許您從筆記本 [!DNL Platform] 中的資料集讀取資料。 但是，對分頁資料的支援僅限於 [!DNL Python] 和R筆記本。

### 筆記型電腦資料限制

以下資訊定義可讀取的資料量上限、使用的資料類型，以及讀取資料所花費的估計時間範圍。 對於 [!DNL Python] 和R ，使用配置為40GB RAM的筆記型電腦伺服器作為基準。 對於PySpark和Scala，以下概述的基準使用了以64GB RAM、8個內核、2個DBU（最多4個工作人員）配置的資料庫群集。

使用的ExperienceEvent架構資料的大小不同，從1000(1K)列開始，最多可達10億(1B)列。 請注意，對於PySpark和 [!DNL Spark] 度量，XDM資料的日期範圍是10天。

臨機架構資料是使用「以選取方式建立表 [!DNL Query Service] 格」(CTAS)預先處理。 這些資料的大小也從1,000列(1K)開始，最多10億列(1B)。

#### [!DNL Python] 筆記型資料限制

**XDM ExperienceEvent架構：** 在不到22分鐘內，您最多可以讀取200萬行（磁碟上約6.1 GB的資料）的XDM資料。 新增其他列可能會導致錯誤。

| 行數 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK（以秒為單位） | 20.3 | 86.8 | 63 | 659 | 1315 |

**臨機架構：** 在不到14分鐘內，您最多可讀取500萬行（磁碟上約5.6 GB資料）的非XDM（臨機）資料。 新增其他列可能會導致錯誤。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁碟大小(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（以秒為單位） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### R筆記本資料限制

**XDM ExperienceEvent架構：** 在13分鐘內，您最多可讀取100萬行XDM資料（磁碟上的3GB資料）。

| 行數 | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 |
| R內核（以秒為單位） | 14.03 | 69.6 | 86.8 | 775 |

**臨機架構：** 您應能在大約10分鐘內讀取最多300萬列的臨機資料（293MB的磁碟資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁碟大小(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK（秒） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### PySpark(內核[!DNL Python] )筆記型電腦資料限制：

**XDM ExperienceEvent架構：** 在交互模式下，您應該能夠在大約20分鐘內讀取XDM資料的最多500萬行（磁碟上約13.42GB的資料）。 互動模式僅支援多達5百萬列。 如果您想要讀取較大的資料集，建議您切換到批處理模式。 在「批處理」模式下，您應能在大約14小時內讀取XDM資料的最多5億行（磁碟上約1.31TB資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK（互動模式） | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK（批次模式） | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**臨機架構：** 在互動模式下，您最多可在3分鐘內讀取10億行（磁碟上約1.05TB資料）的非XDM資料。 在批處理模式下，您應能在大約18分鐘內讀取非XDM資料的10億行（磁碟上約1.05TB資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁碟大小 | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK互動模式（以秒為單位） | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| SDK批次模式（以秒為單位） | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### [!DNL Spark] （Scala內核）筆記本資料限制：

**XDM ExperienceEvent架構：** 在交互模式下，您應該能夠在大約18分鐘內讀取XDM資料的最多500萬行（磁碟上的資料約13.42GB）。 互動模式僅支援多達5百萬列。 如果您想要讀取較大的資料集，建議您切換到批處理模式。 在「批處理」模式下，您應能在大約14小時內讀取XDM資料的最多5億行（磁碟上約1.31TB資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK互動模式（以秒為單位） | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK批次模式（以秒為單位） | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**臨機架構：** 在互動模式下，您最多可在3分鐘內讀取10億行（磁碟上約1.05TB資料）的非XDM資料。 在批處理模式下，您應能在大約16分鐘內讀取非XDM資料的10億行（磁碟上約1.05TB資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁碟大小 | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK互動模式（以秒為單位） | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| SDK批次模式（以秒為單位） | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### 在 [!DNL Python]/R中讀取資料集

[!DNL Python] 和R筆記型電腦允許您在訪問資料集時分頁資料。 下面顯示有分頁和無分頁讀取資料的范常式式碼。

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### 在 [!DNL Python]/R中從資料集讀取，不需編頁

執行下列程式碼會讀取整個資料集。 如果執行成功，則資料將保存為變數引用的Apcotis資料幀 `df`。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`:要訪問的資料集的唯一標識

#### 在 [!DNL Python]/R中從資料集讀取並分頁

執行下列程式碼會讀取指定資料集的資料。 分頁是通過分別通過函式和函式限制和偏移資料 `limit()` 來實現 `offset()` 的。 限制資料是指要讀取的資料點數上限，而偏移指在讀取資料之前要跳過的資料點數。 如果讀取操作成功執行，則資料將被保存為變數引用的Apcotis資料幀 `df`。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`:要訪問的資料集的唯一標識

### 從PySpark/[!DNL Spark]/Scala的資料集讀取

在開啟作用中的PySpark或Scala筆記型電腦後，從左側邊欄展開 **Data Explorer** （資料總管）標籤，然後按兩下 **Datasets** （資料集）以檢視可用資料集清單。 按一下右鍵要訪問的資料集清單，然後按一下「 **Explore Data in Notebook(在筆記本中瀏覽資料**)」。 產生下列程式碼儲存格：

#### PySpark([!DNL Spark] 2.4) {#pyspark2.4}

隨著Spark 2.4的推出，自訂功能 [`%dataset`](#magic) 也隨之提供。

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala([!DNL Spark] 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>在Scala中，可以使 `sys.env()` 用在中聲明和返回值 `option`。

### 在PySpark 3([!DNL Spark] 2.4)筆記型電腦中使用%dataset魔術 {#magic}

隨著 [!DNL Spark] 2.4的推出， `%dataset` 為新的PySpark 3([!DNL Spark] 2.4)筆記型電腦([!DNL Python] 3內核)提供了定制功能。

**使用狀況**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**說明**

用於 [!DNL Data Science Workspace] 從筆記本( [!DNL Python] 3內核)讀取或寫入資料集的自定[!DNL Python] 義魔術命令。

* **{action}**:要在資料集上執行的動作類型。 有兩個動作是「讀取」或「寫入」。
* **—datasetId {id}**:用於提供要讀取或寫入的資料集的ID。 這是必要的引數。
* **—dataFrame {df}**:熊貓資料框。 這是必要的引數。
   * 當動作為&quot;read&quot;時，{df}是資料集讀取作業結果可用的變數。
   * 當動作為&quot;write&quot;時，此資料幀{df}將寫入資料集。
* **—mode（可選）**:允許的參數為「批次」和「互動」。 依預設，模式會設為「互動」。 建議在讀取大量資料時使用「批次」模式。

**範例**

* **閱讀範例**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **寫示例**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### 查詢資料使 [!DNL Query Service] 用 [!DNL Python]

[!DNL JupyterLab] on可 [!DNL Platform] 讓您在筆記型電腦中使 [!DNL Python] 用SQL透過 <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">Adobe Experience Platform Query Service存取資料</a>。 由於資料的運 [!DNL Query Service] 行時間優越，通過訪問資料對處理大型資料集非常有用。 請注意，使用查詢 [!DNL Query Service] 資料的處理時間限制為10分鐘。

在中使 [!DNL Query Service] 用 [!DNL JupyterLab]之前，請確定您對 <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">[!DNL Query Service] SQL語法有正確的理解</a>。

使用查詢 [!DNL Query Service] 資料需要提供目標資料集的名稱。 您可以使用「資料總管」來尋找所需的資料集，以產生必要的 **程式碼儲存格**。 按一下右鍵資料集清單，然後按一下「 **Notebook（筆記本）」中的** 「Query Data（查詢資料）」 ，在筆記本中生成以下兩個代碼單元格：


為了在中使 [!DNL Query Service] 用， [!DNL JupyterLab]您必須首先在工作筆記本和之間建立 [!DNL Python] 連接 [!DNL Query Service]。 這可以通過執行第一生成單元來實現。

```python
qs_connect()
```

在第二個生成的單元格中，第一行必須在SQL查詢之前定義。 預設情況下，生成的單元格定義一個可選變數(`df0`)，該變數將查詢結果保存為Pactices資料幀。 <br>該 `-c QS_CONNECTION` 參數是強制的，它指示內核執行SQL查詢 [!DNL Query Service]。 有關其 [他引數的清單](#optional-sql-flags-for-query-service) ，請參見附錄。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python變數可在SQL查詢中直接引用，方法是使用字串格式語法，並將變數包住大括弧(`{}`)，如下列範例所示：

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### 在 [!DNL Python]/R中篩選ExperienceEvent資料

若要存取及篩選筆記型電腦或 [!DNL Python] R筆記型電腦中的ExperienceEvent資料集，您必須提供資料集的ID(`{DATASET_ID}`)，以及使用邏輯運算子定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考慮整個資料集。

篩選運算子的清單說明如下：

* `eq()`: Equal to
* `gt()`: Greater than
* `ge()`: Greater than or equal to
* `lt()`: Less than
* `le()`: Less than or equal to
* `And()`:邏輯AND運算子
* `Or()`:邏輯OR運算子

以下儲存格會將ExperienceEvent資料集篩選為2019年1月1日至2019年12月31日止期間僅存在的資料。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### 在PySpark/中篩選ExperienceEvent資料[!DNL Spark]

在PySpark或Scala筆記型電腦中存取和篩選ExperienceEvent資料集時，您必須提供資料集識別(`{DATASET_ID}`)、組織的IMS識別，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式定義的，其 `spark.sql()`中函式參數是SQL查詢字串。

以下儲存格會將ExperienceEvent資料集篩選為2019年1月1日至2019年12月31日止期間僅存在的資料。

#### PySpark 3([!DNL Spark] 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Scala([!DNL Spark] 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>
>
>在Scala中，可以使 `sys.env()` 用在中聲明和返回值 `option`。 如此，若您知道變數只會在單次使用，就不需要定義變數。 以下示例從 `val userToken` 上述示例中取得，並聲明它為 `option` 替代項：
>
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

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
| kit | 4.0.30.44 |
| py-xgboost | 0.60 |
| 彈性 | 3.1.0 |
| pyarrow | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |

## 可選的SQL標誌 [!DNL Query Service] {#optional-sql-flags-for-query-service}

此表概述了可用於的可選SQL標誌 [!DNL Query Service]。

| **旗標** | **說明** |
| --- | --- |
| `-h`, `--help` | 顯示幫助消息並退出。 |
| `-n`, `--notify` | 切換選項以通知查詢結果。 |
| `-a`, `--async` | 使用此標誌可非同步執行查詢，並可在查詢執行時釋放內核。 在將查詢結果指派給變數時請務必小心，因為如果查詢未完成，變數可能未定義。 |
| `-d`, `--display` | 使用此標幟可防止顯示結果。 |

