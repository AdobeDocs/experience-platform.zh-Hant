---
keywords: Experience Platform;JupyterLab；筆記型電腦；Data Science Workspace；熱門主題；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
topic-legacy: Overview
description: JupyterLab是Project Jupyter的基於Web的用戶介面，並緊密整合到Adobe Experience Platform中。 它為資料科學家提供互動式開發環境，以便與Jupyter Notebooks、代碼和資料協作。 本檔案概述JupyterLab及其功能，以及執行常見動作的指示。
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 91003bf142008bcb1277269b45d8a55234ea6564
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 3%

---

# [!DNL JupyterLab] UI概述

[!DNL JupyterLab] 是專案Jupyter的網頁型使用者介 [面，](https://jupyter.org/) 並緊密整合至Adobe Experience Platform。它為資料科學家提供互動式開發環境，以便與Jupyter Notebooks、代碼和資料協作。

本檔案概述[!DNL JupyterLab]及其功能，以及執行常見動作的指示。

## [!DNL JupyterLab] on  [!DNL Experience Platform]

Experience Platform的JupyterLab整合附帶了架構變更、設計考量、自訂的筆記型電腦擴充功能、預先安裝的程式庫，以及Adobe主題介面。

下列清單概述JupyterLab在Platform上獨有的部分功能：

| 功能 | 說明 |
| --- | --- |
| **內核** | 內核提供筆記本和其他[!DNL JupyterLab]前端，以不同的寫程式語言執行和查看代碼的能力。 [!DNL Experience Platform] 提供額外的內核，以支 [!DNL Python]援在、 R、 PySpark和中的開 [!DNL Spark]發。有關詳細資訊，請參閱[kernels](#kernels)部分。 |
| **資料存取** | 直接從[!DNL JupyterLab]中存取現有資料集，並完全支援讀取和寫入功能。 |
| **[!DNL Platform]服務整合** | 內建整合可讓您直接從[!DNL JupyterLab]中利用其他[!DNL Platform]服務。 [與其他平台服務整合](#service-integration)的區段中提供完整的支援整合清單。 |
| **驗證** | 除了<a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab的內建安全模型</a>外，您的應用程式與Experience Platform（包括平台服務對服務通信）之間的每次交互都通過<a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System](IMS)</a>加密和驗證。 |
| **開發程式庫** | 在[!DNL Experience Platform]中，[!DNL JupyterLab]提供預先安裝的[!DNL Python]、R和PySpark的庫。 如需支援程式庫的完整清單，請參閱[附錄](#supported-libraries)。 |
| **程式庫控制器** | 當預安裝的庫缺少滿足您的需要時，可以為Python和R安裝其他庫，並臨時儲存在隔離的容器中，以保持[!DNL Platform]的完整性並保證資料的安全。 有關詳細資訊，請參閱[kernels](#kernels)部分。 |

>[!NOTE]
>
>其他程式庫僅適用於安裝程式庫的工作階段。 啟動新會話時，必須重新安裝需要的任何其他庫。

## 與其他[!DNL Platform]服務整合 {#service-integration}

標準化和互操作性是[!DNL Experience Platform]背後的重要概念。 將[!DNL Platform]上的[!DNL JupyterLab]整合為嵌入式IDE，使其能夠與其他[!DNL Platform]服務交互，從而使您能夠充分利用[!DNL Platform]的潛能。 [!DNL JupyterLab]中提供以下[!DNL Platform]服務：

* **[!DNL Catalog Service]:** 使用讀取和寫入功能存取和探索資料集。
* **[!DNL Query Service]:** 使用SQL存取和探索資料集，在處理大量資料時提供較低的資料存取開銷。
* **[!DNL Sensei ML Framework]:** 能夠訓練及計分資料的模型開發，以及只需按一下即可建立方式。
* **[!DNL Experience Data Model (XDM)]:** 標準化和互操作性是Adobe Experience Platform背後的重要概念。[由Adobe驅動的Experience Data Model(XDM)](https://www.adobe.com/go/xdm-home-en)，可讓客戶體驗資料標準化，並定義客戶體驗管理的結構。

>[!NOTE]
>
>[!DNL JupyterLab]上的某些[!DNL Platform]服務整合僅限於特定內核。 有關詳細資訊，請參閱[kernels](#kernels)上的部分。

## 主要功能和常見操作

有關[!DNL JupyterLab]的主要功能以及執行常見操作的說明的資訊，請參見以下各節：

* [訪問JupyterLab](#access-jupyterlab)
* [JupyterLab介面](#jupyterlab-interface)
* [程式碼儲存格](#code-cells)
* [內核](#kernels)
* [內核會話](#kernel-sessions)
* [啟動器](#launcher)

### 存取 [!DNL JupyterLab] {#access-jupyterlab}

在[Adobe Experience Platform](https://platform.adobe.com)中，從左側導航列中選擇&#x200B;**[!UICONTROL Notebooks]**。 請允許一些時間讓[!DNL JupyterLab]完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 介面 {#jupyterlab-interface}

[!DNL JupyterLab]介面由菜單欄、可折疊的左側邊欄和包含文檔和活動頁簽的主要工作區組成。

**功能表列**

介面頂部的菜單欄具有頂級菜單，這些菜單顯示[!DNL JupyterLab]中可用的操作及其鍵盤快捷鍵：

* **檔案：** 與檔案和目錄相關的動作
* **編輯：** 與編輯檔案和其他活動相關的動作
* **檢視：** 會改變外觀的動作  [!DNL JupyterLab]
* **執行：** 在不同活動（例如筆記型電腦和程式碼主控台）中執行程式碼的動作
* **內核：** 用於管理內核的操作
* **索引標籤：** 已開啟的檔案和活動的清單
* **設定：** 常見設定和進階設定編輯器
* **幫助：** 和內核幫 [!DNL JupyterLab] 助連結的清單

**左側欄**

左側邊欄包含可點按的標籤，這些標籤提供對以下功能的訪問：

* **檔案瀏覽器：** 已保存的筆記本文檔和目錄的清單
* **資料總管：** 瀏覽、存取及探索資料集和結構
* **運行內核和終端：** 可終止的活動內核和終端會話的清單
* **命令：** 有用命令的清單
* **單元檢查器：** 一種單元編輯器，提供對工具和元資料的訪問，這些工具和元資料可用於設定筆記本以用於演示
* **頁簽：** 已開啟頁簽的清單

選取標籤以公開其功能，或選取展開的標籤以折疊左側邊欄，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作區**

[!DNL JupyterLab]中的主要工作區可讓您將文檔和其他活動排列成可調整大小或細分的頁簽面板。 將標籤拖曳至標籤面板的中央，以移轉標籤。 將標籤拖曳至面板的左、右、上或底部，以分割面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### [!DNL Python]/R中的GPU和記憶體伺服器配置

在[!DNL JupyterLab]中，選擇右上角的齒輪表徵圖以開啟&#x200B;*筆記本伺服器配置*。 您可以使用滑塊開啟GPU並分配所需的記憶體量。 您可分配的記憶體量取決於貴組織已布建的記憶體量。 選擇&#x200B;**[!UICONTROL 更新配置]**&#x200B;以保存。

>[!NOTE]
>
>每個組織只為筆記型電腦配置一個GPU。 如果GPU正在使用中，則需要等待當前已保留GPU的用戶釋放它。 這可以通過註銷或將GPU保持空閒狀態達四小時或更長時間來完成。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 終止並重新啟動[!DNL JupyterLab]

在[!DNL JupyterLab]中，您可以終止會話以防止使用更多資源。 首先，選擇&#x200B;**電源表徵圖** ![電源表徵圖](../images/jupyterlab/user-guide/power_button.png)，然後從彈出窗口中選擇&#x200B;**[!UICONTROL 關閉]**&#x200B;以終止您的會話。 筆記型電腦會話在12小時無活動後自動終止。

若要重新啟動[!DNL JupyterLab]，請選擇直接位於電源表徵圖左側的&#x200B;**重新啟動表徵圖** ![重新啟動表徵圖](../images/jupyterlab/user-guide/restart_button.png)，然後從顯示的彈出窗口中選擇&#x200B;**[!UICONTROL 重新啟動]**。

![終止jupterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 程式碼儲存格 {#code-cells}

代碼單元格是筆記本的主要內容。 它們包含以筆記本關聯內核的語言和作為執行代碼單元的結果的輸出的原始碼。 每個代碼儲存格的右側會顯示執行計數，代表其執行順序。

![](../images/jupyterlab/user-guide/code_cell.png)

常見儲存格動作說明如下：

* **添加單元格：** 按一下筆記本菜單中的加號(**+**)以添加空單元格。新單元格將放置在當前正在進行交互的單元格下，或者如果沒有特定單元格處於焦點，則放置在筆記本的末尾。

* **移動儲存格：** 將游標置於您要移動的儲存格右側，然後按一下並拖曳儲存格至新位置。此外，將單元格從一個筆記本移動到另一個筆記本將複製單元格及其內容。

* **執行儲存格：** 按一下您要執行之儲存格的內文，然後按一下筆記 **** 本功能表中的播放圖示(**▶**)。當內核處理執行時，儲存格的執行計數器中會顯示星號(**\***)，並在完成時以整數取代。

* **刪除儲存格：** 按一下您要刪除之儲存格的本文，然後按一下剪 **** 式圖示。

### 內核 {#kernels}

筆記型電腦內核是用於處理筆記型電腦單元的語言專用計算引擎。 除了[!DNL Python]外，[!DNL JupyterLab]還在R、PySpark和[!DNL Spark](Scala)中提供其他語言支援。 開啟筆記本文檔時，將啟動關聯的內核。 當執行筆記型電腦單元時，內核執行計算並產生可能消耗大量CPU和記憶體資源的結果。 請注意，在關閉內核之前不會釋放已分配的記憶體。

如下表所述，某些特徵和功能僅限於特定內核：

| 內核 | 程式庫安裝支援 | [!DNL Platform] 整合 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 無 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 內核會話 {#kernel-sessions}

[!DNL JupyterLab]上的每個活動筆記本或活動都使用內核會話。 從左側邊欄展開&#x200B;**運行終端和內核**&#x200B;頁簽，可找到所有活動會話。 通過觀察筆記本介面的右上角，可以識別筆記本的內核的類型和狀態。 在下圖中，筆記本的關聯內核為&#x200B;**[!DNL Python]3**，其當前狀態由右側的灰色圓表示。 空心圓表示空閒內核，實心圓表示繁忙內核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果內核長時間處於關閉狀態或非活動狀態，則&#x200B;**無內核！** 顯示實心圓。通過按一下內核狀態並選擇相應的內核類型來激活內核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 啟動器 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定義的&#x200B;*啟動器*&#x200B;為支援的內核提供了有用的筆記本模板，以幫助您啟動任務，包括：

| 範本 | 說明 |
| --- | --- |
| 空白 | 空的筆記本檔案。 |
| 入門者 | 預填的筆記型電腦，演示使用樣本資料進行資料探索。 |
| 零售銷售 | 預填的筆記型電腦，使用樣本資料顯示[零售銷售方式](https://adobe.ly/2wOgO3L)。 |
| 方式產生器 | 在[!DNL JupyterLab]中建立配方的筆記本模板。 它預先填入程式碼和評註，以示範和描述方式建立程式。 有關詳細的逐步說明，請參閱[筆記型電腦至配方教程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en)。 |
| [!DNL Query Service] | 預填的筆記本直接在[!DNL JupyterLab]中演示[!DNL Query Service]的用法，並提供了按規模分析資料的示例工作流。 |
| XDM事件 | 預填的筆記型電腦，展示對後置值體驗事件資料的資料探索，著重於資料結構中常見的功能。 |
| XDM查詢 | 預填的筆記型電腦，展示Experience Event資料的業務查詢範例。 |
| 彙總 | 預填的筆記型電腦，演示了將大量資料聚合為較小、可管理的塊的示例工作流。 |
| Clustering | 預填的筆記型電腦，演示使用群集算法的端到端機器學習建模過程。 |

某些筆記型電腦模板僅限於某些內核。 下表映射了每個內核的模板可用性：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>入門者</strong></th>
        <th><strong>零售銷售</strong></th>
        <th><strong>方式產生器</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>XDM事件</strong></th>
        <th><strong>XDM查詢</strong></th>
        <th><strong>彙總</strong></th>
        <th><strong>聚類</strong></th>
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

要開啟新的&#x200B;*啟動器*，請按一下&#x200B;**檔案>新啟動器**。 或者，從左側邊欄展開&#x200B;**檔案瀏覽器**，然後按一下加號(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 後續步驟

要詳細了解每個受支援的筆記型電腦及其使用方法，請訪問[Jupyterlab筆記本資料訪問](./access-notebook-data.md)開發人員指南。 本指南著重於如何使用JupyterLab筆記型電腦來存取資料，包括讀取、寫入和查詢資料。 資料存取指南還包含每個受支援筆記型電腦可讀取的最大資料量資訊。

## 支援的程式庫 {#supported-libraries}

要獲取Python、R和PySpark中支援的包的清單，請在新單元格中複製並貼上`!conda list`，然後運行該單元格。 支援的套件清單會依字母順序填入。

![範例](../images/jupyterlab/user-guide/libraries.PNG)

此外，還使用但未列出下列相依性：
* CUDA 11.2
* CUDN 8.1

