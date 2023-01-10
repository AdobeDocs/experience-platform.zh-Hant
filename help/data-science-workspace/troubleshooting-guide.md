---
keywords: Experience Platform；疑難排解；Data Science Workspace；熱門主題
solution: Experience Platform
title: Data Science Workspace疑難排解指南
description: 本檔案提供Adobe Experience Platform Data Science Workspace常見問題的解答。
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 疑難排解指南

本檔案提供關於Adobe Experience Platform常見問題的解答 [!DNL Data Science Workspace]. 若有下列問題和疑難排解： [!DNL Platform] 一般而言，請參閱 [Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md).

## JupyterLab筆記本查詢狀態卡在執行狀態

JupyterLab筆記型電腦可能指示單元處於無限執行狀態，某些處於記憶體不足狀態。 例如，查詢大型資料集或執行多個後續查詢時，JupyterLab筆記型電腦可能會耗盡可用記憶體，而無法儲存產生的資料幀對象。 在這種情況下，可以看到一些指標。 首先，即使儲存格顯示為執行，內核仍會進入空閒狀態 [`*`] 表徵圖。 此外，底欄指示RAM的使用/可用量。

![可用記憶體](./images/jupyterlab/user-guide/allocate-ram.png)

在資料讀取期間，記憶體可能會增長，直到達到您所分配的最大記憶體量。 當達到最大記憶體且內核重新啟動時，記憶體即被釋放。 這意味著，由於內核重新啟動，此情境中使用的記憶體可能顯示為非常低，而在重新啟動之前，記憶體將非常接近最大分配的RAM。

要解決此問題，請選取JupyterLab右上角的齒輪圖示，然後將滑桿滑至右側，然後選取 **[!UICONTROL 更新設定]** 配置更多RAM。 此外，如果您正在運行多個查詢，並且您的RAM值接近最大分配量，除非您需要先前查詢的結果，否則請重新啟動內核以重置可用的RAM量。 這可確保您擁有當前查詢可用的最大RAM量。

![分配更多記憶體](./images/jupyterlab/user-guide/notebook-gpu-config.png)

如果在分配最大記憶體量(RAM)時仍遇到此問題，則可以通過減少資料列或資料範圍來修改查詢以操作較小的資料集大小。 要使用全部資料，建議您使用Spark筆記本。

## [!DNL JupyterLab] 環境未載入 [!DNL Google Chrome]

>[!IMPORTANT]
>
>此問題已解決，但Google Chrome 80.x瀏覽器中仍可能存在。 請確定您的Chrome瀏覽器為最新。

使用 [!DNL Google Chrome] 瀏覽器80.x版，預設會封鎖所有協力廠商cookie。 此策略可防止 [!DNL JupyterLab] 從Adobe Experience Platform內載入。

若要解決此問題，請使用下列步驟：

