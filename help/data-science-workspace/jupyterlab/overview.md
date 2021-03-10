---
keywords: Experience Platform;JupyterLab；筆記型電腦；資料科學工作區；熱門主題；jupyterlab
solution: Experience Platform
title: JupyterLab UI概觀
topic: 概述
description: JupyterLab是Project Jupyter的基於Web的用戶介面，與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與Jupyter Notebooks、程式碼和資料搭配使用。 本文檔概述了JupyterLab及其功能，以及執行常見操作的說明。
translation-type: tm+mt
source-git-commit: 23128fb481452b558c52f962f78ae638fc1f0418
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 3%

---


# [!DNL JupyterLab] UI概觀

[!DNL JupyterLab] 是Project  [Jupyter的Web使用者介面，並](https://jupyter.org/) 與Adobe Experience Platform緊密整合。它為資料科學家提供互動式開發環境，以便與Jupyter Notebooks、程式碼和資料搭配使用。

本檔案概述[!DNL JupyterLab]及其功能，以及執行常見動作的指示。

## [!DNL JupyterLab] on  [!DNL Experience Platform]

Experience Platform公司的JupyterLab整合附帶了體系結構更改、設計考慮、定製的筆記本擴展、預安裝的庫和Adobe主題介面。

下列清單概述JupyterLab在Platform上獨有的一些功能：

| 功能 | 說明 |
| --- | --- |
| **內核** | 內核提供筆記型電腦和其他[!DNL JupyterLab]前端，以不同的寫程式語言執行和查看代碼。 [!DNL Experience Platform] 提供額外的內核，以支 [!DNL Python]援R、PySpark和的開發 [!DNL Spark]。有關詳細資訊，請參閱[kernels](#kernels)部分。 |
| **資料存取** | 直接從[!DNL JupyterLab]中訪問現有資料集，並完全支援讀寫功能。 |
| **[!DNL Platform]服務整合** | 內建整合可讓您直接從[!DNL JupyterLab]內運用其他[!DNL Platform]服務。 [與其他平台服務](#service-integration)整合一節提供支援整合的完整清單。 |
| **驗證** | 除了<a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab的內建安全模型</a>外，您的應用程式與Experience Platform之間的每次互動，包括平台服務對服務通訊，都會透過<a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System](IMS)</a>進行加密和驗證。 |
| **開發程式庫** | 在[!DNL Experience Platform]中，[!DNL JupyterLab]提供了[!DNL Python]、R和PySpark的預安裝庫。 有關支援庫的完整清單，請參見[附錄](#supported-libraries)。 |
| **程式庫控制器** | 當預先安裝的程式庫不符合您的需求時，可為Python和R安裝其他程式庫，並暫時儲存在隔離的容器中，以維持[!DNL Platform]的完整性並保有資料的安全。 有關詳細資訊，請參閱[kernels](#kernels)部分。 |

>[!NOTE]
>
>其他程式庫僅適用於安裝程式庫的作業階段。 啟動新會話時，必須重新安裝所需的任何其他庫。

## 與其他[!DNL Platform]服務{#service-integration}整合

標準化和互操作性是[!DNL Experience Platform]背後的關鍵概念。 將[!DNL Platform]上的[!DNL JupyterLab]整合為內嵌IDE，可讓它與其他[!DNL Platform]服務互動，讓您充份運用[!DNL Platform]。 [!DNL JupyterLab]提供以下[!DNL Platform]服務：

* **[!DNL Catalog Service]：訪** 問和探索具有讀寫功能的資料集。
* **[!DNL Query Service]：使** 用SQL訪問和瀏覽資料集，在處理大量資料時提供較低的資料存取開銷。
* **[!DNL Sensei ML Framework]：可** 以訓練和分數資料的模型開發，以及只需按一下即可建立方式。
* **[!DNL Experience Data Model (XDM)]：標** 準化和互操作性是Adobe Experience Platform背後的關鍵概念。[Experience Data Model(XDM)](https://www.adobe.com/go/xdm-home-en)，由Adobe驅動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

>[!NOTE]
>
>[!DNL JupyterLab]上的某些[!DNL Platform]服務整合僅限於特定內核。 有關詳細資訊，請參閱[kernels](#kernels)上的一節。

## 主要功能與常用作業

有關[!DNL JupyterLab]的主要功能和執行常見操作的說明的資訊，請參見以下各節：

* [存取JupyterLab](#access-jupyterlab)
* [JupyterLab介面](#jupyterlab-interface)
* [程式碼儲存格](#code-cells)
* [內核](#kernels)
* [內核會話](#kernel-sessions)
* [啟動程式](#launcher)

### 存取 [!DNL JupyterLab] {#access-jupyterlab}

在[Adobe Experience Platform](https://platform.adobe.com)中，從左側導航列中選擇&#x200B;**[!UICONTROL Notebooks]**。 請讓[!DNL JupyterLab]稍候完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 介面 {#jupyterlab-interface}

[!DNL JupyterLab]介麵包含功能表列、可折疊的左側邊欄，以及包含檔案和活動標籤的主要工作區。

**選單列**

介面頂部的菜單欄具有頂級菜單，這些菜單使用鍵盤快捷鍵顯示[!DNL JupyterLab]中的可用操作：

* **檔案：與** 檔案和目錄相關的操作
* **編輯：與編** 輯文檔和其他活動相關的操作
* **檢視：** 改變外觀的動作  [!DNL JupyterLab]
* **Run：在不** 同活動（例如筆記型電腦和程式碼主控台）中執行程式碼的動作
* **內核：用** 於管理內核的操作
* **頁籤：** 開啟的文檔和活動的清單
* **設定：常** 用設定和進階設定編輯器
* **幫助：** 和內核幫 [!DNL JupyterLab] 助連結清單

**左側欄**

左側邊欄包含可點選的標籤，可存取下列功能：

* **檔案瀏覽器：** 已保存的筆記本文檔和目錄清單
* **資料總管：** 瀏覽、存取和探索資料集和結構
* **運行內核和終端：** 具有終止能力的活動內核和終端會話清單
* **命令：** 有用命令的清單
* **儲存格檢視** 器：儲存格編輯器，可存取工具和中繼資料，以用於設定筆記型電腦以進行簡報
* **頁籤：** 開啟的頁籤清單

選取要公開其功能的標籤，或在展開的標籤上選取以收合左側邊欄，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作區**

[!DNL JupyterLab]中的主要工作區域可讓您將檔案和其他活動排列成標籤面板，這些標籤可以調整大小或細分。 將標籤拖曳至標籤面板的中央，以移轉標籤。 將標籤拖曳至面板的左、右、上或下方，以劃分面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### [!DNL Python]/R中的GPU和記憶體伺服器配置

在[!DNL JupyterLab]中，選擇右上角的齒輪表徵圖以開啟&#x200B;*筆記本伺服器配置*。 您可以使用滑桿來切換GPU並分配所需的記憶體量。 可分配的記憶體量取決於您的組織已布建的記憶體量。 選擇&#x200B;**[!UICONTROL 更新配置]**&#x200B;以保存。

>[!NOTE]
>
>每個組織只為筆記型電腦配置一個GPU。 如果GPU正在使用中，您需要等待目前已保留GPU的使用者釋放它。 若要這麼做，請登出或讓GPU處於閒置狀態達4小時以上。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 終止並重新啟動[!DNL JupyterLab]

在[!DNL JupyterLab]中，您可以終止會話，以防止使用其他資源。 從選擇&#x200B;**電源表徵圖**&#x200B;開始，然後從顯示為終止會話的快顯窗口中選擇&#x200B;**[!UICONTROL 關閉]**。 筆記型電腦會話在12小時無活動後自動終止。

要重新啟動[!DNL JupyterLab]，請選擇位於電源表徵圖左側的&#x200B;**重新啟動表徵圖**，然後從顯示的快顯窗口中選擇&#x200B;**[!UICONTROL 重新啟動]**。

![終止jupterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 代碼單元格{#code-cells}

代碼單元格是筆記型電腦的主要內容。 它們包含的原始碼為筆記型電腦相關內核的語言，以及執行代碼單元格後的輸出。 每個代碼單元格的右側顯示一個執行計數，該代碼單元格表示其執行順序。

![](../images/jupyterlab/user-guide/code_cell.png)

常見的儲存格動作說明如下：

* **添加單元格：** 從筆記本菜單中按一下加號(**+**)可添加空單元格。新儲存格會置於目前正在互動的儲存格下方，或在筆記型電腦的結尾處（如果沒有特定儲存格在焦點中）。

* **移動單元格：將** 游標置於要移動的單元格的右側，然後按一下並將單元格拖動到新位置。此外，將一個單元格從一個筆記本移動到另一個筆記本會複製該單元格及其內容。

* **執行儲存格：** 按一下您要執行之儲存格的內文，然後從筆記型電腦選單 **** 按一▶下播放圖示(****)。當內核處理執行時，在單元格的執行計數器中顯示星號(**\***)，並在完成時被整數替換。

* **刪除儲存格：** 按一下您要刪除之儲存格的內文，然後按一下剪 **** 式圖示。

### 內核{#kernels}

筆記型電腦內核是用於處理筆記型電腦單元的語言專用計算引擎。 除了[!DNL Python]外，[!DNL JupyterLab]還提供R、PySpark和[!DNL Spark](Scala)中的其他語言支援。 開啟筆記本文檔時，將啟動關聯內核。 當執行筆記本單元時，內核執行計算並產生可能消耗大量CPU和記憶體資源的結果。 請注意，在內核關閉之前，不會釋放已分配的記憶體。

某些特性和功能限於下表所述的特定內核：

| 內核 | 資料庫安裝支援 | [!DNL Platform] 整合 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 無 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 內核會話{#kernel-sessions}

[!DNL JupyterLab]上的每個活動筆記本或活動都使用內核會話。 通過從左側邊欄展開&#x200B;**運行終端和內核**&#x200B;頁籤，可以找到所有活動會話。 通過觀察筆記本介面的右上角，可以確定筆記本內核的類型和狀態。 在下圖中，筆記本的關聯內核為&#x200B;**[!DNL Python]3** ，其當前狀態由右側的灰色圓表示。 空心圓表示空閒內核，實心圓表示忙碌內核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果內核長時間處於關閉或非活動狀態，則&#x200B;**無內核！** 顯示實心圓。通過按一下內核狀態並選擇相應的內核類型激活內核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 啟動器{#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定義的&#x200B;*Launcher*&#x200B;為支援的內核提供了實用的筆記本模板，可幫助您啟動任務，包括：

| 範本 | 說明 |
| --- | --- |
| 空白 | 空的筆記本檔案。 |
| 入門者 | 預填充的筆記型電腦演示使用樣本資料進行資料探索。 |
| 零售銷售 | 一種預填充的筆記型電腦，其特徵是使用樣本資料使[零售銷售方式](https://adobe.ly/2wOgO3L)。 |
| 方式產生器 | 用於在[!DNL JupyterLab]中建立配方的筆記本模板。 它預先填入程式碼和評註，以示範並說明方式建立程式。 請參閱[筆記型電腦至配方教程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en)以取得詳細的逐步說明。 |
| [!DNL Query Service] | 預填充的筆記本直接在[!DNL JupyterLab]中演示[!DNL Query Service]的使用情況，並提供了可大規模分析資料的示例工作流。 |
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

要開啟新的&#x200B;*Launcher*，請按一下&#x200B;**「檔案」>「新建啟動程式」**。 或者，從左側邊欄展開&#x200B;**檔案瀏覽器**，然後按一下加號(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 後續步驟

若要進一步瞭解每個受支援的筆記型電腦以及如何使用它們，請造訪[Jupyterlab筆記型電腦資料存取](./access-notebook-data.md)開發人員指南。 本指南著重說明如何使用JupyterLab筆記型電腦存取您的資料，包括讀取、寫入和查詢資料。 資料存取指南還包含每個支援的筆記型電腦可以讀取的最大資料量的資訊。

## 支援的程式庫{#supported-libraries}

如需Python、R和PySpark中支援的套件清單，請複製並貼入新儲存格中的`!pip list --format=columns`，然後執行儲存格。 支援的包清單按字母順序填充。

![示例](../images/jupyterlab/user-guide/libraries.PNG)