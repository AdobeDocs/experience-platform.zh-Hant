---
title: 天氣資料欄位對應
description: 可用天氣資料欄位的參考頁面，這些欄位會以和 The Weather Channel 整合的一部分提供。
exl-id: bc0f158b-f9d0-424a-aa21-953e8380473f
source-git-commit: e2122008fcae1016db03d6b5f56e4fa25520f9d0
workflow-type: tm+mt
source-wordcount: '12787'
ht-degree: 100%

---

# 天氣資料欄位對應

Adobe 已和 [!DNL [The Weather Company]](https://www.ibm.com/weather) 合作，將美國天氣的附加內容引進透過資料流收集的資料中。您可以在 Experience Platform 中使用此資料進行分析、目標定位和區段建立。

此頁面會列出可用於擴充對象資料的所有可用欄位。

這些欄位會分解為和欄位群組對齊的三個不同群組。

* [**[!UICONTROL 目前的天氣]**](#current-weather)：根據使用者的位置提供目前的天氣狀況。其中包括目前的溫度、降水量、雲量等。
* [**[!UICONTROL 預報的天氣]**](#forecast)：預報內容包括使用者所在位置的 1、2、3、5、7、10 天預報。
* [**[!UICONTROL 觸發因素]**](#triggers)：觸發因素指對應至不同語義天氣狀況的特定組合。有三種不同類型的天氣觸發因素：

   * **[!UICONTROL 相對觸發因素]**：具有語義意義的狀況，例如寒冷或下雨的天氣。這些在不同氣候下的定義可能有所不同。
   * **[!UICONTROL 產品觸發因素]**：會導致購買不同類型產品的狀況。例如：寒冷天氣的預報可能表示購買雨衣的可能性提高了。
   * **[!UICONTROL 惡劣天氣觸發因素]**：惡劣天氣的警告，例如冬季暴風雨或颶風警告。

## 目前的天氣 {#current-weather}

根據使用者所在位置的目前天氣狀況。

| 欄位 | 說明 | XDM 路徑 |
| --- | ---- | --- |
| [!UICONTROL 攝氏露點溫度] | 空氣必須在定壓下冷卻才能達到飽和的溫度。露點也能用於間接測量空氣濕度。露點絕不會超過溫度。當露點和溫度相等時，通常會形成雲朵或霧氣。溫度和露點的值越接近，相對濕度越高。範圍：-80 至 100 (°F) 或 -62 至 37 (°C)。溫度 (攝氏度數) | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 華氏露點溫度] | 空氣必須在定壓下冷卻才能達到飽和的溫度。露點也能用於間接測量空氣濕度。露點絕不會超過溫度。當露點和溫度相等時，通常會形成雲朵或霧氣。溫度和露點的值越接近，相對濕度越高。範圍：-80 至 100 (°F) 或 -62 至 37 (°C)。溫度 (華氏度數) | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 最後一小時降水量 (英吋)] | 滾動小時液體降落量。顯示的量為直到要求時間 (現在) 的滾動時間。降水量 (英吋) | `weather.current.precip1Hour.inches` |
| [!UICONTROL 最後一小時降水量 (公釐)] | 滾動小時液體降落量。顯示的量為直到要求時間 (現在) 的滾動時間。降水量 (公釐) | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 滾動二十四小時液體降落量。顯示的量為直到要求時間 (現在) 的滾動時間。降水量 (英吋) | `weather.current.precip24Hour.inches` |
| [!UICONTROL 最後 24 小時降水量 (公釐)] | 滾動二十四小時液體降落量。顯示的量為直到要求時間 (現在) 的滾動時間。降水量 (公釐) | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 最後 6 小時降水量 (英吋)] | 滾動六小時液體降落量。顯示的量為直到要求時間 (現在) 的滾動時間。降水量 (英吋) | `weather.current.precip6Hour.inches` |
| [!UICONTROL 最後 6 小時降水量 (公釐)] | 滾動六小時液體降落量。顯示的量為直到要求時間 (現在) 的滾動時間。降水量 (公釐) | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 壓力變化] | 過去三小時的壓力變化 (毫巴)。 | `weather.current.pressureChange` |
| [!UICONTROL 平均海平面壓力] | 平均海平面壓力 (毫巴)。換句話說，海平面的平均氣壓。<br>範圍：毫巴，精確到 1/10 mb。 | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 相對濕度] | 空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：0 到 100。 | `weather.current.relativeHumidity` |
| [!UICONTROL 最後一小時降雪 (公分)] | 一小時降雪量。顯示的量為直到要求時間 (現在) 的滾動時間。降雪量 (公分) | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 最後一小時降雪 (英吋)] | 一小時降雪量。顯示的量為直到要求時間 (現在) 的滾動時間。降雪量 (英吋) | `weather.current.snow1Hour.inches` |
| [!UICONTROL 24 小時降雪 (公分)] | 二十四小時降雪量。顯示的量為直到要求時間 (現在) 的滾動時間。降雪量 (公分) | `weather.current.snow24Hour.centimeters` |
| 24 小時降雪 (英吋) | 二十四小時降雪量。顯示的量為直到要求時間 (現在) 的滾動時間。降雪量 (英吋) | `weather.current.snow24Hour.inches` |
| [!UICONTROL 最後 6 小時降雪 (公分)] | 一小時降雪量。顯示的量為直到要求時間 (現在) 的滾動時間。降雪量 (公分) | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 最後 6 小時降雪 (英吋)] | 一小時降雪量。顯示的量為直到要求時間 (現在) 的滾動時間。降雪量 (英吋) | `weather.current.snow6Hour.inches` |
| [!UICONTROL 日落時間] | 日落時間 (UTC)。 | `weather.current.sunsetTime` |
| [!UICONTROL 攝氏溫度] | 以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.current.temperature.celsius` |
| [!UICONTROL 華氏溫度] | 以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 24 小時的攝氏溫度變化] | 相較於 24 小時前報告的溫度變化。溫度 (攝氏度數) | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 24 小時華氏溫度變化] | 相較於 24 小時前報告的溫度變化。溫度 (華氏度數) | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 攝氏體感溫度] | 表面溫度。這代表由於風寒指數或酷熱指數的綜合效應，暴露在外的人體肌膚上「感覺起來」的空氣溫度。<br>當溫度為 65°F 或更高時，「體感」值即代表計算出的酷熱指數。當溫度低於 65°F 時，「體感」值則代表計算出的風寒指數。<br>範圍：-140 到 140。溫度 (攝氏度數) | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 華氏體感溫度] | 表面溫度。這代表由於風寒指數或酷熱指數的綜合效應，暴露在外的人體肌膚上「感覺起來」的空氣溫度。<br>當溫度為 65°F 或更高時，「體感」值即代表計算出的酷熱指數。當溫度低於 65°F 時，「體感」值則代表計算出的風寒指數。<br>範圍：-140 到 140。溫度 (華氏度數) | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 上午 7 點以來的攝氏最高溫度] | 當地時間上午 7 點以來的最高溫度。溫度 (攝氏度數) | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 上午 7 點以來的華氏最高溫度] | 當地時間上午 7 點以來的最高溫度。溫度 (華氏度數) | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 過去 24 小時的攝氏最低溫度] | 過去 24 小時的最低溫度。24 小時期間指參照要求時間 (現在) 而言。溫度 (攝氏度數) | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 過去 24 小時華氏最低溫度] | 過去 24 小時的最低溫度。24 小時期間指參照要求時間 (現在) 而言。溫度 (華氏度數) | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 風向] | 風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.current.windDirection` |
| [!UICONTROL 每小時的陣風公里數] | 此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 每小時陣風英里數] | 此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.current.windGust.`milesPerHour |
| [!UICONTROL 風速 (每小時公里數)] | 風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 風速 (每小時英里數)] | 風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.current.windSpeed.milesPerHour` |

