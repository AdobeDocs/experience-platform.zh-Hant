---
keywords: Experience Platform；首頁；熱門主題；沙盒使用手冊；沙盒指南
solution: Experience Platform
title: 沙盒UI指南
description: 本文檔提供了如何在Adobe Experience Platform用戶介面中執行與沙箱相關的各種操作的步驟。
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 8%

---

# 沙盒UI指南

本文檔提供了如何在Adobe Experience Platform用戶介面中執行與沙箱相關的各種操作的步驟。

## 查看沙箱

在平台UI中，選擇 **[!UICONTROL 沙箱]** 在左側導航中，然後選擇 **[!UICONTROL 瀏覽]** 開啟 [!UICONTROL 沙箱] 控制項欄。 控制板列出組織的所有可用沙箱，包括它們各自的類型（生產或開發）。

![視圖箱](../images/ui/view-sandboxes.png)

## 在沙箱之間切換

沙盒指示器位於平台UI的頂部標題中，並顯示您當前所在沙盒的標題、其區域及其類型。

![沙盒指示器](../images/ui/sandbox-indicator.png)

要在沙盒之間切換，請選擇沙盒指示器並從下拉清單中選擇所需沙盒。

![交換機介面](../images/ui/switcher-interface.png)

選擇沙盒後，螢幕將刷新並更新您選擇的沙盒。

![沙盒交換](../images/ui/sandbox-switched.png)

## 建立新沙盒 {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="沙箱名稱"
>abstract="沙箱名稱指在後端用於為此沙箱建立唯一 ID 的文字。"

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="沙箱標題"
>abstract="沙箱標題指在整個 Experience Platform UI 的選單和下拉式清單中代表沙箱的顯示名稱。"

>[!NOTE]
>
>建立新沙盒時，必須先將新沙盒添加到產品配置檔案中 [Adobe Admin Console](https://adminconsole.adobe.com/) 才能開始使用新沙盒。 請參閱 [管理產品配置檔案的權限](../../access-control/ui/permissions.md) 有關如何將沙盒設定到產品配置檔案的資訊。

使用以下視頻快速概述如何在Experience Platform中使用「沙箱」。

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

要建立新沙盒，請選擇 **[!UICONTROL 建立沙盒]** 在螢幕右上角。

![建立沙盒](../images/ui/create-sandbox.png)

的 **[!UICONTROL 建立沙盒]** 對話框。 如果要建立開發沙箱，請選擇 **[!UICONTROL 開發]** 的下界。 要建立新的生產沙盒，請選擇 **[!UICONTROL 生產]**。

![沙盒類型](../images/ui/sandbox-type.png)

選擇類型後，請為沙盒提供名稱和標題。 標題應具有人類可讀性，並應具有足夠的描述性，以便容易識別。 沙盒名稱是用於API調用的全小寫標識符，因此應是唯一和簡潔的。 沙盒名稱必須以字母開頭，最多包含256個字元，並且只包含字母數字字元和連字元(-)。

完成後，選擇 **[!UICONTROL 建立]**。

![沙盒資訊](../images/ui/sandbox-info.png)

建立完沙盒後，刷新頁面，新沙盒將出現在 **[!UICONTROL 沙箱]** 狀態為「」的儀表板[!UICONTROL 建立]。 新沙箱需要大約30秒才能由系統設定，之後它們的狀態將更改為「[!UICONTROL 活動]。

![新沙盒](../images/ui/new-sandbox.png)

## 重置沙盒

>[!WARNING]
>
>以下是例外清單，它可阻止您重置預設生產沙盒或用戶建立的生產沙盒： <ul><li>如果沙盒中承載的標識圖也由Adobe Analytics用於 [跨設備分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 的子菜單。</li><li>如果沙盒中承載的標識圖也由Adobe Audience Manager用於 [基於人員的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html)。</li><li>如果預設生產沙盒包含CDA和PBD功能的資料，則無法重置它。</li><li>用戶建立的用於與Adobe Audience Manager或觀眾核心服務進行雙向段共用的生產沙盒可以在警告消息後重置。</li></ul>

重置生產沙盒或開發沙盒將刪除與該沙盒（架構、資料集等）關聯的所有資源，同時維護沙盒的名稱和關聯權限。 此「乾淨」沙盒繼續以同一名稱可供有權訪問它的用戶使用。

從沙箱清單中選擇要重置的沙箱。 在顯示的右導航面板中，選擇 **[!UICONTROL 沙盒重置]**。

![重置](../images/ui/reset.png)

將出現一個對話框，提示您確認您的選擇。 選擇 **[!UICONTROL 繼續]** 繼續。

![重置警告](../images/ui/reset-warning.png)

在最終確認窗口中，在對話框中輸入沙盒的名稱並選擇 **[!UICONTROL 重置]**。

![重置確認](../images/ui/reset-confirm.png)

## 刪除沙盒

>[!WARNING]
>
>無法刪除預設的生產沙盒。 但是，任何用戶建立的用於雙向段共用的生產沙盒 [!DNL Audience Manager] 或 [!DNL Audience Core Service] 可以在出現警告消息後刪除。

刪除生產沙盒或開發沙盒將永久刪除與該沙盒關聯的所有資源，包括權限。

從沙箱清單中選擇要刪除的沙箱。 在顯示的右導航面板中，選擇 **[!UICONTROL 刪除]**。

![delete](../images/ui/delete.png)

將出現一個對話框，提示您確認您的選擇。 選擇 **[!UICONTROL 繼續]** 繼續。

![刪除警告](../images/ui/delete-warning.png)

在最終確認窗口中，在對話框中輸入沙盒的名稱並選擇  **[!UICONTROL 繼續]**。

![刪除確認](../images/ui/delete-confirm.png)

## 後續步驟

本文檔演示了如何在Experience PlatformUI中管理沙箱。 有關如何使用沙盒API管理沙盒的資訊，請參見 [沙盒開發人員指南](../api/getting-started.md)。
