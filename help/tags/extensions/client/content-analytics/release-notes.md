---
title: Adobe Content Analytics擴充功能發行說明
description: Adobe Experience Platform中Content Analytics標籤擴充功能的最新發行說明。
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 057d1ad8d61ed386a777175026a3f01f21541389
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---

# Adobe Content Analytics擴充功能發行說明

以下為Content Analytics標籤擴充功能的發行說明清單。

| 版本 | 日期 | 修正 |
|---|---|---|
| 1.0.52 | 2026年4月27日 | <ul><li>新增CSS在DOM中元素背景中載入影像的資產追蹤。</li><li>已新增硬式編碼的`permanentlyBlockedURLs`陣列，其中包含[maps.googleapis.com](https://maps.googleapis.com)和[mapsresources-pa.googleapis.com](https://mapsresources-pa.googleapis.com)。 Content Analytics資料庫中預設一律會封鎖這些URL。</li><li>已新增`idSource`和`channel`欄位至XDM資料收集要求。</li></ul> |
| 1.0.51 | 2026年3月13日 | <ul><li>修正可能導致在頁面之間導覽時快取`experienceIDs`的次要錯誤。</li><li>修正體驗查詢字串引數擷取的問題。 查詢引數的功能如下：<ul><li>查詢引數欄位是空的：體驗ID中未擷取任何查詢字串引數。</li><li>查詢引數是明確定義的（例如，一、二、三）：只有那些查詢字串引數和值會擷取到體驗ID中。</li><li>查詢引數已設定為萬用字元(`.*`)：整個document.location.search字串包含在URL中。</li></ul></li></ul> |
| 1.0.49 | 2025年9月12日 | <ul><li>修正使用者沒有資料流許可權時，標籤擴充功能UI無法載入的次要錯誤。 UI現在將在&#x200B;**[!UICONTROL Choose from list]**&#x200B;資料流選項中顯示許可權警告，並且仍允許使用者手動輸入值。</li><li>更新l10n的路徑問題。</li><li>修正了屬於非影像父項之子元素的某些影像未正確擷取這些子影像元素的資產點選數的問題。</li><li>如果使用者的WebSDK設定於標籤中，而該標籤與`alloy`具有不同的執行個體名稱，則Content Analytics程式庫將會偵測WebSDK程式庫的第一個執行個體，並使用它來傳送Content Analytics事件。</li></ul> |
| 1.0.48 | 2025年8月25日 | <ul><li>新增在檔案的陰影根DOM元素中追蹤資產的支援。</li></ul> |
| 1.0.47 | 2025年7月23日 | <ul><li>修正未啟用體驗時所發生的錯誤，此錯誤會導致體驗的規則運算式檢查失敗。 此問題會導致無法收集Content Analytics資料。</li><li>解決預設語言設定無法向某些未在Experience Cloud中設定主要預設語言的使用者顯示標籤UI的問題。</li></ul> |
| 1.0.46 | 2025年6月18日 | <ul><li>已新增在嘗試儲存擴充功能設定時（如果生產資料流不存在）的toast通知。</li><li>暫時修正Content Analytics裝載的可見度問題，方法是將字串化的裝載內容改為置於主控台。</li><li>新增擴充功能UI的本地化支援。</li><li>部分修正CSS問題，此問題導致擴充功能UI內容周圍出現額外邊框間距。</li></ul> |
| 1.0.45 | 2025年4月14日 | <ul><li>已解決在等待頁面檢視事件時與保留Content Analytics事件相關的組態設定中的幾個錯誤。 Content Analytics現在預設會等到第一個頁面檢視事件發生後再引發事件。</li></ul> |
| 1.0.44 | 2025年3月31日 | <ul><li>AppMeasurement整合的第一個反複專案。</li><li>此版本尚不支援篩選特定請求（例如頁面檢視），但此功能可在未來的更新中新增。 其目前使用在頁面上找到的第一個AppMeasurement執行個體。</li></ul> |
| 1.0.43 | 2025年3月10日 | <ul><li>初始擴充功能發行。</li></ul> |
