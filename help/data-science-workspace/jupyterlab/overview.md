---
keywords: Experience Platform;JupyterLab；筆記本；資料科學工作區；熱門主題；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
description: JupyterLab是Project Jupyter的一個基於Web的用戶介面，並與Adobe Experience Platform緊密整合。 它為資料科學家提供了互動式開發環境，以便他們與Jupyter筆記本、代碼和資料一起工作。 本文檔概述了JupyterLab及其功能以及執行常見操作的說明。
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] UI概述

[!DNL JupyterLab] 是基於Web的用戶介面 [朱佩特工程](https://jupyter.org/) 並且緊密融入Adobe Experience Platform。 它為資料科學家提供了互動式開發環境，以便他們與Jupyter筆記本、代碼和資料一起工作。

此文檔提供 [!DNL JupyterLab] 以及執行常見操作的說明。

## [!DNL JupyterLab] 上 [!DNL Experience Platform]

Experience Platform的JupyterLab整合附帶了架構更改、設計考慮、定製的筆記本擴展、預安裝的庫和Adobe主題介面。

以下清單概述了JupyterLab在平台上獨有的一些功能：

| 功能 | 說明 |
| --- | --- |
| **核** | 內核提供筆記本和其他 [!DNL JupyterLab] 前端是以不同寫程式語言執行和反映代碼的能力。 [!DNL Experience Platform] 提供其他內核以支援開發 [!DNL Python]、R、PySpark和 [!DNL Spark]。 查看 [核](#kernels) 的子菜單。 |
| **資料存取** | 直接從中訪問現有資料集 [!DNL JupyterLab] 完全支援讀寫功能。 |
| **[!DNL Platform]服務整合** | 內置整合允許您利用其他 [!DNL Platform] 直接從內部 [!DNL JupyterLab]。 有關支援的整合的完整清單，請參見 [與其他平台服務整合](#service-integration)。 |
| **驗證** | 除 <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab的內置安全模型</a>，應用程式與Experience Platform之間的每個交互（包括平台服務到服務通信）都通過加密和驗證 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>。 |
| **開發程式庫** | 在 [!DNL Experience Platform]。 [!DNL JupyterLab] 為 [!DNL Python]、R和PySpark。 查看 [附錄](#supported-libraries) 的子菜單。 |
| **庫控制器** | 當預安裝的庫因您的需要而不足時，可以為Python和R安裝其他庫，並臨時儲存在隔離的容器中以保持 [!DNL Platform] 保證資料安全。 查看 [核](#kernels) 的子菜單。 |

>[!NOTE]
>
>其他庫僅可用於安裝它們的會話。 啟動新會話時，必須重新安裝所需的任何其他庫。

## 與其他 [!DNL Platform] 服務 {#service-integration}

標準化和互操作性是其背後的關鍵概念 [!DNL Experience Platform]。 整合 [!DNL JupyterLab] 上 [!DNL Platform] 作為嵌入式IDE，它可以與其他 [!DNL Platform] 服務，使您能夠利用 [!DNL Platform] 它的潛力。 以下 [!DNL Platform] 服務 [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** 使用讀寫功能訪問和瀏覽資料集。
* **[!DNL Query Service]:** 使用SQL訪問和瀏覽資料集，在處理大量資料時提供較低的資料存取開銷。
* **[!DNL Sensei ML Framework]:** 能夠訓練和評分資料的模型開發，以及只需按一下即可建立處方。
* **[!DNL Experience Data Model (XDM)]:** 標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 [體驗資料模型(XDM)](https://www.adobe.com/go/xdm-home-en)在Adobe的推動下，這是一種努力，目的是標準化客戶體驗資料並定義客戶體驗管理模式。

>[!NOTE]
>
>部分 [!DNL Platform] 服務整合 [!DNL JupyterLab] 限於特定的內核。 請參閱上 [核](#kernels) 的子菜單。

## 關鍵功能和常見操作

有關以下關鍵功能的資訊 [!DNL JupyterLab] 以下各節提供了有關執行常見操作的說明：

* [訪問JupyterLab](#access-jupyterlab)
* [JupyterLab介面](#jupyterlab-interface)
* [代碼單元格](#code-cells)
* [核](#kernels)
* [內核會話](#kernel-sessions)
* [啟動程式](#launcher)

### 存取 [!DNL JupyterLab] {#access-jupyterlab}

在 [Adobe Experience Platform](https://platform.adobe.com)選中 **[!UICONTROL 筆記本]** 的下界。 允許一些時間 [!DNL JupyterLab] 完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 介面 {#jupyterlab-interface}

的 [!DNL JupyterLab] 介面由菜單欄、可折疊左側提要欄和包含文檔和活動頁籤的主工作區組成。

**功能表列**

介面頂部的菜單欄具有顯示操作的頂級菜單， [!DNL JupyterLab] 鍵盤快捷鍵：

* **檔案：** 與檔案和目錄相關的操作
* **編輯：** 與編輯文檔和其他活動相關的操作
* **視圖：** 改變外觀的操作 [!DNL JupyterLab]
* **運行：** 在不同活動（如筆記本和代碼控制台）中運行代碼的操作
* **內核：** 用於管理內核的操作
* **頁籤：** 開啟的文檔和活動清單
* **設定：** 常用設定和高級設定編輯器
* **幫助：** 清單 [!DNL JupyterLab] 和內核幫助連結

**左側欄**

左側提要欄包含可點擊的頁籤，可訪問以下功能：

* **檔案瀏覽器：** 保存的筆記本文檔和目錄清單
* **資料資源管理器：** 瀏覽、訪問和瀏覽資料集和架構
* **運行內核和終端：** 具有終止功能的活動內核和終端會話的清單
* **命令：** 有用命令清單
* **單元格檢查器：** 提供對工具和元資料的訪問的單元格編輯器，這些工具和元資料對於設定筆記本以用於演示目的非常有用
* **頁籤：** 開啟的頁籤清單

選擇一個頁籤以顯示其功能，或在展開的頁籤上選擇以折疊左側提要欄，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作區**

中國 [!DNL JupyterLab] 允許您將文檔和其他活動排列到可調整大小或細分的頁籤面板中。 將標籤拖到標籤面板的中心以遷移標籤。 將頁籤拖動到面板的左、右、頂部或底部，以分隔面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### GPU和記憶體伺服器配置 [!DNL Python]/R

在 [!DNL JupyterLab] 選擇右上角的齒輪表徵圖以開啟 *筆記本伺服器配置*。 可以通過使用滑塊開啟GPU並分配所需的記憶體量。 您可以分配的記憶體量取決於您的組織已調配的記憶體量。 選擇 **[!UICONTROL 更新配置]** 來保存。

>[!NOTE]
>
>每個組織只為筆記本預配一個GPU。 如果GPU正在使用，則需要等待當前已保留GPU的用戶釋放它。 這可以通過註銷或將GPU處於空閒狀態達四小時或更長時間來完成。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 終止並重新啟動 [!DNL JupyterLab]

在 [!DNL JupyterLab]，您可以終止會話，以防止使用更多資源。 從選擇 **電源表徵圖** ![電源表徵圖](../images/jupyterlab/user-guide/power_button.png)，然後選擇 **[!UICONTROL 關閉]** 從終止會話的跨距。 筆記本會話在12小時無活動後自動終止。

重新啟動 [!DNL JupyterLab]，選擇 **重新啟動表徵圖** ![重新啟動表徵圖](../images/jupyterlab/user-guide/restart_button.png) 位於電源表徵圖的左側，然後選擇 **[!UICONTROL 重新啟動]** 從出現的跨距。

![終止jupterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 代碼單元格 {#code-cells}

代碼單元是筆記本的主要內容。 它們包含以筆記本關聯內核語言和作為執行代碼單元格結果的輸出的原始碼。 每個代碼單元的右側顯示一個執行計數，該代碼單元表示其執行順序。

![](../images/jupyterlab/user-guide/code_cell.png)

下面介紹了常用單元格操作：

* **添加單元格：** 按一下加號(**+**)以添加空單元格。 新的單元被放置在當前正在交互的單元下，或者如果沒有特定單元處於焦點中，則放置在筆記本的末尾。

* **移動單元格：** 將游標置於要移動的單元格的右側，然後按一下並將單元格拖動到新位置。 此外，將單元格從一個筆記本移動到另一個筆記本會複製該單元格及其內容。

* **執行單元格：** 按一下要執行的單元格的主體，然後按一下 **玩** 表徵圖。**▶**)。 星號(**\***)在內核處理執行時顯示在單元格的執行計數器中，並在完成後替換為整數。

* **刪除單元格：** 按一下要刪除的單元格的正文，然後按一下 **剪刀** 表徵圖

### 核 {#kernels}

筆記型電腦內核是處理筆記型電腦單元的語言特定計算引擎。 除 [!DNL Python]。 [!DNL JupyterLab] 在R、PySpark和 [!DNL Spark] （斯卡拉）。 開啟筆記本文檔時，將啟動關聯的內核。 當筆記本單元被執行時，內核執行計算並產生可能消耗大量CPU和記憶體資源的結果。 請注意，在內核關閉之前不會釋放已分配的記憶體。

下表所述，某些功能和特性僅限於特定內核：

| 內核 | 庫安裝支援 | [!DNL Platform] 整合 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 無 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 內核會話 {#kernel-sessions}

每個活動筆記本或活動 [!DNL JupyterLab] 利用內核會話。 通過擴展 **運行終端和內核** 的下界。 可通過觀察筆記本介面的右上角來標識筆記本內核的類型和狀態。 在下圖中，筆記本的關聯內核是 **[!DNL Python]3** 其當前狀態由右邊的灰色圓表示。 空心圓表示空閒內核，實心圓表示忙碌內核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果內核長時間關閉或處於非活動狀態，則 **無內核！** 顯示實心圓。 通過按一下內核狀態並選擇相應的內核類型來激活內核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 啟動程式 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定義 *啟動程式* 為支援的內核提供了有用的筆記本模板，以幫助您啟動任務，包括：

| 範本 | 說明 |
| --- | --- |
| 空白 | 空的筆記本檔案。 |
| 啟動器 | 預填充的筆記本演示使用示例資料的資料探索。 |
| 零售銷售 | 預填充筆記本 [零售銷售處理](../pre-built-recipes/retail-sales.md) 使用示例資料。 |
| 處方生成器 | 用於在中建立處方的筆記本模板 [!DNL JupyterLab]。 它預填充了演示和描述處方建立過程的代碼和注釋。 請參閱 [筆記本 — 處方教程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) 詳細的漫步。 |
| [!DNL Query Service] | 預填充的筆記本演示了 [!DNL Query Service] 直接 [!DNL JupyterLab] 提供了以規模分析資料的示例工作流。 |
| XDM事件 | 預填充的筆記本演示有關後值體驗事件資料的資料探索，重點介紹資料結構中常見的功能。 |
| XDM查詢 | 預填充的筆記本演示有關體驗事件資料的示例業務查詢。 |
| 彙總 | 預填充的筆記本演示了將大量資料聚合到更小、可管理的塊中的示例工作流。 |
| Clustering | 一種預先填充的筆記本演示使用聚類算法的端到端機器學習建模過程。 |

某些筆記本模板限於某些內核。 下表映射了每個內核的模板可用性：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>啟動器</strong></th>
        <th><strong>零售銷售</strong></th>
        <th><strong>處方生成器</strong></th>
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

開啟新 *啟動程式*&#x200B;按一下 **「檔案」>「新建啟動程式」**。 或者，展開 **檔案瀏覽器** 從左側欄中按一下加號(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 後續步驟

要瞭解有關每個受支援筆記本的詳細資訊以及如何使用這些筆記本，請訪問 [Jupyterlab筆記本資料存取](./access-notebook-data.md) 的子菜單。 本指南重點介紹如何使用JupyterLab筆記本訪問資料，包括讀取、寫入和查詢資料。 資料存取指南還包含關於每個受支援筆記本可讀取的最大資料量的資訊。

## 支援的庫 {#supported-libraries}

有關Python、R和PySpark中支援的包的清單，請複製和貼上 `!conda list` 的子菜單。 支援的包清單按字母順序填充。

![示例](../images/jupyterlab/user-guide/libraries.PNG)

此外，還使用但未列出以下依賴項：
* CUDA 11.2
* CUDN 8.1

