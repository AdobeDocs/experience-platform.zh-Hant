---
keywords: Experience Platform；首頁；熱門主題；標籤身分
title: 在UI中將欄位標示為身分
description: 包含個人識別資訊(PII)的欄位可標示為身分欄位。 身分欄位中提供的值會由Identity Service解譯為身分。 身分的名稱空間是在標示欄位時指定的。
hide: true
hidefromtoc: true
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 0d111241658b4014d1ca2e6013d21a4782d81be9
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# 在UI中將欄位標示為身分

包含個人識別資訊(PII)的欄位可標示為身分欄位。 [!DNL Identity Service]會將識別欄位中提供的值解譯為識別。 身分的名稱空間是在標示欄位時指定的。

欄位必須符合下列條件，才能標示為身分：

* 只有字串型別欄位可用於身分
* 身分只能在記錄和時間序列資料中識別
* 只有PII欄位應該標示為身分。 選擇代表較通用資料的欄位可能會導致關係較不精確，並且可能導致從身分圖表存取相關身分時發生錯誤

如需如何在UI中標籤身分欄位的指示，請參閱[在UI中定義身分欄位的指南](../xdm/ui/fields/identity.md)。

## 後續步驟

如需有關 [!DNL Identity Service] 的詳細資訊，請參閱 [[!DNL Identity Service]  概觀](./home.md)。
