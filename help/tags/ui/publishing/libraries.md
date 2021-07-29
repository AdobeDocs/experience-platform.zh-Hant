---
title: 程式庫
description: 了解標籤程式庫的概念，以及它們在Adobe Experience Platform中的運作方式。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 59%

---

# 程式庫

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

程式庫是擴充功能、資料元素和規則部署後彼此間互動方式的一組指示。建立程式庫時，您需指定要對程式庫進行的變更。在建置期間，這些變更會與先前程式庫中已提交、核准或發佈的所有內容結合。

程式庫的功能包含新增或移除以下項目：

* 規則
* 元素
* 擴充功能組態

必須先將程式庫指派給環境，才能將其編譯到組建中。核准或拒絕是以程式庫整體為單位。您無法單獨核准或拒絕程式庫內的個別項目。逐步通過發佈工作流程期間，程式庫會在多個環境間移動。

## 建立程式庫 {#create-a-library}

若要建立程式庫，請完成下列步驟。

1. 開啟[!UICONTROL Publishing]標籤。

   [!UICONTROL 發佈]頁面會列出開發程式庫，並提供工具來提交以進行核准、將其移至測試環境，或發佈至生產環境。

1. 選擇&#x200B;**[!UICONTROL 添加新庫]**。

   ![](../../images/library-create.jpg)

1. 為程式庫命名。
1. 將程式庫指派至開發環境。
1. 對程式庫新增變更。若要新增項目，請選取「**[!UICONTROL 新增變更]**」，然後選擇您要新增的項目。 任何經過編輯或已刪除的項目，都可以新增至選擇的程式庫。

   ![](../../images/library-add-change.jpg)

   您可以將下列項目新增至程式庫：

   * 規則
   * 資料元素
   * 擴充功能組態

1. 要添加已更改的任何資源，請選擇&#x200B;**[!UICONTROL 添加所有已更改的資源]**。
1. 選擇&#x200B;**[!UICONTROL Save]**&#x200B;或&#x200B;**[!UICONTROL Save and Build for Development]**。

   進行部署會編譯組建，並將其部署至指派的環境。

程式庫建立後，請從該程式庫的下拉式選單中選取下列任一選項：

* **編輯**:此選項可讓您變更程式庫組態。

* **建置以供開發**:此選項會編譯組建，並將其部署至指派的環境。

* **提交以進行核准**:此選項可讓核准者將程式庫移至發佈程式的下一個步驟。

* **刪除**:此選項會從發佈程式中移除目前選取的程式庫。

![](../../images/library-menu.png)

## 新增至程式庫 {#add-to-a-library}

若要新增至程式庫，請完成下列步驟。

1. 安裝您要新增的[擴充功能](../managing-resources/extensions/overview.md)。
1. 建立您要新增的[資料元素](../managing-resources/data-elements.md)和規則。
1. 開啟&#x200B;**[!UICONTROL Publishing]**&#x200B;標籤。
1. 選擇要更改的[library](libraries.md)，然後選擇&#x200B;**[!UICONTROL Edit]**。
1. 使用規則、資料元素和擴充功能按鈕，選取要新增至程式庫的項目。
1. 儲存變更。

程式庫的變更會顯示在「程式庫內容」變更記錄檔中。

>[!NOTE]
>
> 資料元素取決於擴充功能。規則取決於資料元素和擴充功能。若您未納入程式庫中所有必要的元件，建置期間組建將會失敗，而且您必須先新增必要的元件，才能完成成功的組建。未來版本會在對程式庫進行變更時檢查相依性。

## 從程式庫中移除

若要從程式庫移除某些項目，您必須先停用該項目，然後再發佈停用狀態。

1. 停用您要移除的擴充功能，以及任何依賴這些擴充功能的資料元素和規則。
1. 停用您要移除的資料元素和規則。
1. 開啟&#x200B;**[!UICONTROL Publishing]**&#x200B;標籤。
1. 選取您要變更的程式庫。
1. 使用規則、資料元素和擴充功能按鈕，選取要從程式庫中移除的停用項目。
1. 儲存變更。

## 管理程式庫變更

要編輯庫選項，請完成以下步驟。

1. 選擇一個庫，然後選擇&#x200B;**[!UICONTROL Edit]**&#x200B;以查看庫更改。 所有變更都會顯示在[!UICONTROL 程式庫內容]清單中。

   ![](../../images/library-contents.jpg)

1. 選取變更即可檢視並選取修訂項目。

   ![](../../images/library-contents-revision.jpg)

1. 選擇是顯示&#x200B;**All**&#x200B;項目還是顯示&#x200B;**Changed**&#x200B;項目。
1. 選擇修訂，然後選擇&#x200B;**[!UICONTROL 選擇修訂]**。
1. 選擇「**[!UICONTROL 添加更改]**」或「**[!UICONTROL 添加所有更改的資源]**」。

## 作用中程式庫 {#active-library}

程式庫會封裝您想對已部署的程式碼進行的一組變更。作用中程式庫讓這項工作變得更輕鬆，您可以快速重複變更及查看影響。

擴充功能、規則和資料元素現在可直接儲存至您使用的程式庫。 如有需要，您也可以從[!UICONTROL Active Library]下拉式清單中建立新組建，甚至建立新程式庫。

下列清單提供管理使用中程式庫的詳細資訊。

1. [建立新程式庫](libraries.md#create-a-library)。
1. 前往[規則](../managing-resources/rules.md)、[資料元素](../managing-resources/data-elements.md)或[擴充功能](../managing-resources/extensions/overview.md)。
1. 選取您的作用中程式庫。
1. 進行變更，然後儲存並建置程式庫。
1. 測試您的變更，然後視需要重複這些步驟。
