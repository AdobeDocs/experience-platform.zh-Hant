---
title: Capillary Streaming Events概述
description: 瞭解如何將資料從Capillary串流至Experience Platform。
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>[!DNL Capillary Streaming Events]來源是測試版。 閱讀來源概觀中的[條款與條件](../../home.md#terms-and-conditions)，以取得有關使用測試版標籤之來源的詳細資訊。

[!DNL Capillary Technologies]是領先的忠誠度和參與平台，受到全球300多個品牌的信任。 使用[!DNL Capillary Streaming Events]來源讓您的企業可以順暢地從[!DNL Capillary]將客戶設定檔、忠誠度資料和交易事件串流到Adobe Experience Platform。 連線您的[!DNL Capillary]來源以啟用即時個人化、進階對象細分和全通路行銷活動策劃。

將[!DNL Capillary]與Experience Platform整合後，您可以：

* 即時同步&#x200B;**忠誠度點數、層級和獎勵**。
* 將&#x200B;**異動資料**&#x200B;傳送到Experience Platform以進行分析和啟用。
* 運用Real-Time CDP、Experience Platform和Adobe Journey Optimizer進行細分、歷程協調和個人化。

## 先決條件

在將[!DNL Capillary]連線至Adobe Experience Platform之前，請確定您具備下列條件：

* 有效的&#x200B;**Adobe組織ID**&#x200B;和啟用Experience Platform沙箱的存取權。
* 您必須同時為您的帳戶啟用&#x200B;**[!UICONTROL 檢視來源]**&#x200B;和&#x200B;**[!UICONTROL 管理來源]**&#x200B;許可權，才能將您的[!DNL Capillary]帳戶連線至Experience Platform。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/ui/overview.md)。

### 建立結構描述

您必須建立Experience Data Model (XDM)結構描述來說明資料集，該資料集可以儲存將從[!DNL Capillary]傳送的可能欄位和資料型別。

1. 登入Adobe Experience Platform，並透過您組織的登入存取Experience Platform。
2. 在左側導覽面板中，選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;以開啟[!UICONTROL 結構描述]工作區。
3. 選取右上角的&#x200B;**[!UICONTROL 建立結構描述]**。
4. 在建立結構描述對話方塊中，挑選介於&#x200B;**[!UICONTROL 手動建立]** （自行新增欄位和欄位群組）或&#x200B;**[!UICONTROL ML輔助建立]** （上傳CSV檔案並使用機器學習來產生建議的結構描述）。
5. 為您的結構描述選擇基底類別（例如XDM個別設定檔、XDM ExperienceEvent或其他）。 如果您選取&#x200B;**[!UICONTROL 其他]**，則可以從可用的自訂或標準類別中選取。
6. 輸入結構描述的人類易記名稱和說明。
7. 使用結構描述編輯器：新增欄位群組（可重複使用的欄位區塊）、定義個別欄位（自訂名稱、資料型別和選項），以及選擇性地建立自訂資料型別或欄位群組（如果現有型別或欄位群組不符合您的需求）。
8. 檢閱畫布中的結構描述結構。 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立結構描述。
9. （選用）在結構編輯器中，視需要編輯欄位、新增說明以及調整欄位群組。

如需有關如何建立XDM結構描述的詳細指示，請閱讀[使用結構描述編輯器](../../../xdm/tutorials/create-schema-ui.md)建立結構描述的指南。

### 建立資料集

接下來，您必須建立參照您剛建立的結構描述的資料集。

1. 在Experience Platform UI中，選取左側導覽中的[!UICONTROL 資料集]以開啟[!UICONTROL 資料集]工作區。
2. 選取右上方的&#x200B;**[!UICONTROL 建立資料集]**。
3. 在建立選項中，選取&#x200B;**[!UICONTROL 從結構描述建立資料集]**。
4. 從清單中，搜尋並選取您先前建立的XDM結構描述。 找到結構描述後，請選取&#x200B;**[!UICONTROL 下一步]**。
5. 為您的資料集輸入唯一的描述性名稱。
6. 可選擇新增說明，協助未來的使用者識別資料集。
7. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立資料集。

如需如何建立資料集的詳細說明，請參閱[資料集UI指南](../../../catalog/datasets/user-guide.md)。

## 將[!DNL Capillary Streaming Events]連線至Experience Platform

完成[!DNL Capillary]的先決條件設定後，請閱讀[[!DNL Capillary Streaming Events] 使用者介面教學課程](../../tutorials/ui/create/loyalty/capillary.md)，瞭解如何將您的帳戶連線並從[!DNL Capillary]將資料串流至Experience Platform。
