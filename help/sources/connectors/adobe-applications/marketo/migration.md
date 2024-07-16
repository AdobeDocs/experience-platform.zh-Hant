---
title: 使用Marketo Engage來源將ECID對應從人員移轉至活動
description: 瞭解如何使用Marketo Engage來源，將ECID對應從人員資料集移轉至活動資料集。
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 將ECID對應從[!DNL Person]資料集移轉至[!DNL Activity]資料集

您可以將ECID對應從[!DNL Marketo Engage Person]資料集移轉至[!DNL Activity]資料集，以提供更穩定的資料擷取和身分管理行為。 此外，此移轉會處理下列問題：

| 問題 | 解決方案 |
| --- | --- |
| 當您的[!DNL Marketo Person]資料集具有多個ECID的連結時，當Experience Data Model (XDM)記錄中的[身分總數超過20](../../../../identity-service/guardrails.md)時，資料擷取會失敗。 | 將ECID欄位對應移轉到[!DNL Activity]，您可以確保來自[!DNL Marketo Person]資料流程的身分數量保持在限制內，從而允許資料擷取成功。 |
| 每次使用ECID擷取[!DNL Marketo Person]資料集時，[!DNL Marketo Person]資料集中所有ECID的時間戳記都會以人員記錄的最後更新時間戳記更新。 這可能會導致[不正確刪除身分圖表](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated)中最近的身分。 | 藉由將ECID欄位對應移轉至[!DNL Activity]，Identity Service可正確反映ECID的時間戳記，而Identity Service的「先進先出」機制可提供更穩定的行為。 |
| 透過[!DNL Marketo Person]資料流擷取ECID時，新新增的ECID不會擷取到Experience Platform中，除非[!DNL Marketo]中的[!DNL Person]記錄有更新。 | 當新的ECID連結至[!DNL Marketo]中的[!DNL Person]記錄時，您可以透過[!DNL Marketo Activity]資料流擷取該ECID資料，並在Experience Platform時立即提示身分圖表更新。 |

基本上，您必須：

* 更新您的[!DNL Marketo Activity]資料流。
* 更新您的[!DNL Marketo Person]資料流。

## 更新[!DNL Marketo Activity]資料流 {#update-activity-dataflow}

請依照下列步驟更新您的[!DNL Marketo Activity]資料流：

* 在Experience PlatformUI中，導覽至&#x200B;*來源*&#x200B;工作區，並尋找您現有的[!DNL Marketo Activity]資料流。
* 假設資料流已啟用，請選取資料流名稱旁邊的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 更新資料流]**。
* 接著，選取&#x200B;**[!UICONTROL 下一步]**，直到您到達&#x200B;*對應*&#x200B;介面為止。
* 在&#x200B;*對應*&#x200B;介面中，選取&#x200B;**[!UICONTROL 新增欄位]**，然後選取&#x200B;**[!UICONTROL 新增計算欄位]**。 您必須從此新增下列專案：

| Source資料集 | xdm目標欄位 |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>如果您對現有[!DNL Marketo]資料流程的更新僅包含新增或移除ECID對應欄位，則資料流程會自動略過歷史回填作業。 只有在發生「造訪網頁」和「點按網頁」等活動型別時，才會發生新資料擷取。

## 更新[!DNL Marketo Person]資料流 {#update-person-dataflow}

請依照下列步驟更新您的[!DNL Marketo Person]資料流：

* 在Experience PlatformUI中，導覽至&#x200B;*來源*&#x200B;工作區，並尋找您現有的[!DNL Marketo Person]資料流。
* 假設資料流已啟用，請選取資料流名稱旁邊的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 更新資料流]**。
* 接著，選取&#x200B;**[!UICONTROL 下一步]**，直到您到達&#x200B;*對應*&#x200B;介面為止。
* 在&#x200B;*對應*&#x200B;介面中，移除對應至`identityMap`的計算欄位，然後選取&#x200B;**[!UICONTROL 下一步]**&#x200B;和&#x200B;**[!UICONTROL 儲存與擷取]**。

>[!NOTE]
>
>如果您對現有[!DNL Marketo]資料流程的更新僅包含新增或移除ECID對應欄位，則資料流程會自動略過歷史回填作業。 先前已擷取的ECID時間戳記將維持不變。 只有在擷取與現有ECID對應的新資料時，才會更新這些ID。

## 後續步驟

閱讀本檔案後，您現在便知道如何將ECID對應從[!DNL Marketo Person]資料集移轉至[!DNL Marketo Activity]資料集。 如需詳細資訊，請閱讀下列[!DNL Marketo]份檔案：

* [建立資料流以擷取 [!DNL Marketo] 資料至Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md)。
* [欄位對應指南](../mapping/marketo.md)。