在 [!DNL Chrome] 瀏覽器，導覽至右上角並選取 **設定** (您也可以複製「chrome://settings/」並貼到位址列)。 下一步，捲動至頁面底部，然後按一下 **進階** 下拉式清單。

![chrome advanced](./images/faq/chrome-advanced.png)

此 **隱私權與安全性** 的上界。 下一步，按一下 **網站設定** 後跟 **Cookie和網站資料**.

![chrome advanced](./images/faq/privacy-security.png)

![chrome advanced](./images/faq/cookies.png)

最後，將「封鎖第三方Cookie」切換為「關閉」。

![chrome advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您也可以停用第三方Cookie並新增 [*.]ds.adobe.net至允許清單。

導覽至您位址列中的「chrome://flags/」。 搜尋並停用標題為的標幟 *&quot;SameSite依預設Cookie&quot;* 使用右側的下拉式功能表。

![停用samesite標幟](./images/faq/samesite-flag.png)

步驟2後，系統會提示您重新啟動瀏覽器。 重新啟動後， [!DNL Jupyterlab] 應可供存取。

## 為什麼我無法存取 [!DNL JupyterLab] 在Safari?

Safari預設會在Safari &lt; 12中停用第三方Cookie。 因為 [!DNL Jupyter] 虛擬機實例位於與其父幀不同的域上，Adobe Experience Platform當前要求啟用第三方cookie。 請啟用第三方Cookie或切換至其他瀏覽器，例如 [!DNL Google Chrome].

若是Safari 12，您需要將使用者代理切換為「[!DNL Chrome]&#39;或&#39;[!DNL Firefox]&#39;。 若要切換使用者代理，請從開啟 *Safari* 選取 **偏好設定**. 將出現首選項窗口。

![Safari偏好設定](./images/faq/preferences.png)

在Safari偏好設定視窗中，選取 **進階**. 然後檢查 *在菜單欄中顯示開髮菜單* 框。 完成此步驟後，可以關閉首選項窗口。

![Safari進階](./images/faq/advanced.png)

接下來，從頂端導覽列選取 **開發** 功能表。 從 **開發** 下拉式清單，暫留在 **使用者代理**. 您可以選取 **[!DNL Chrome]** 或 **[!DNL Firefox]** 您要使用的使用者代理字串。

![開發功能表](./images/faq/user-agent.png)

## 嘗試上傳或刪除中的檔案時，為何會看到「403禁止」訊息 [!DNL JupyterLab]?

如果您的瀏覽器啟用了播發阻止軟體，例如 [!DNL Ghostery] 或 [!DNL AdBlock] 此外，每個廣告封鎖軟體中都必須允許網域「\*.adobe.net」， [!DNL JupyterLab] 才能正常運作。 這是因為 [!DNL JupyterLab] 虛擬機運行在與 [!DNL Experience Platform] 網域。

## 為什麼我的 [!DNL Jupyter Notebook] 看起來已加亂，或未呈現為代碼？

如果意外將相關儲存格從「程式碼」變更為「Markdown」，就會發生此情況。 當程式碼儲存格聚焦時，按鍵組合 **ESC+M** 將儲存格的類型變更為Markdown。 通過筆記本頂部的下拉指示器，可以更改所選單元格的類型。 若要將儲存格類型變更為程式碼，請從選取您要變更的指定儲存格開始。 接下來，按一下指出儲存格目前類型的下拉式清單，然後選取「程式碼」。

![](./images/faq/code_type.png)

## 如何安裝自訂 [!DNL Python] 圖書館？

此 [!DNL Python] kernel隨許多流行的機器學習庫預裝。 不過，您可以在程式碼儲存格內執行下列命令，以安裝其他自訂程式庫：

```shell
!pip install {LIBRARY_NAME}
```

如需預先安裝的完整清單 [!DNL Python] 程式庫，請參閱 [JupyterLab使用手冊附錄一節](./jupyterlab/overview.md#supported-libraries).

## 我可以安裝自訂的PySpark程式庫嗎？

很遺憾，無法為PySpark內核安裝其他庫。 不過，您可以聯絡Adobe客戶服務代表，為您安裝自訂PySpark程式庫。

如需預先安裝的PySpark程式庫清單，請參閱 [JupyterLab使用手冊附錄一節](./jupyterlab/overview.md#supported-libraries).

## 是否可以配置 [!DNL Spark] 群集資源 [!DNL JupyterLab] [!DNL Spark] 還是PySpark內核？

通過將以下塊添加到筆記本的第一個單元格中，可以配置資源：

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

如需 [!DNL Spark] 群集資源配置，包括可配置屬性的完整清單，請參見 [JupyterLab使用手冊](./jupyterlab/overview.md#kernels).

## 嘗試對較大的資料集執行特定任務時，為何出現錯誤？

如果您收到錯誤，原因如 `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` 這通常表示驅動程式或執行器記憶體不足。 請參閱JupyterLab筆記型電腦 [資料存取](./jupyterlab/access-notebook-data.md) 檔案，以取得資料限制以及如何在大型資料集上執行工作的詳細資訊。 通常，此錯誤可透過變更 `mode` 從 `interactive` to `batch`.

此外，在撰寫大型Spark/PySpark資料集時，請快取您的資料(`df.cache()`)之前執行寫程式碼可大幅提升效能。

<!-- remove this paragraph at a later date once the sdk is updated -->

如果您在讀取資料時遇到問題，並將轉換套用至資料，請嘗試在轉換之前快取資料。 快取資料可防止網路上出現多次讀取。 從讀取資料開始。 下一步，快取(`df.cache()`)資料。 最後，執行轉換。

## Spark/PySpark筆記本為何花了這麼長的時間才讀取和寫入資料？

如果您要對資料執行轉換，例如使用 `fit()`，則轉換可能會執行多次。 若要提高效能，請使用 `df.cache()` 執行 `fit()`. 這可確保轉換只執行一次，並防止網路上出現多次讀取。

**建議訂單：** 從讀取資料開始。 接下來，執行轉換，然後快取(`df.cache()`)資料。 最後，執行 `fit()`.

## 為什麼我的Spark/PySpark筆記本無法運行？

如果您收到下列任何錯誤：

- 作業因預備失敗而中止……只能壓縮每個分區中元素數量相同的RDD。
- 遠程RPC客戶端斷開關聯和其他記憶體錯誤。
- 讀取和寫入資料集時效能不佳。

檢查以確定您正在快取資料(`df.cache()`)，再寫入資料。 在筆記本中執行代碼時，使用 `df.cache()` (例如 `fit()` 可大大提高筆記型電腦的效能。 使用 `df.cache()` 寫入資料集前，請確保轉換只執行一次，而非執行多次。

## [!DNL Docker Hub] Data Science Workspace的限制限制

自2020年11月20日起，Docker Hub的匿名免費驗證使用率限制已生效。 匿名和免費 [!DNL Docker Hub] 使用者每六小時最多只能有100個容器影像提取請求。 如果您受到這些變更的影響，將會收到此錯誤訊息： `ERROR: toomanyrequests: Too Many Requests.` 或 `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

目前，此限制僅在您試圖在6小時內構建100個筆記型電腦至配方，或在Data Science Workspace中使用Spark筆記型電腦（經常放大和縮小）時，才會影響您的組織。 但是，這不太可能，因為這些運行在上的群集在空閒之前保持活動狀態兩小時。 這會減少叢集作用中時所需的提取數。 如果您收到上述任何錯誤，則需等待您 [!DNL Docker] 限制已重設。

如需 [!DNL Docker Hub] 速率限制，造訪 [DockerHub檔案](https://www.docker.com/increase-rate-limits). 解決方案正在運作中，且預期會在後續版本中推出。