## 預報的天氣 {#forecast}

根據使用者所在位置的預報天氣 (特定時間點)。

| 欄位 | 說明 | XDM 路徑 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 一天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (攝氏度數) | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 一天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (華氏度數) | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 一天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (攝氏度數) | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 一天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (華氏度數) | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 一天的天氣預報。白天的天氣資訊。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 一天的天氣預報。白天的天氣資訊。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 一天的天氣預報。白天的天氣資訊。降水機率 (百分比)。 | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 一天的天氣預報。白天的天氣資訊。降水的可能形式 (雨、雪、雨夾雪等)。 | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 一天的天氣預報。白天的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 一天的天氣預報。白天的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 一天的天氣預報。白天的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 一天的天氣預報。白天的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 一天的天氣預報。白天的天氣資訊。空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：- 0 到 100。 | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 一天的天氣預報。白天的天氣資訊。潛在大量降雪 (1-3 英吋、3-6 英吋等)。 | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 一天的天氣預報。白天的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 一天的天氣預報。白天的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 一天的天氣預報。白天的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 一天的天氣預報。白天的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 一天的天氣預報。白天的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 一天的天氣預報。白天的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 一天的天氣預報。白天的天氣資訊。影響某個區域的大雷雨機率指數。0 級 (未打雷) 到 5 級 (劇烈大雷雨的高風險)。 | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 一天的天氣預報。白天的天氣資訊。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 一天的天氣預報。白天的天氣資訊。風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 一天的天氣預報。白天的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 一天的天氣預報。白天的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 一天的天氣預報。白天的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 一天的天氣預報。白天的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 一天的天氣預報。夜間的天氣資訊。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 一天的天氣預報。夜間的天氣資訊。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第 1 天預報的夜間降水機率] | 一天的天氣預報。夜間的天氣資訊。降水機率 (百分比)。 | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 一天的天氣預報。夜間的天氣資訊。降水的可能形式 (雨、雪、雨夾雪等)。 | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 一天的天氣預報。夜間的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 一天的天氣預報。夜間的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 一天的天氣預報。夜間的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 一天的天氣預報。夜間的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 一天的天氣預報。夜間的天氣資訊。空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：- 0 到 100。 | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 一天的天氣預報。夜間的天氣資訊。潛在大量降雪 (1-3 英吋、3-6 英吋等)。 | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 一天的天氣預報。夜間的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 一天的天氣預報。夜間的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 一天的天氣預報。夜間的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 一天的天氣預報。夜間的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 一天的天氣預報。夜間的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第 1 天預報的夜間華氏風寒溫度] | 一天的天氣預報。夜間的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第 1 天預報的夜間打雷指數] | 一天的天氣預報。夜間的天氣資訊。影響某個區域的大雷雨機率指數。0 級 (未打雷) 到 5 級 (劇烈大雷雨的高風險)。 | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 第 1 天預報的夜間 UV 指數] | 一天的天氣預報。夜間的天氣資訊。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 第 1 天預報的夜間風向] | 一天的天氣預報。夜間的天氣資訊。風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 第 1 天預報的夜間陣風 (每小時公里數)] | 一天的天氣預報。夜間的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第 1 天預報的夜間陣風 (每小時英里數)] | 一天的天氣預報。夜間的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第 1 天預報的夜間風速 (每小時公里數)] | 一天的天氣預報。夜間的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 1 天預報的夜間風速 (每小時英里數)] | 一天的天氣預報。夜間的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第 1 天預報的 QPF (英吋)] | 一天的天氣預報。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 第 1 天預報的 QPF (公釐)] | 一天的天氣預報。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 第 1 天預報的 QPF 雪量 (公分)] | 一天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第 1 天預報的 QPF 雪量 (英吋)] | 一天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 第 2 天預報的日曆天攝氏最高溫度] | 兩天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (攝氏度數) | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第 2 天預報的日曆天華氏最高溫度] | 兩天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (華氏度數) | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第 2 天預報的日曆天攝氏最低溫度] | 兩天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (攝氏度數) | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第 2 天預報的日曆天華氏最低溫度] | 兩天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (華氏度數) | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第 2 天預報的日雲量 (英里)] | 兩天的天氣預報。白天的天氣資訊。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 第 2 天預報的日雲量 (公里)] | 兩天的天氣預報。白天的天氣資訊。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第 2 天預報的日降水機率] | 兩天的天氣預報。白天的天氣資訊。降水機率 (百分比)。 | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 第 2 天預報的日降水類型] | 兩天的天氣預報。白天的天氣資訊。降水的可能形式 (雨、雪、雨夾雪等)。 | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 第 2 天預報的日 QPF (英吋)] | 兩天的天氣預報。白天的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 第 2 天預報的日 QPF (公釐)] | 兩天的天氣預報。白天的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 第 2 天預報的日 QPF 雪量 (公分)] | 兩天的天氣預報。白天的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第 2 天預報的日 QPF 雪量 (英吋)] | 兩天的天氣預報。白天的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第 2 天預報的日相對濕度] | 兩天的天氣預報。白天的天氣資訊。空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：0 到 100。 | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 第 2 天預報的日雪範圍] | 兩天的天氣預報。白天的天氣資訊。潛在大量降雪 (1-3 英吋、3-6 英吋等)。 | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 第 2 天預報的攝氏日溫度] | 兩天的天氣預報。白天的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 第 2 天預報的華氏日溫度] | 兩天的天氣預報。白天的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第 2 天預報的攝氏日溫度酷熱指數] | 兩天的天氣預報。白天的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第 2 天預報的華氏日溫度酷熱指數] | 兩天的天氣預報。白天的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第 2 天預報的日攝氏風寒溫度] | 兩天的天氣預報。白天的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第 2 天預報的日華氏風寒溫度] | 兩天的天氣預報。白天的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第 2 天預報的打雷指數] | 兩天的天氣預報。白天的天氣資訊。影響某個區域的大雷雨機率指數。0 級 (未打雷) 到 5 級 (劇烈大雷雨的高風險)。 | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 第 2 天預報的日 UV 指數] | 兩天的天氣預報。白天的天氣資訊。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 第 2 天預報的日風向] | 兩天的天氣預報。白天的天氣資訊。風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 第 2 天預報的日陣風 (每小時公里數)] | 兩天的天氣預報。白天的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第 2 天預報的日陣風 (每小時英里數)] | 兩天的天氣預報。白天的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第 2 天預報的日風速 (每小時公里數)] | 兩天的天氣預報。白天的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 2 天預報的日風速 (每小時英里數)] | 兩天的天氣預報。白天的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第 2 天預報的夜間雲量 (英里)] | 兩天的天氣預報。夜間的天氣資訊。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 第 2 天預報的夜間雲量 (公里)] | 兩天的天氣預報。夜間的天氣資訊。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第 2 天預報的夜間降水機率] | 兩天的天氣預報。夜間的天氣資訊。降水機率 (百分比)。 | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 第 2 天預報的夜間降水類型] | 兩天的天氣預報。夜間的天氣資訊。降水的可能形式 (雨、雪、雨夾雪等)。 | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 第 2 天預報的夜間 QPF (英吋)] | 兩天的天氣預報。夜間的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 第 2 天預報的夜間 QPF (公釐)] | 兩天的天氣預報。夜間的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 第 2 天預報的夜間 QPF 雪量 (公分)] | 兩天的天氣預報。夜間的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第 2 天預報的夜間 QPF 雪量 (英吋)] | 兩天的天氣預報。夜間的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第 2 天預報的夜間相對濕度] | 兩天的天氣預報。夜間的天氣資訊。空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：0 到 100。 | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 第 2 天預報的夜間雪範圍] | 兩天的天氣預報。夜間的天氣資訊。潛在大量降雪 (1-3 英吋、3-6 英吋等)。 | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 第 2 天預報的夜間攝氏溫度] | 兩天的天氣預報。夜間的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 第 2 天預報的夜間華氏溫度] | 兩天的天氣預報。夜間的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第 2 天預報的夜間攝氏溫度酷熱指數] | 兩天的天氣預報。夜間的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第 2 天預報的夜間華氏溫度酷熱指數] | 兩天的天氣預報。夜間的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第 2 天預報的夜間攝氏風寒溫度] | 兩天的天氣預報。夜間的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第 2 天預報的夜間華氏風寒溫度] | 兩天的天氣預報。夜間的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第 2 天預報的夜間打雷指數] | 兩天的天氣預報。夜間的天氣資訊。影響某個區域的大雷雨機率指數。0 級 (未打雷) 到 5 級 (劇烈大雷雨的高風險)。 | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 第 2 天預報的夜間 UV 指數] | 兩天的天氣預報。夜間的天氣資訊。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 第 2 天預報的夜間風向] | 兩天的天氣預報。夜間的天氣資訊。風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 第 2 天預報的夜間陣風 (每小時公里數)] | 兩天的天氣預報。夜間的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第 2 天預報的夜間陣風 (每小時英里數)] | 兩天的天氣預報。夜間的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第 2 天預報的夜間風速 (每小時公里數)] | 兩天的天氣預報。夜間的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 2 天預報的夜間風速 (每小時英里數)] | 兩天的天氣預報。夜間的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第 2 天預報的 QPF (英吋)] | 兩天的天氣預報。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 第 2 天預報的 QPF (公釐)] | 兩天的天氣預報。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 第 2 天預報的 QPF 雪量 (公分)] | 兩天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第 2 天預報的 QPF 雪量 (英吋)] | 兩天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 第 3 天預報的日曆天攝氏最高溫度] | 三天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (攝氏度數) | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第 3 天預報的日曆天華氏最高溫度] | 三天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (華氏度數) | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第 3 天預報的日曆天攝氏最低溫度] | 三天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (攝氏度數) | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第 3 天預報的日曆天華氏最低溫度] | 三天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (華氏度數) | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第 3 天預報的日雲量 (英里)] | 三天的天氣預報。白天的天氣資訊。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 第 3 天預報的日雲量 (公里)] | 三天的天氣預報。白天的天氣資訊。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第 3 天預報的日降水機率] | 三天的天氣預報。白天的天氣資訊。降水機率 (百分比)。 | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 第 3 天預報的日降水類型] | 三天的天氣預報。白天的天氣資訊。降水的可能形式 (雨、雪、雨夾雪等)。 | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 第 3 天預報的日 QPF (英吋)] | 三天的天氣預報。白天的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 第 3 天預報的日 QPF (公釐)] | 三天的天氣預報。白天的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 第 3 天預報的日 QPF 雪量 (公分)] | 三天的天氣預報。白天的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第 3 天預報的日 QPF 雪量 (英吋)] | 三天的天氣預報。白天的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第 3 天預報的日相對濕度] | 三天的天氣預報。白天的天氣資訊。空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：0 到 100。 | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 第 3 天預報的日雪範圍] | 三天的天氣預報。白天的天氣資訊。潛在大量降雪 (1-3 英吋、3-6 英吋等)。 | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 第 3 天預報的攝氏日溫度] | 三天的天氣預報。白天的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 第 3 天預報的華氏日溫度] | 三天的天氣預報。白天的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第 3 天預報的攝氏日溫度酷熱指數] | 三天的天氣預報。白天的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第 3 天預報的華氏日溫度酷熱指數] | 三天的天氣預報。白天的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第 3 天預報的日攝氏風寒溫度] | 三天的天氣預報。白天的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第 3 天預報的日華氏風寒溫度] | 三天的天氣預報。白天的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第 3 天預報的打雷指數] | 三天的天氣預報。白天的天氣資訊。影響某個區域的大雷雨機率指數。0 級 (未打雷) 到 5 級 (劇烈大雷雨的高風險)。 | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 第 3 天預報的日 UV 指數] | 三天的天氣預報。白天的天氣資訊。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 第 3 天預報的日風向] | 三天的天氣預報。白天的天氣資訊。風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 第 3 天預報的日陣風 (每小時公里數)] | 三天的天氣預報。白天的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第 3 天預報的日陣風 (每小時英里數)] | 三天的天氣預報。白天的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第 3 天預報的日風速 (每小時公里數)] | 三天的天氣預報。白天的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 3 天預報的日風速 (每小時英里數)] | 三天的天氣預報。白天的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第 3 天預報的夜間雲量 (英里)] | 三天的天氣預報。夜間的天氣資訊。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 第 3 天預報的夜間雲量 (公里)] | 三天的天氣預報。夜間的天氣資訊。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第 3 天預報的夜間降水機率] | 三天的天氣預報。夜間的天氣資訊。降水機率 (百分比)。 | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 第 3 天預報的夜間降水類型] | 三天的天氣預報。夜間的天氣資訊。降水的可能形式 (雨、雪、雨夾雪等)。 | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 第 3 天預報的夜間 QPF (英吋)] | 三天的天氣預報。夜間的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 第 3 天預報的夜間 QPF (公釐)] | 三天的天氣預報。夜間的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 第 3 天預報的夜間 QPF 雪量 (公分)] | 三天的天氣預報。夜間的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第 3 天預報的夜間 QPF 雪量 (英吋)] | 三天的天氣預報。夜間的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第 3 天預報的夜間相對濕度] | 三天的天氣預報。夜間的天氣資訊。空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：0 到 100。 | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 第 3 天預報的夜間雪範圍] | 三天的天氣預報。夜間的天氣資訊。潛在大量降雪 (1-3 英吋、3-6 英吋等)。 | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 第 3 天預報的夜間攝氏溫度] | 三天的天氣預報。夜間的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 第 3 天預報的夜間華氏溫度] | 三天的天氣預報。夜間的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第 3 天預報的夜間攝氏溫度酷熱指數] | 三天的天氣預報。夜間的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第 3 天預報的夜間華氏溫度酷熱指數] | 三天的天氣預報。夜間的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第 3 天預報的夜間攝氏風寒溫度] | 三天的天氣預報。夜間的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第 3 天預報的夜間華氏風寒溫度] | 三天的天氣預報。夜間的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第 3 天預報的夜間打雷指數] | 三天的天氣預報。夜間的天氣資訊。影響某個區域的大雷雨機率指數。0 級 (未打雷) 到 5 級 (劇烈大雷雨的高風險)。 | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 第 3 天預報的夜間 UV 指數] | 三天的天氣預報。夜間的天氣資訊。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 第 3 天預報的夜間風向] | 三天的天氣預報。夜間的天氣資訊。風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 第 3 天預報的夜間陣風 (每小時公里數)] | 三天的天氣預報。夜間的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第 3 天預報的夜間陣風 (每小時英里數)] | 三天的天氣預報。夜間的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第 3 天預報的夜間風速 (每小時公里數)] | 三天的天氣預報。夜間的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 3 天預報的夜間風速 (每小時英里數)] | 三天的天氣預報。夜間的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第 3 天預報的 QPF (英吋)] | 三天的天氣預報。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 第 3 天預報的 QPF (公釐)] | 三天的天氣預報。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 第 3 天預報的 QPF 雪量 (公分)] | 三天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第 3 天預報的 QPF 雪量 (英吋)] | 三天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 第 5 天預報的日曆天攝氏最高溫度] | 五天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (攝氏度數) | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第 5 天預報的日曆天華氏最高溫度] | 五天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (華氏度數) | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第 5 天預報的日曆天攝氏最低溫度] | 五天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (攝氏度數) | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第 5 天預報的日曆天華氏最低溫度] | 五天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (華氏度數) | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第 5 天預報的日雲量 (英里)] | 五天的天氣預報。白天的天氣資訊。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 第 5 天預報的日雲量 (公里)] | 五天的天氣預報。白天的天氣資訊。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第 5 天預報的日降水機率] | 五天的天氣預報。白天的天氣資訊。降水機率 (百分比)。 | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 第 5 天預報的日降水類型] | 五天的天氣預報。白天的天氣資訊。降水的可能形式 (雨、雪、雨夾雪等)。 | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 第 5 天預報的日 QPF (英吋)] | 五天的天氣預報。白天的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 第 5 天預報的日 QPF (公釐)] | 五天的天氣預報。白天的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 第 5 天預報的日 QPF 雪量 (公分)] | 五天的天氣預報。白天的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第 5 天預報的日 QPF 雪量 (英吋)] | 五天的天氣預報。白天的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第 5 天預報的日相對濕度] | 五天的天氣預報。白天的天氣資訊。空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：0 到 100。 | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 第 5 天預報的日雪範圍] | 五天的天氣預報。白天的天氣資訊。潛在大量降雪 (1-3 英吋、3-6 英吋等)。 | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 第 5 天預報的攝氏日溫度] | 五天的天氣預報。白天的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 第 5 天預報的華氏日溫度] | 五天的天氣預報。白天的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第 5 天預報的攝氏日溫度酷熱指數] | 五天的天氣預報。白天的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第 5 天預報的華氏日溫度酷熱指數] | 五天的天氣預報。白天的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第 5 天預報的日攝氏風寒溫度] | 五天的天氣預報。白天的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第 5 天預報的日華氏風寒溫度] | 五天的天氣預報。白天的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第 5 天預報的打雷指數] | 五天的天氣預報。白天的天氣資訊。影響某個區域的大雷雨機率指數。0 級 (未打雷) 到 5 級 (劇烈大雷雨的高風險)。 | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 第 5 天預報的日 UV 指數] | 五天的天氣預報。白天的天氣資訊。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 第 5 天預報的日風向] | 五天的天氣預報。白天的天氣資訊。風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 第 5 天預報的日陣風 (每小時公里數)] | 五天的天氣預報。白天的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第 5 天預報的日陣風 (每小時英里數)] | 五天的天氣預報。白天的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第 5 天預報的日風速 (每小時公里數)] | 五天的天氣預報。白天的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 5 天預報的日風速 (每小時英里數)] | 五天的天氣預報。白天的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第 5 天預報的夜間雲量 (英里)] | 五天的天氣預報。夜間的天氣資訊。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 第 5 天預報的夜間雲量 (公里)] | 五天的天氣預報。夜間的天氣資訊。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第 5 天預報的夜間降水機率] | 五天的天氣預報。夜間的天氣資訊。降水機率 (百分比)。 | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 第 5 天預報的夜間降水類型] | 五天的天氣預報。夜間的天氣資訊。降水的可能形式 (雨、雪、雨夾雪等)。 | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 第 5 天預報的夜間 QPF (英吋)] | 五天的天氣預報。夜間的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 第 5 天預報的夜間 QPF (公釐)] | 五天的天氣預報。夜間的天氣資訊。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 第 5 天預報的夜間 QPF 雪量 (公分)] | 五天的天氣預報。夜間的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第 5 天預報的夜間 QPF 雪量 (英吋)] | 五天的天氣預報。夜間的天氣資訊。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第 5 天預報的夜間相對濕度] | 五天的天氣預報。夜間的天氣資訊。空氣的相對濕度，定義為空氣中的水蒸氣含量和在恆溫下使空氣達到飽和所需的水蒸氣含量的比例。相對濕度一定會以百分比表示。<br>範圍：0 到 100。 | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 第 5 天預報的夜間雪範圍] | 五天的天氣預報。夜間的天氣資訊。潛在大量降雪 (1-3 英吋、3-6 英吋等)。 | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 第 5 天預報的夜間攝氏溫度] | 五天的天氣預報。夜間的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (攝氏度數) | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 第 5 天預報的夜間華氏溫度] | 五天的天氣預報。夜間的天氣資訊。以定義的測量單位表示的溫度。範圍：-140 到 140。溫度 (華氏度數) | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第 5 天預報的夜間攝氏溫度酷熱指數] | 五天的天氣預報。夜間的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第 5 天預報的夜間華氏溫度酷熱指數] | 五天的天氣預報。夜間的天氣資訊。根據溫度和濕度，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第 5 天預報的夜間攝氏風寒溫度] | 五天的天氣預報。夜間的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (攝氏度數) | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第 5 天預報的夜間華氏風寒溫度] | 五天的天氣預報。夜間的天氣資訊。根據溫度和風速，人體所感受到的溫度。溫度 (華氏度數) | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第 5 天預報的夜間打雷指數] | 五天的天氣預報。夜間的天氣資訊。影響某個區域的大雷雨機率指數。0 級 (未打雷) 到 5 級 (劇烈大雷雨的高風險)。 | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 第 5 天預報的夜間 UV 指數] | 五天的天氣預報。夜間的天氣資訊。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 第 5 天預報的夜間風向] | 五天的天氣預報。夜間的天氣資訊。風吹造成的磁性風向，以度數表示。磁性方向的範圍從 0 到 359 度，其中 0° 表示北方，90° 表示東方，180° 表示南方，270° 表示西方，依此類推。<br>範圍 - 0&lt;=wind_dire_deg&lt;=350，以 10 度為間隔。 | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 第 5 天預報的夜間陣風 (每小時公里數)] | 五天的天氣預報。夜間的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時公里數) | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第 5 天預報的夜間陣風 (每小時英里數)] | 五天的天氣預報。夜間的天氣資訊。此資料欄位包含有關平均風速瞬間和暫時變化的資訊。報告會一律顯示觀察期間所記錄的最大陣風速度。如果顯示風速，則為必填的顯示欄位。陣風的速度可以用每小時英里數或每小時公里數表示。風速 (每小時英里數) | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第 5 天預報的夜間風速 (每小時公里數)] | 五天的天氣預報。夜間的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 5 天預報的夜間風速 (每小時英里數)] | 五天的天氣預報。夜間的天氣資訊。風會被視為向量；因此，風必須有方向和強度 (速度)。目前狀況下報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第 5 天預報的 QPF (英吋)] | 五天的天氣預報。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (英吋) | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 第 5 天預報的 QPF (公釐)] | 五天的天氣預報。12 或 24 小時期間預測的可測量降水量 (液體或液體相等物)。測量 (公釐)。降水量 (公釐) | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 第 5 天預報的 QPF 雪量 (公分)] | 五天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第 5 天預報的 QPF 雪量 (英吋)] | 五天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 第 7 天預報的日曆天攝氏最高溫度] | 7 天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (攝氏度數) | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第 7 天預報的日曆天華氏最高溫度] | 7 天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (華氏度數) | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第 7 天預報的日曆天攝氏最低溫度] | 7 天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (攝氏度數) | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第 7 天預報的日曆天華氏最低溫度] | 7 天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (華氏度數) | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第 7 天預報的雲量 (英里)] | 7 天的天氣預報。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 第 7 天預報的雲量 (公里)] | 7 天的天氣預報。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 第 7 天預報的 QPF (英吋)] | 7 天的天氣預報。24 小時期間預測的可測量降水量 (液體或液體相等物)。降水量 (英吋) | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 第 7 天預報的 QPF (公釐)] | 7 天的天氣預報。24 小時期間預測的可測量降水量 (液體或液體相等物)。降水量 (公釐) | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 第 7 天預報的 QPF 雪量 (公分)] | 7 天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第 7 天預報的 QPF 雪量 (英吋)] | 7 天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 第 7 天預報的 UV 指數] | 7 天的天氣預報。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 第 7 天預報的風向] | 7 天的天氣預報。平均風向 (磁性標記)。 | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 第 7 天預報的風速 (每小時公里數)] | 7 天的天氣預報。12 小時預報期間預測的最大持續風速。<br>風會被視為向量；因此，風必須有方向和強度 (速度)。預報中報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 7 天預報的風速 (每小時英里數)] | 7 天的天氣預報。12 小時預報期間預測的最大持續風速。<br>風會被視為向量；因此，風必須有方向和強度 (速度)。預報中報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第 10 天預報的日曆天攝氏最高溫度] | 十天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (攝氏度數) | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第 10 天預報的日曆天華氏最高溫度] | 十天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (華氏度數) | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第 10 天預報的日曆天攝氏最低溫度] | 十天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (攝氏度數) | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第 10 天預報的日曆天華氏最低溫度] | 十天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (華氏度數) | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第 10 天預報的雲量 (英里)] | 十天的天氣預報。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 第 10 天預報的雲量 (公里)] | 十天的天氣預報。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 第 10 天預報的 QPF (英吋)] | 十天的天氣預報。24 小時期間預測的可測量降水量 (液體或液體相等物)。降水量 (英吋) | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 第 10 天預報的 QPF (公釐)] | 十天的天氣預報。24 小時期間預測的可測量降水量 (液體或液體相等物)。降水量 (公釐) | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 第 10 天預報的 QPF 雪量 (公分)] | 十天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第 10 天預報的 QPF 雪量 (英吋)] | 十天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 第 10 天預報的 UV 指數] | 十天的天氣預報。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 第 10 天預報的風向] | 十天的天氣預報。平均風向 (磁性標記)。 | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 第 10 天預報的風速 (每小時公里數)] | 十天的天氣預報。12 小時預報期間預測的最大持續風速。<br>風會被視為向量；因此，風必須有方向和強度 (速度)。預報中報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 10 天預報的風速 (每小時英里數)] | 十天的天氣預報。12 小時預報期間預測的最大持續風速。<br>風會被視為向量；因此，風必須有方向和強度 (速度)。預報中報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第 14 天預報的日曆天攝氏最高溫度] | 十四天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (攝氏度數) | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第 14 天預報的日曆天華氏最高溫度] | 十四天的天氣預報。特定日期午夜至午夜的每日最高溫度。溫度 (華氏度數) | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第 14 天預報的日曆天攝氏最低溫度] | 十四天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (攝氏度數) | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第 14 天預報的日曆天華氏最低溫度] | 十四天的天氣預報。特定日期午夜至午夜的每日最低溫度。溫度 (華氏度數) | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第 14 天預報的雲量 (英里)] | 十四天的天氣預報。白天平均雲量 (以百分比表示)。距離 (英里)。 | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 第 14 天預報的雲量 (公里)] | 十四天的天氣預報。白天平均雲量 (以百分比表示)。距離 (公里)。 | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 第 14 天預報的 QPF (英吋) | 十四天的天氣預報。24 小時期間預測的可測量降水量 (液體或液體相等物)。降水量 (英吋) | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 第 14 天預報的 QPF (公釐)] | 十四天的天氣預報。24 小時期間預測的可測量降水量 (液體或液體相等物)。降水量 (公釐) | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 第 14 天預報的 QPF 雪量 (公分)] | 十四天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (公分) | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第 14 天預報的 QPF 雪量 (英吋)] | 十四天的天氣預報。12 或 24 小時預報期間預測的可測量降水量 (例如雪)。測量 (公分)。降雪量 (英吋) | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 第 14 天預報的 UV 指數] | 十四天的天氣預報。12 小時預報期間的最大 UV 指數。 | `weather.forecast.day14Forecast.uvIndex` |
| 第 14 天預報的風向 | 十四天的天氣預報。平均風向 (磁性標記)。 | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 第 14 天預報的風速 (每小時公里數)] | 十四天的天氣預報。12 小時預報期間預測的最大持續風速。<br>風會被視為向量；因此，風必須有方向和強度 (速度)。預報中報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時公里數) | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第 14 天預報的風速 (每小時英里數)] | 十四天的天氣預報。12 小時預報期間預測的最大持續風速。<br>風會被視為向量；因此，風必須有方向和強度 (速度)。預報中報告的風資訊會和稱為持續風速的 10 分鐘平均值相對應。風速的瞬間或短暫變化稱為「陣風」，並會在單獨的資料欄位中報告。風向會一律以「風從何處吹來」表示，意思就是北風即為從北方吹向南方。如果您在北風中面向北方，風即會往您的臉上吹。面向南方，則北風會在您的背後。風速 (每小時英里數) | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 觸發器 {#triggers}

觸發因素會根據各種輸入定義語義上的天氣狀況。

| 欄位 | 說明 | XDM 路徑 |
| --- | ---- | --- |
| [!UICONTROL 產品觸發因素] | 顯示狀況何時適合提升特定類別產品的銷售。它們會被對應至整數實體。可以從 IBM 取得完整清單。 | `weather.productTriggers` |
| [!UICONTROL 相對觸發因素] | 根據人類感知的相對狀況。諸如熱或冷之類的東西。它們會被對應至整數實體。可以從 IBM 取得完整清單。 | `weather.relativeTriggers` |
| [!UICONTROL 惡劣天氣觸發因素] | 顯示各種惡劣的天氣狀況，例如颶風或降雨過多。 | `weather.severeTriggers` |
