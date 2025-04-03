---
keywords: Experience Platform；首頁；熱門主題；分段；區段比對；區段比對
solution: Experience Platform
title: 區段比對常見問題集
description: 「區段比對」是Adobe Experience Platform中的區段共用服務，可讓兩位或更多Experience Platform使用者以安全、受規管且有利於隱私權的方式交換區段資料。
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# [!DNL Segment Match]常見問題

本指南針對Adobe Experience Platform區段比對的隱私權與法律問題，提供常見問答集。

## 預估重疊期間會共用哪些資料，以及Adobe如何確保安全地取得這些量度？

![overlap-report.png](./images/overlap-report.png)

沒有在沙箱間移動客戶或區段資料以取得這些重疊預估量度。 任何指定沙箱中客戶選取的預先雜湊適用身分，會新增至機率資料結構，其中ID本身會以雜湊格式表示。

此為單向流程，表示原始的預先雜湊識別碼不會公開，且無法進行反向工程。

這些資料結構具有獨特的屬性，可讓工程在它們之間執行聯集和交集作業，即使編碼的資訊被嚴格壓縮或雜湊亦然。 這些作業允許[!DNL Segment Match]取得兩個資料結構的預估交集，由兩個不同沙箱的ID組成，而不需要比較實際值。 由於[!DNL Segment Match]僅使用資料結構，因此ID絕對不會離開其個別組織的設定檔儲存區以進行估計。 這可讓Adobe符合客戶的隱私權及安全性需求，同時提供高度精確的估計工具，以指導資料共同作業協定。

## 指定哪些身分會收到共用區段ID的程式為何？

[!DNL Segment Match]為客戶提供設定要在服務中使用的名稱空間的選項。 如果客戶決定發佈摘要至合作夥伴沙箱，此選取範圍會套用至先前問題中所述的預估程式與資料傳輸程式。

兩個不同組織加密的身分之間的資料傳輸程式會在中立的計算環境中執行。 資料傳輸工作歸Adobe所有，參與夥伴關係的組織無權存取此環境，也無法存取任何可能是資料傳輸工作結果的記錄。

只有區段會籍會內嵌到接收者組織的重疊設定檔片段中，並且不會從傳送者組織向接收者組織傳輸額外的身分。 資料傳輸工作不會讀取純文字的個人識別資訊(PII)，因為[!DNL Segment Match]只允許在資料為PII時，在SHA256加密的名稱空間（電子郵件/電話）上重疊。 運算環境中絕不會儲存結果。
