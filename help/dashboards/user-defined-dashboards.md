---
title: 用戶定義的儀表板
description: 瞭解如何構建和管理自定義儀表板，在此可以建立、添加和編輯定制小部件以可視化關鍵度量。
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: bf2b35e3366c71c51c58b6257cc55f7c9b0cd9c7
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# 用戶定義的儀表板(Beta)

>[!IMPORTANT]
>
>用戶定義的儀表板功能位於Beta中。 其功能和文檔可能會更改。

Adobe Experience Platform儀表板通過用戶定義的儀表板功能幫助您加快洞察和自定義可視化。 此功能使您能夠構建和管理自定義儀表板，您可以在其中建立、添加和編輯定制小部件，以可視化與您的組織相關的關鍵度量。

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 建立自定義儀表板

要建立自定義儀表板，請首先導航至儀表板清單。 選擇 **[!UICONTROL 儀表板]** 從平台UI的左側導航，然後 **[!UICONTROL 建立儀表板]**。

![左側導航中帶有儀表板的儀表板清單和突出顯示的「建立儀表板」。](./images/user-defined-dashboards/create-dashboard.png)

在添加自定義儀表板之前，儀表板清單為空並顯示「未找到儀表板」。 。 建立後，所有用戶定義的儀表板都會列在儀表板清單中。

的 [!UICONTROL 建立儀表板] 對話框。 輸入要建立的小部件集合的人性化的描述性名稱，然後選擇 **[!UICONTROL 保存]**。

![「建立儀表板」對話框。](./images/user-defined-dashboards/create-dashboard-dialog.png)

新建立的空白儀表板將以您所選的名稱出現在視圖的左上角。

## 建立小部件

從新儀表板視圖中，選擇 **[!UICONTROL 添加新小部件]** 開始構件建立過程。

![突出顯示了「添加新小部件」的新空儀表板。](./images/user-defined-dashboards/add-new-widget.png)

### 小部件編寫器

將顯示小部件編寫器工作區。 下一步，選擇 **[!UICONTROL 選擇資料]** 選擇向小部件添加屬性的資料模型。

![小部件編寫器工作區。](./images/user-defined-dashboards/widget-composer.png)

的 [!UICONTROL 選擇資料] 對話框。 從左列中選擇一個資料模型以顯示所有可用表的預覽清單。

>[!NOTE]
>
>用戶定義的儀表板當前僅支援配置檔案資料模型。 將支援更多選項。

![選擇資料對話框。](./images/user-defined-dashboards/select-data-dialog.png)

預覽清單提供有關資料模型中包含的表的詳細資訊。 下表提供了列欄位及其潛在值的說明。

| 列欄位 | 說明 |
|---|---|
| [!UICONTROL 標題] | 表的名稱。 |
| [!UICONTROL 表類型] | 表的類型。 潛在類型包括： `fact`。 `dimension`, `none`。 |
| [!UICONTROL 查找] | 聯接到所選表的表數。 |

選擇 **[!UICONTROL 下一個]** 確認您選擇的資料模型。 下一個視圖顯示左滑軌中可用表的清單。 選擇一個表，查看所選表中包含的資料的全面細分。

的 [!UICONTROL 預覽] 面板包含頁籤 [!UICONTROL 示例記錄] 和 [!UICONTROL 屬性]。 的 [!UICONTROL 示例記錄] 頁籤提供清單視圖中選定表中記錄的子集。 的 [!UICONTROL 屬性] 頁籤為與所選表關聯的每個屬性提供屬性名稱、資料類型和源表。

從左滑軌中可用的清單中選擇一個表，以提供小部件的資料並選擇 **[!UICONTROL 選擇]** 返回到小部件作曲家。

![「選擇資料」對話框，其中「選擇」突出顯示。](./images/user-defined-dashboards/select-a-table.png)

現在，小部件編寫器將填充所選表中的資料。

資料模型和當前選定的表顯示在左滑軌的頂部，可用於建立小部件的屬性列在屬性列中。

![在小部件編寫器中填充資料的小部件。](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>可以通過選擇鉛筆表徵圖(![鉛筆表徵圖。](./images/user-defined-dashboards/edit-icon.png))。

選擇添加表徵圖(。/images/user-defined-dashboards/add-icon.png)中，將屬性添加到X軸或Y軸。

![帶有添加表徵圖下拉清單的小部件編寫器突出顯示，以將屬性添加到小部件軸。](./images/user-defined-dashboards/attributes-dropdown.png)

接下來，從 [!UICONTROL 標籤] 下拉菜單可生成小部件當前設定的預覽可視化。 在 [!UICONTROL 屬性] 在螢幕右側的滑軌中，在 [!UICONTROL 小部件標題] 的子菜單。

![突出顯示了「標籤」下拉清單和小部件標題文本欄位的小部件編寫器。](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

當您對小部件滿意時，請選擇 **[!UICONTROL 保存]**。 小部件名稱下面的勾選表徵圖表示該小部件已保存。

>[!NOTE]
>
>在小部件編寫器中保存小部件時，會將該小部件本地保存到儀表板。 如果退出儀表板編輯器而不保存儀表板，則該小部件將不會保存到儀表板。

![新小部件保存確認。](./images/user-defined-dashboards/save-confirmation.png)

選擇 **[!UICONTROL 取消]** 返回到自定義儀表板。

![建立了帶示例小部件的小部件編寫器。](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>選擇儀表板名稱旁邊的設定表徵圖以查看有關其建立的詳細資訊。 可在顯示的對話框中更改儀表板的名稱。

在此工作區中可以重新排列小部件並調整小部件大小。 選擇 **[!UICONTROL 保存]** 以保留儀表板名稱和配置的佈局。

![帶有自定義小部件的用戶定義的儀表板和突出顯示的保存按鈕。](./images/user-defined-dashboards/user-defined-dashboard.png)

## 後續步驟

通過閱讀此文檔，您可以更好地瞭解如何建立自定義儀表板以及如何為該儀表板建立、編輯和更新自定義小部件。

查找可用的預配置度量和可視化 [配置檔案](./guides/profiles.md#standard-widgets)。 [段](./guides/segments.md#standard-widgets), [目的地](./guides/destinations.md#standard-widgets) 控制板，請參閱各自文檔中的標準小部件清單。
