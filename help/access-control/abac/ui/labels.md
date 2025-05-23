---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制管理標籤
description: 本檔案提供透過Adobe Experience Cloud中的許可權介面管理標籤的資訊
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 24%

---

# 管理標籤

>[!NOTE]
>
>若要使用包含指定標籤的欄位來建立或檢視計算屬性，您必須擁有該標籤的存取權。

標籤可讓您根據套用至該資料的使用和存取原則，將資料集和欄位分類。 標籤可隨時套用，提供您選擇控管資料方式的靈活性。 最佳實務建議在資料內嵌至Experience Platform後立即加上標籤，或資料可在Experience Platform中使用後立即加上標籤。

## 建立新標籤 {#create-new-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="標籤使用"
>abstract="您可以使用自訂標籤，將資料控管和存取權控制的設定套用至您的資料。"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="建立新標籤"
>abstract="您可以建立適合您組織需求的自訂標籤。自訂標籤可用於資料控管和存取控制設定套用到您的資料。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=zh-Hant#manage-labels" text="管理自訂標籤"

>[!NOTE]
>
>整個組織只有一個標籤清單。 若要建立自訂標籤，您需要在生產沙箱上有&#x200B;**[!UICONTROL 管理使用標籤]**&#x200B;許可權。 目前不支援刪除標籤。

若要建立新標籤，請選取側邊欄中的&#x200B;**[!UICONTROL 標籤]**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 建立標籤]**。

![flac-new-label](../../images/flac-ui/create-label.png)

**[!UICONTROL 建立新標籤]**&#x200B;對話方塊隨即顯示，提示您輸入名稱、選用的易記名稱和選用的說明。

![new-label-info](../../images/flac-ui/new-label-info.png)

完成後，選取&#x200B;**[!UICONTROL 確認]**。
