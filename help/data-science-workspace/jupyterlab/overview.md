---
keywords: Experience Platform;JupyterLab；筆記型電腦；Data Science Workspace；熱門主題；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
description: JupyterLab是Project Jupyter的基於Web的用戶介面，並緊密整合到Adobe Experience Platform中。 它為資料科學家提供互動式開發環境，以便與Jupyter Notebooks、代碼和資料協作。 本檔案概述JupyterLab及其功能，以及執行常見動作的指示。
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] UI概述

[!DNL JupyterLab] 是 [朱佩特專案](https://jupyter.org/) 與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與Jupyter Notebooks、代碼和資料協作。

本檔案提供 [!DNL JupyterLab] 及其功能，以及執行常見動作的指示。

## [!DNL JupyterLab] on [!DNL Experience Platform]

Experience Platform的JupyterLab整合附帶了架構變更、設計考量、自訂的筆記型電腦擴充功能、預先安裝的程式庫，以及Adobe主題介面。

下列清單概述JupyterLab在Platform上獨有的部分功能：

| 功能 | 說明 |
| --- | --- |
| **內核** | 內核提供筆記型電腦和其他 [!DNL JupyterLab] 前端是以不同的寫程式語言執行和查看代碼的能力。 [!DNL Experience Platform] 提供其他內核，以支援 [!DNL Python]、R、PySpark和 [!DNL Spark]. 請參閱 [核](#kernels) 一節以取得詳細資訊。 |
| **資料存取** | 直接從記憶體取現有資料集 [!DNL JupyterLab] 完全支援讀寫功能。 |
| **[!DNL Platform]服務整合** | 內建整合可讓您運用其他 [!DNL Platform] 直接從內部 [!DNL JupyterLab]. 支援整合的完整清單位於 [與其他Platform服務整合](#service-integration). |
| **驗證** | 除 <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab的內置安全模型</a>，您的應用程式與Experience Platform（包括Platform服務對服務通訊）之間的每次互動，都會透過 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **開發程式庫** | 在 [!DNL Experience Platform], [!DNL JupyterLab] 提供預先安裝的程式庫 [!DNL Python]、R和PySpark。 請參閱 [附錄](#supported-libraries) 以取得支援程式庫的完整清單。 |
| **程式庫控制器** | 當預安裝的庫缺少滿足您的需要時，可以為Python和R安裝其他庫，並臨時儲存在隔離的容器中以保持 [!DNL Platform] 並確保資料安全。 請參閱 [核](#kernels) 一節以取得詳細資訊。 |

>[!NOTE]
>
>其他程式庫僅適用於其安裝所在的工作階段。 啟動新會話時，必須重新安裝需要的任何其他庫。

## 與其他 [!DNL Platform] 服務 {#service-integration}

標準化和互操作性是背後的關鍵概念 [!DNL Experience Platform]. 整合 [!DNL JupyterLab] on [!DNL Platform] 作為嵌入式IDE，它可以與其他IDE交互 [!DNL Platform] 服務，使您能夠利用 [!DNL Platform] 充分發揮潛力。 以下 [!DNL Platform] 服務於 [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** 使用讀寫功能存取和探索資料集。
* **[!DNL Query Service]:** 使用SQL存取和探索資料集，在處理大量資料時提供較低的資料存取開銷。
* **[!DNL Sensei ML Framework]:** 可訓練及計分資料的模型開發，以及只需按一下即可建立方式。
* **[!DNL Experience Data Model (XDM)]:** 標準化和互操作性是Adobe Experience Platform背後的重要概念。 [Experience Data Model(XDM)](https://www.adobe.com/go/xdm-home-en)受Adobe推動，目標是標準化客戶體驗資料，並定義客戶體驗管理的結構。

>[!NOTE]
>
>部分 [!DNL Platform] 服務整合 [!DNL JupyterLab] 限於特定的內核。 請參閱 [核](#kernels) 以取得更多詳細資訊。

## 主要功能和常見操作

有關 [!DNL JupyterLab] 以下各節提供執行常見操作的說明：

* [訪問JupyterLab](#access-jupyterlab)
* [JupyterLab介面](#jupyterlab-interface)
* [程式碼儲存格](#code-cells)
* [內核](#kernels)
* [內核會話](#kernel-sessions)
* [啟動器](#launcher)

### 存取 [!DNL JupyterLab] {#access-jupyterlab}

在 [Adobe Experience Platform](https://platform.adobe.com)，選取 **[!UICONTROL 筆記本]** 從左側導覽欄。 為 [!DNL JupyterLab] 完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 介面 {#jupyterlab-interface}

此 [!DNL JupyterLab] 介面由菜單欄、可折疊的左側邊欄和包含文檔和活動頁簽的主要工作區組成。

**功能表列**

介面頂端的功能表列有頂層功能表，可顯示 [!DNL JupyterLab] 使用鍵盤快速鍵：

* **檔案：** 與檔案和目錄相關的操作
* **編輯：** 與編輯文檔和其他活動相關的操作
* **查看：** 改變外觀的動作 [!DNL JupyterLab]
* **執行：** 在不同活動（例如筆記型電腦和程式碼主控台）中執行程式碼的動作
* **內核：** 用於管理內核的操作
* **標籤：** 已開啟的文檔和活動的清單
* **設定：** 常見設定和進階設定編輯器
* **說明：** 清單 [!DNL JupyterLab] 內核幫助連結

**左側欄**

左側邊欄包含可點按的標籤，這些標籤提供對以下功能的訪問：

* **檔案瀏覽器：** 已保存的筆記本文檔和目錄的清單
* **資料資源管理器：** 瀏覽、存取和探索資料集和結構
* **運行內核和終端：** 具有終止能力的活動內核和終端會話的清單
* **命令：** 有用命令的清單
* **單元格檢查器：** 提供對工具和元資料的訪問的單元格編輯器，這些工具和元資料可用於設定筆記本以用於呈現
* **索引標籤：** 已開啟標籤的清單

選取標籤以公開其功能，或選取展開的標籤以折疊左側邊欄，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作區**

主要工作領域 [!DNL JupyterLab] 可讓您將檔案和其他活動排列到可調整大小或細分的索引標籤面板中。 將標籤拖曳至標籤面板的中央，以移轉標籤。 將標籤拖曳至面板的左、右、上或底部，以分割面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### GPU和記憶體伺服器配置 [!DNL Python]/R

在 [!DNL JupyterLab] 選取右上角的齒輪圖示以開啟 *筆記型電腦伺服器配置*. 您可以使用滑塊開啟GPU並分配所需的記憶體量。 您可分配的記憶體量取決於貴組織已布建的記憶體量。 選擇 **[!UICONTROL 更新設定]** 儲存。

>[!NOTE]
>
>每個組織只為筆記型電腦配置一個GPU。 如果GPU正在使用中，則需要等待當前已保留GPU的用戶釋放它。 這可以通過註銷或將GPU保持空閒狀態達四小時或更長時間來完成。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 終止和重新啟動 [!DNL JupyterLab]

在 [!DNL JupyterLab]，您可以終止工作階段，以防止使用其他資源。 從選取 **電源表徵圖** ![電源表徵圖](../images/jupyterlab/user-guide/power_button.png)，然後選取 **[!UICONTROL 關閉]** 從彈出式視窗中終止您的工作階段。 筆記型電腦會話在12小時無活動後自動終止。

要重新啟動 [!DNL JupyterLab]，請選取 **重新啟動圖示** ![重新啟動圖示](../images/jupyterlab/user-guide/restart_button.png) 位於電源表徵圖的左側，然後選擇 **[!UICONTROL 重新啟動]** 從彈出視窗顯示。

![終止jupterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 程式碼儲存格 {#code-cells}

代碼單元格是筆記本的主要內容。 它們包含以筆記本關聯內核的語言和作為執行代碼單元的結果的輸出的原始碼。 每個代碼儲存格的右側會顯示執行計數，代表其執行順序。

![](../images/jupyterlab/user-guide/code_cell.png)

常見儲存格動作說明如下：

* **新增儲存格：** 按一下加號(**+**)以新增空白儲存格。 新單元格將放置在當前正在進行交互的單元格下，或者如果沒有特定單元格處於焦點，則放置在筆記本的末尾。

* **移動單元格：** 將游標置於要移動的儲存格右側，然後按一下並拖曳儲存格至新位置。 此外，將單元格從一個筆記本移動到另一個筆記本將複製單元格及其內容。

* **執行儲存格：** 按一下您要執行之儲存格的內文，然後按一下 **play** 圖示(**▶**)。 星號(**\***)會在內核處理執行時顯示在儲存格的執行計數器中，並在完成時以整數取代。

* **刪除儲存格：** 按一下您要刪除之儲存格的內文，然後按一下 **剪刀** 表徵圖。

### 內核 {#kernels}

筆記型電腦內核是用於處理筆記型電腦單元的語言專用計算引擎。 除 [!DNL Python], [!DNL JupyterLab] 在R、PySpark和 [!DNL Spark] （斯卡拉）。 開啟筆記本文檔時，將啟動關聯的內核。 當執行筆記型電腦單元時，內核執行計算並產生可能消耗大量CPU和記憶體資源的結果。 請注意，在關閉內核之前不會釋放已分配的記憶體。

如下表所述，某些特徵和功能僅限於特定內核：

| 內核 | 程式庫安裝支援 | [!DNL Platform] 整合 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 無 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 內核會話 {#kernel-sessions}

上的每個活動筆記本或活動 [!DNL JupyterLab] 使用內核會話。 展開 **運行終端和內核** 標籤。 通過觀察筆記本介面的右上角，可以識別筆記本的內核的類型和狀態。 在下圖中，筆記本的關聯內核為 **[!DNL Python]3** 其當前狀態由右邊的灰色圓表示。 空心圓表示空閒內核，實心圓表示繁忙內核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果內核長時間關閉或處於非活動狀態，則 **沒有內核！** 顯示實心圓。 通過按一下內核狀態並選擇相應的內核類型來激活內核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 啟動器 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自訂 *啟動器* 為支援的內核提供了有用的筆記型電腦模板，以幫助您啟動任務，包括：

| 範本 | 說明 |
| --- | --- |
| 空白 | 空的筆記本檔案。 |
| 入門者 | 預填的筆記型電腦，演示使用樣本資料進行資料探索。 |
| 零售銷售 | 預填的筆記型電腦 [零售方式](../pre-built-recipes/retail-sales.md) 使用範例資料。 |
| 方式產生器 | 用於在 [!DNL JupyterLab]. 它預先填入程式碼和評註，以示範和描述方式建立程式。 請參閱 [筆記型電腦指南](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) 詳細的解說。 |
| [!DNL Query Service] | 預填的筆記本，演示了 [!DNL Query Service] 直接在 [!DNL JupyterLab] 提供大規模分析資料的範例工作流程。 |
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
        <th><strong>Clustering</strong></th>
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

開啟新 *啟動器*，按一下 **「檔案」>「新建啟動器」**. 或者，展開 **檔案瀏覽器** 從左側邊欄按一下加號(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 後續步驟

若要進一步了解每個支援的筆記型電腦以及如何使用，請造訪 [Jupyterlab筆記型電腦資料存取](./access-notebook-data.md) 開發人員指南。 本指南著重於如何使用JupyterLab筆記型電腦來存取資料，包括讀取、寫入和查詢資料。 資料存取指南還包含每個受支援筆記型電腦可讀取的最大資料量資訊。

## 支援的程式庫 {#supported-libraries}

有關Python、R和PySpark中支援的包的清單，請複製並貼上 `!conda list` 在新儲存格中，然後執行儲存格。 支援的套件清單會依字母順序填入。

![範例](../images/jupyterlab/user-guide/libraries.PNG)

此外，還使用但未列出下列相依性：
* CUDA 11.2
* CUDN 8.1

