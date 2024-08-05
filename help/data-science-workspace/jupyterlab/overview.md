---
keywords: Experience Platform；JupyterLab；筆記本；資料科學Workspace；熱門主題；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
description: JupyterLab是Project Jupyter的網頁型使用者介面，並緊密整合至Adobe Experience Platform。 它提供互動式開發環境，讓資料科學家能夠使用Jupyter Notebooks、程式碼和資料。 本檔案概述JupyterLab及其功能，以及執行常見動作的指示。
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 2%

---

# [!DNL JupyterLab] UI 概觀

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

[!DNL JupyterLab]是[Project Jupyter](https://jupyter.org/)的網頁式使用者介面，且已緊密整合至Adobe Experience Platform。 它提供互動式開發環境，讓資料科學家能夠使用Jupyter Notebooks、程式碼和資料。

本檔案提供[!DNL JupyterLab]及其功能的概觀，以及執行一般動作的指示。

## [!DNL Experience Platform]上的[!DNL JupyterLab]

Experience Platform的JupyterLab整合伴隨著架構變更、設計考量、自訂的筆記型電腦擴充功能、預先安裝的程式庫，以及Adobe主題的介面。

下列清單概述JupyterLab on Platform的專屬功能：

| 功能 | 說明 |
| --- | --- |
| **核心** | 核心提供筆記型電腦和其他[!DNL JupyterLab]前端以不同程式語言執行和內部檢查程式碼的能力。 [!DNL Experience Platform]提供額外的核心以支援[!DNL Python]、R、PySpark和[!DNL Spark]中的開發。 如需詳細資訊，請參閱[核心](#kernels)區段。 |
| **數據存取** | 從內部 [!DNL JupyterLab] 直接存取現有資料集，完全支援讀寫功能。 |
| **[!DNL Platform]服務整合** | 內建整合可讓您直接從[!DNL JupyterLab]內使用其他[!DNL Platform]服務。 在[與其他Platform服務](#service-integration)整合的區段中，提供支援整合的完整清單。 |
| **驗證** | 除了JupyterLab的內置安全模型</a>外<a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">，您的應用程式和Experience Platform之間的每次交互，包括Platform服務到服務的通信，都通過（IMS）</a>進行<a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System]加密和身份驗證。 |
| **開發資料庫** | 在 中 [!DNL Experience Platform]， [!DNL JupyterLab] 提供了 、R 和 PySpark 的 [!DNL Python]預安裝資料庫。 [有關受支持資料庫的完整清單，請參閱附錄](#supported-libraries)。 |
| **庫控制器** | 當預安裝的資料庫無法滿足您的需求時，可以為 Python 和 R 安裝額外的資料庫，並臨時存儲在隔離的容器中，以維護數據的完整性 [!DNL Platform] 並確保數據的安全。 如需詳細資訊，請參閱[核心](#kernels)區段。 |

>[!NOTE]
>
>其他程式庫僅適用於已安裝這些程式庫的工作階段。 啟動新工作階段時，您必須重新安裝任何其他所需的程式庫。

## 與其他[!DNL Platform]服務整合 {#service-integration}

標準化和互通性是[!DNL Experience Platform]背後的重要概念。 將[!DNL Platform]上的[!DNL JupyterLab]整合為內嵌IDE，可讓您與其他[!DNL Platform]服務互動，讓您充分利用[!DNL Platform]的潛力。 下列[!DNL Platform]服務可在[!DNL JupyterLab]中使用：

* **[!DNL Catalog Service]：** 使用讀寫功能訪問和瀏覽數據集。
* **[!DNL Query Service]：** 使用 SQL 訪問和瀏覽資料集，在處理大量數據時提供更低的數據訪問開銷。
* **[!DNL Sensei ML Framework]：** 模型開發，能夠訓練和評分數據，只需按一下即可創建方式。
* **[!DNL Experience Data Model (XDM)]：** 標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 [體驗資料模型(XDM)](https://www.adobe.com/go/xdm-home-en)由Adobe驅動，致力於標準化客戶體驗資料並定義客戶體驗管理的結構描述。

>[!NOTE]
>
>[!DNL JupyterLab]上的某些[!DNL Platform]服務整合僅限特定核心。 如需詳細資訊，請參閱[核心](#kernels)的章節。

## 主要功能與常見操作

有關[!DNL JupyterLab]主要功能的資訊，以及執行一般作業的指示在以下各節中提供：

* [存取JupyterLab](#access-jupyterlab)
* [JupyterLab介面](#jupyterlab-interface)
* [Code儲存格](#code-cells)
* [內核](#kernels)
* [內核會話](#kernel-sessions)
* [發射](#launcher)

### 存取[!DNL JupyterLab] {#access-jupyterlab}

在[Adobe Experience Platform](https://platform.adobe.com)中，從左側導覽欄選取&#x200B;**[!UICONTROL 筆記本]**。 留出時間讓[!DNL JupyterLab]完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 介面 {#jupyterlab-interface}

該 [!DNL JupyterLab] 介面由功能表欄、可摺疊左側邊欄以及包含文件和活動選項卡的主工作區組成。

**功能表欄**

介面頂部的功能表列具有頂級功能表，這些功能表顯示其鍵盤快捷鍵中可用的 [!DNL JupyterLab] 操作：

* **檔案：**&#x200B;與檔案和目錄相關的動作
* **編輯：**&#x200B;與編輯檔案和其他活動相關的動作
* **檢視：**&#x200B;變更[!DNL JupyterLab]外觀的動作
* **執行：**&#x200B;在不同活動（例如筆記本和程式碼主控台）中執行程式碼的動作
* **核心：**&#x200B;管理核心的動作
* **標籤：**&#x200B;開啟的檔案和活動清單
* **設定：**&#x200B;一般設定和進階設定編輯器
* **說明：** [!DNL JupyterLab]與核心說明連結的清單

**左側欄**

左側邊欄包含可點按的標籤，可讓您存取以下功能：

* **檔案瀏覽器：**&#x200B;已儲存的筆記本檔案和目錄清單
* **資料總管：**&#x200B;瀏覽、存取及探索資料集和結構描述
* **正在執行核心與終端機：**&#x200B;具有終止功能的作用中核心與終端機工作階段清單
* **命令：**&#x200B;有用的命令清單
* **儲存格檢視窗：**&#x200B;儲存格編輯器，可讓您存取用來設定筆記本以供簡報使用的工具和中繼資料
* **標籤：**&#x200B;開啟的標籤清單

選取標籤以公開其功能，或在展開的標籤上選取以摺疊左側邊欄，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作區**

[!DNL JupyterLab]中的主要工作區域可讓您將檔案和其他活動排列成可調整大小或可再分割的標籤面板。 將標籤拖曳至標籤面板中央以移轉標籤。 將標籤拖曳至面板的左側、右側、頂端或底部來分割面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### [!DNL Python]/R中的GPU和記憶體伺服器組態

在[!DNL JupyterLab]中，選取右上角的齒輪圖示以開啟&#x200B;*Notebook伺服器組態*。 您可以使用滑桿打開 GPU 並分配所需的內存量。 可以分配的內存量取決於組織已預配的內存量。 選擇「****&#x200B;更新配置」 以保存。

>[!NOTE]
>
>每個組織僅為筆記型電腦預配一個 GPU。 如果GPU正在使用中，您需要等待目前保留GPU的使用者釋出它。 登出或讓GPU處於閒置狀態四個小時以上，即可完成這項作業。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 終止並重新啟動[!DNL JupyterLab]

在[!DNL JupyterLab]中，您可以終止工作階段以防止使用其他資源。 開始方法是選擇電源圖示![**電源**&#x200B;圖示](/help/images/icons/power.png)，然後從彈出的彈出視窗中選擇關機&#x200B;]**，以**[!UICONTROL &#x200B;終止會話。筆記本會話在 12 小時無活動後自動終止。

要重新啟動 [!DNL JupyterLab]，請選擇&#x200B;**直接位於電源圖示左側的重新啟動圖示**](/help/images/icons/restart.png)![重新啟動圖示，然後&#x200B;**[!UICONTROL 從顯示的彈出視窗中選擇重新啟動]**。

![終止 Jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Code儲存格 {#code-cells}

Code單元是筆記本的主要內容。 它們包含筆記本關聯內核語言的原始程式碼以及執行代碼單元的結果輸出。 執行計數顯示在表示其執行順序的每個代碼儲存格的右側。

![](../images/jupyterlab/user-guide/code_cell.png)

常見的儲存格操作如下所述：

* **新增儲存格：**&#x200B;按一下筆記本功能表中的加號符號(**+**)以新增空白儲存格。 新儲存格會放置在目前互動的儲存格下方，如果沒有特定儲存格處於焦點，則位於筆記本的結尾。

* **移動儲存格：**&#x200B;將游標放在您要移動的儲存格右側，然後按一下並將儲存格拖曳到新的位置。 此外，將儲存格從一個筆記本移到另一個筆記本會複製儲存格及其內容。

* **執行儲存格：**&#x200B;按一下您要執行的儲存格內文，然後按一下筆記本功能表中的&#x200B;**播放**&#x200B;圖示(**▶**)。 當核心處理執行時，儲存格的執行計數器會顯示星號(**\***)，並在完成時以整數取代。

* **刪除單元格：** 按下要刪除的儲存格的正文，然後按下 **剪刀** 圖示。

### 核心 {#kernels}

筆記型電腦核心是處理筆記型電腦儲存格的語言專屬運算引擎。 除了[!DNL Python]，[!DNL JupyterLab]還提供R、PySpark和[!DNL Spark] (Scala)的額外語言支援。 當您開啟筆記本檔案時，會啟動相關的核心。 執行筆記型電腦儲存格時，核心會執行運算並產生耗用大量CPU和記憶體資源的結果。 請注意，在關閉核心之前，不會釋放配置的記憶體。

某些特性和功能僅限於特定的內核，如下表所述：

| 核心 | 庫安裝支援 | [!DNL Platform] 集成 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | 無 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 內核會話 {#kernel-sessions}

[!DNL JupyterLab]上的每個使用中筆記本或活動都使用核心工作階段。 從左側邊欄展開&#x200B;**執行中的終端機和核心**&#x200B;標籤，即可找到所有使用中的工作階段。 觀察筆記型電腦介面的右上角，即可識別筆記型電腦核心的型別和狀態。 在下圖中，筆記本的關聯核心為&#x200B;**[!DNL Python]3**，其目前狀態由右邊的灰色圓圈表示。 空心圓表示閒置核心，實心圓表示忙碌核心。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果內核長時間關閉或處於非活動狀態，則 **沒有內核！** 顯示實心圓圈。 通過單擊內核狀態並選擇適當的內核類型來啟動內核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 發射 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自訂的&#x200B;*啟動器*&#x200B;提供您實用的筆記本範本，供您使用受支援的核心，協助您開始工作，包括：

| 範本 | 說明 |
| --- | --- |
| 空白 | 空的筆記本檔案。 |
| 入門者 | 預先填入的筆記型電腦，示範使用範例資料進行資料探索。 |
| 零售銷售 | 使用範例資料預先填入的筆記本，其中包含[零售銷售方式](../pre-built-recipes/retail-sales.md)。 |
| 配方產生器 | 用來在[!DNL JupyterLab]中建立配方的筆記本範本。 其中預先填入程式碼和註解，以示範和說明配方建立流程。 如需詳細逐步解說，請參閱[筆記本到配方教學課程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en)。 |
| [!DNL Query Service] | 預先填入的筆記本，以示範直接在[!DNL JupyterLab]中使用[!DNL Query Service]，並提供大規模分析資料的範例工作流程。 |
| XDM事件 | 預先填寫的筆記型電腦，示範有關後值體驗事件資料的資料探索，重點放在資料結構中的共同功能。 |
| XDM查詢 | 預先填寫的筆記本，示範有關體驗事件資料的範例企業查詢。 |
| 彙總 | 預先填入的筆記型電腦，展示將大量資料彙總成可管理之較小區塊的範例工作流程。 |
| 叢集 | 預先填寫的筆記型電腦，展示使用叢集演演算法的端對端機器學習模型化程式。 |

有些筆記本範本僅限於某些核心。 每個核心的範本可用性如下表所示：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>起動機</strong></th>
        <th><strong>零售銷售</strong></th>
        <th><strong>配方產生器</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>XDM事件</strong></th>
        <th><strong>XDM 查詢</strong></th>
        <th><strong>彙總</strong></th>
        <th><strong>叢集</strong></th>
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
        <th  ><strong>PySpark 3 （[!DNL Spark] 2.4）</strong></th>
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
        <th ><strong>Scala</strong></th>
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

若要開啟新的&#x200B;*啟動器*，請按一下&#x200B;**檔案>新增啟動器**。 或者，從左側邊欄展開&#x200B;**檔案瀏覽器**，然後按一下加號符號(**+**)：

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 後續步驟

若要進一步瞭解每個支援的筆記型電腦及其使用方式，請造訪[Jupyterlab notebooks資料存取](./access-notebook-data.md)開發人員指南。 本指南著重於如何使用JupyterLab Notebooks存取您的資料，包括讀取、寫入和查詢資料。 資料存取指南也包含每個支援筆記型電腦可讀取的最大資料量資訊。

## 支援的程式庫 {#supported-libraries}

如需Python、R和PySpark中支援的套件清單，請將`!conda list`複製並貼到新的儲存格中，然後執行儲存格。 支援的套件清單會依字母順序填入。

![範例](../images/jupyterlab/user-guide/libraries.PNG)

此外，以下相依性已使用但未列出：
* CUDA 11.2
* CUDNN 8.1

