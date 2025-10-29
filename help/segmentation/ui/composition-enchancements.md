---
title: 對象構成增強功能
description: 瞭解透過對象擴充和更快啟動對對象構成進行的增強功能。
hide: true
hidefromtoc: true
source-git-commit: 065990790307124e0992731139abe9641a742a1b
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# 對象構成增強功能

您現在可以存取對象構成的&#x200B;**兩個**&#x200B;增強功能：

- [對象擴充](#audience-enrichment)
- [更快速的啟動](#faster-activation)

## 對象擴充 {#audience-enrichment}

對象擴充可讓您輸出值陣列，讓您的設定檔符合您建立的對象資格。

若要在構成中新增對象擴充，請選取畫布中最上方的&#x200B;**[!UICONTROL Audience]**&#x200B;區塊。 在提供對象名稱后，選取「**[!UICONTROL Build rule]**」以開啟規則產生器畫布。

![已醒目提示「對象」區塊以及「建置規則」按鈕。](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

規則產生器畫布隨即顯示。 您現在可以為對象擴充建立篩選條件。 此篩選條件&#x200B;**必須**&#x200B;包含陣列中的屬性。 陣列屬性取決於您組織的結構描述結構。 建立篩選條件後，在右側面板中選取&#x200B;**[!UICONTROL Delivery]**。

![規則產生器畫布顯示可以擴充對象的範例。 傳遞按鈕也會反白顯示。](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

從左側面板的清單中，選擇您要用來擴充的物件陣列。 如果設定檔上只有一個陣列，則會自動為您選取該陣列。 選取&#x200B;**[!UICONTROL Save]**&#x200B;以返回對象構成。

<!-- , as well as the fields you want to be used in the enrichment. -->

![顯示擴充樹狀結構的結構樹狀結構。](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

在對象構成中，您的[!UICONTROL Audience]區塊現在是&quot;[!UICONTROL Rule builder with enhancement]&quot;型別。 選取&#x200B;**[!UICONTROL Publish]**&#x200B;以啟動下一個每日批次的對象。

![已強調顯示「對象」區塊，顯示已新增擴充的對象。](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### 行為詳細資訊和護欄

使用對象擴充時，請謹記下列詳細資訊和護欄：

- 您只能在對象構成中建立的對象內使用對象擴充
- 構成&#x200B;**中使用的第一個區塊必須**&#x200B;是以規則為基礎的對象。
- 您&#x200B;**無法**&#x200B;在構成中使用任何其他作業。
- 發佈後，您&#x200B;**無法**&#x200B;在規則型對象上編輯構成。

   - 如果想要變更基本構成或規則型對象，您可以&#x200B;*將構成*&#x200B;複製到草稿並編輯草稿。

- 僅&#x200B;**one**&#x200B;物件陣列可用於在單一對象內產生擴充裝載

   - 承載陣列可以巢狀內嵌於物件中（在設定檔結構描述中最多七個層），但&#x200B;**不能包含於另一個陣列中**。
   - 承載陣列&#x200B;**必須**&#x200B;有50列或更少。
   - 承載&#x200B;**中的所有資料行輸出都必須**&#x200B;為基本型別。
   - 只輸出陣列中的前&#x200B;**20**&#x200B;個資料行。

- 目前僅可使用&#x200B;**10**&#x200B;個對象組合

## 更快速的啟動 {#faster-activation}

更快速的啟用可讓您在評估構成後立即將對象啟用到下游目的地。 因此，如果您的目的地設定為在區段評估後啟動，您就不需要再等待24小時完成評估工作。

如需詳細資訊，請參閱[啟用批次設定檔目的地的對象指南](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)。
