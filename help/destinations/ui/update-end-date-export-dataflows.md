---
title: 更新資料集匯出資料流程的結束日期（2025年5月1日前需要採取行動）
type: Tutorial
hide: true
hidefromtoc: true
description: 瞭解如何將資料集匯出資料流的結束日期更新為2025年5月1日的目前結束日期。
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# 更新資料集匯出資料流程的結束日期（2025年5月1日前需要採取行動）

>[!IMPORTANT]
>
>如果您的組織在2024年9月版本的Experience Platform之前設定資料集匯出資料流，則套用此頁面上的動作專案。

## 發生什麼事？

Experience Platform](/help/release-notes/latest/latest.md#destinations)的2024年9月[日發行版本匯入了設定匯出資料集資料流`endTime`日期的選項。 Adobe也針對2024年9月版本&#x200B;*之前建立*&#x200B;的所有資料集匯出資料流，推出預設結束日期為2025年5月1日。 這些資料流目前顯示的訊息類似於以下所示的訊息。

![需要更新匯出資料集資料流結束日期的UI通知。](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**動作專案**：對於這些資料流中的任一項，您必須在結束日期過期之前手動更新結束日期；否則，您的匯出將會停止。 使用Experience Platform UI來識別哪些資料流預計在2025年5月1日停止。

## 為什麼會收到通知？

您的組織具有的活動資料集匯出資料流，結束日期為2025年5月1日。

## 使用UI更新結束日期

使用Experience Platform UI來識別結束日期為2025年5月1日的資料流，並將其更新到未來的日期。

### 尋找需要更新的資料流

導覽至&#x200B;**目的地>瀏覽**，並在&#x200B;**資料型別**&#x200B;欄中尋找&#x200B;**資料集**&#x200B;資料型別，如下所示。 選取所需的資料流以進行檢查。

![在[瀏覽]索引標籤中反白顯示的資料集匯出資料流。](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### 更新資料流程的結束日期

若要更新資料流程的結束日期：

1. 在上一步選取要檢查的資料流中，選取&#x200B;**匯出資料集**。
   ![匯出資料集控制項在[瀏覽]索引標籤中反白顯示。](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. 在工作流程中，繼續進行&#x200B;**排程**&#x200B;步驟並選取&#x200B;**編輯排程**。
   ![編輯排程步驟中反白顯示的排程控制項。](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. 在2025年5月1日之後選擇想要的結束日期，並選取&#x200B;**儲存**。
   ![選取排程步驟中反白顯示的結束日期控制項。](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. 繼續工作流程結尾並儲存您的更新。

如需排程步驟的詳細資訊，請參閱[匯出資料集UI教學課程](/help/destinations/api/export-datasets.md#scheduling)。

## 使用API更新結束日期

### 尋找需要更新的資料流

### 更新資料流程的結束日期
