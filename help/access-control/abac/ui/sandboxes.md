---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制管理沙箱
description: 透過Adobe Experience Cloud中的許可權介面管理沙箱。
exl-id: c21eb319-fc0d-442a-b778-bbfa2d6bb22d
source-git-commit: 8c9503c9923372ef919d485d4ec0e3ebda5a2413
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 16%

---

# 管理沙箱 {#mange-sandboxes}

>[!CONTEXTUALHELP]
>id="platform_permissions_sandboxes_about"
>title="什麼是沙箱？"
>abstract="沙箱是 Experience Platform 單一執行個體內的虛擬分割。沙箱內所有內容及所採取的動作僅能在該沙箱中運作，而不會影響其他沙箱。沙箱的存取權按照角色進行管理。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sandbox/home" text="沙箱概觀"

沙箱是單一Adobe Experience Platform執行個體中的虛擬分割區，可順暢整合您數位體驗應用程式的開發流程。 在沙箱內採取的所有內容和動作都僅限於該沙箱，不會影響任何其他沙箱。 如需沙箱的詳細資訊，請參閱[沙箱概觀](../../../sandboxes/home.md)。

## 探索沙箱 {#explore-sandboxes}

若要檢視沙箱的詳細資訊和相關角色，請在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中導覽至](https://experience.adobe.com/){target="_blank"}。 從左側面板的&#x200B;**[!UICONTROL Sandboxes]**&#x200B;區段中選取&#x200B;**[!UICONTROL Resources]**。

隨即顯示貴組織沙箱的清單。 從清單中選取您要檢視的沙箱。 或者，您也可以將沙箱名稱輸入搜尋列中來搜尋沙箱，或選取篩選圖示（![篩選圖示](../../../images/icons/filter.png)）並使用&#x200B;**[!UICONTROL Sandbox Type]**&#x200B;下拉式功能表來依型別篩選沙箱。

![許可權內的沙箱工作區。](../../images/ui/sandboxes/sandboxes-overview.png){zoomable="yes"}

>[!NOTE]
>
>許可權中的沙箱工作區不允許任何沙箱管理動作。 若要管理沙箱，請從工作區的右上角選取&#x200B;**[!UICONTROL Open sandbox manager]**&#x200B;選項。

**[!UICONTROL Details]**&#x200B;索引標籤提供沙箱的概觀。 總覽會顯示沙箱的&#x200B;**[!UICONTROL Title]**、**[!UICONTROL Sandbox Name]**、**[!UICONTROL Type]**、**[!UICONTROL Region]**、**[!UICONTROL Modified]**&#x200B;日期、**[!UICONTROL Modified by]**&#x200B;和&#x200B;**[!UICONTROL Status]**。

![沙箱的詳細資料工作區。](../../images/ui/sandboxes/sandbox-details.png){zoomable="yes"}

選取&#x200B;**[!UICONTROL Roles]**&#x200B;索引標籤以檢視指派給沙箱的角色。 選取角色會將您帶往角色的工作區。

<!-- To manage the role's sandboxes, follow the [](./roles.md) guide. -->

![沙箱的角色工作區。](../../images/ui/sandboxes/sandbox-roles.png){zoomable="yes"}


## 後續步驟

您現在知道如何檢視沙箱的詳細資訊和角色。 若要深入瞭解屬性型存取控制，請參閱[屬性型存取控制總覽](../overview.md)。
