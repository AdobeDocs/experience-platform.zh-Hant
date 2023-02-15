---
title: 氣象資料欄位對應
description: 可用氣象資料欄位的參考頁面，這些欄位是與氣象管道整合時可用的。
source-git-commit: 3e5ca8fe67e5ad9ce0fe70d0c9f1e2fbc20cee17
workflow-type: tm+mt
source-wordcount: '12238'
ht-degree: 0%

---


# 氣象資料欄位對應

Adobe已與 [!DNL [The Weather Company]](https://www.ibm.com/weather) 為透過資料流收集的資料帶來美國天氣的額外內容。 您可以將此資料用於分析、鎖定目標及建立Experience Platform。

此頁面列出所有可用欄位，供您用來豐富對象資料。

欄位會分成三個與欄位群組對齊的不同群組。

* [**[!UICONTROL 當前天氣]**](#current-weather):使用者目前的天氣狀況（根據其位置）。 這包括目前的溫度、枕頭、雲端覆蓋範圍等。
* [**[!UICONTROL 預測天氣]**](#forecast):預測包括用戶地點的1、2、3、5、7和10天預測。
* [**[!UICONTROL 觸發器]**](#triggers):觸發器是對應至不同語義天氣條件的特定組合。 有三種不同的天氣觸發因素：

   * **[!UICONTROL 相對觸發器]**:在語義上有意義的條件，如寒冷或雨天。 不同氣候的定義可能不同。
   * **[!UICONTROL 產品觸發器]**:導致購買不同產品類型的條件。 例如：天氣預報寒冷意味著購買雨衣的可能性更大。
   * **[!UICONTROL 惡劣天氣觸發]**:嚴重的天氣警告，比如冬季風暴或颶風警告。

## 當前天氣 {#current-weather}

使用者目前的天氣狀況（根據其位置）。

| 欄位 | 說明 | XDM路徑 |
| --- | ---- | --- |
| [!UICONTROL 溫度露點C] | 必須在恆壓下冷卻空氣以達到飽和的溫度。 露點也是間接測量空氣濕度的方法。 露點永遠不會超過溫度。 當Dewpoint和溫度相等時，通常會形成雲或霧。 溫度和露點值越近，相對濕度越高。 範圍 —80 - 100(°F)或–62 - 37(°C)。 攝氏度溫度 | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 溫度露點華氏度] | 必須在恆壓下冷卻空氣以達到飽和的溫度。 露點也是間接測量空氣濕度的方法。 露點永遠不會超過溫度。 當Dewpoint和溫度相等時，通常會形成雲或霧。 溫度和露點值越近，相對濕度越高。 範圍 —80 - 100(°F)或–62 - 37(°C)。 溫度（華氏度） | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 降水最後一小時英吋] | 滾動時液體沈澱量。 呈現的金額是整個請求時間的滾動時間（現在）。 以英吋計的降水 | `weather.current.precip1Hour.inches` |
| [!UICONTROL 降水最後一小時毫米] | 滾動時液體沈澱量。 呈現的金額是整個請求時間的滾動時間（現在）。 以毫米為單位的降水 | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 滾動二十四小時液體沈澱量。 呈現的金額是整個請求時間的滾動時間（現在）。 以英吋計的降水 | `weather.current.precip24Hour.inches` |
| [!UICONTROL 最近24小時降水] | 滾動二十四小時液體沈澱量。 呈現的金額是整個請求時間的滾動時間（現在）。 以毫米為單位的降水 | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 降雨持續6小時] | 滾動六小時液體沈澱量。 呈現的金額是整個請求時間的滾動時間（現在）。 以英吋計的降水 | `weather.current.precip6Hour.inches` |
| [!UICONTROL 持續6小時的降水量] | 滾動六小時液體沈澱量。 呈現的金額是整個請求時間的滾動時間（現在）。 以毫米為單位的降水 | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 壓力變化] | 密里巴斯最近三小時的壓力變化。 | `weather.current.pressureChange` |
| [!UICONTROL 壓力平均海平面] | 平均海平面壓力，毫巴。  換句話說，海平面的平均氣壓。<br>範圍 — 毫巴精確到1/10mb。 | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 相對濕度] | 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.current.relativeHumidity` |
| [!UICONTROL 雪最後一小時公分] | 一小時的降雪量。  呈現的金額是整個請求時間的滾動時間（現在）。 降雪公分 | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 雪最後一小時英吋] | 一小時的降雪量。  呈現的金額是整個請求時間的滾動時間（現在）。 降雪量（英吋） | `weather.current.snow1Hour.inches` |
| [!UICONTROL 雪24小時公分] | 24小時的降雪量。  呈現的金額是整個請求時間的滾動時間（現在）。 降雪公分 | `weather.current.snow24Hour.centimeters` |
| 雪24小時英吋 | 24小時的降雪量。  呈現的金額是整個請求時間的滾動時間（現在）。 降雪量（英吋） | `weather.current.snow24Hour.inches` |
| [!UICONTROL 最近6小時的雪] | 一小時的降雪量。  呈現的金額是整個請求時間的滾動時間（現在）。 降雪公分 | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 雪持續6小時] | 一小時的降雪量。  呈現的金額是整個請求時間的滾動時間（現在）。 降雪量（英吋） | `weather.current.snow6Hour.inches` |
| [!UICONTROL 日落時間] | UTC的日落時間。 | `weather.current.sunsetTime` |
| [!UICONTROL 溫度攝氏] | 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.current.temperature.celsius` |
| [!UICONTROL 溫度華氏度] | 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 溫度變化24小時C] | 與24小時前的報告相比，溫度的變化。 攝氏度溫度 | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 溫度變化24小時華氏度] | 與24小時前的報告相比，溫度的變化。 溫度（華氏度） | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 氣溫感覺像攝氏度] | 一個明顯的溫度。 它代表了風寒或熱指數共同影響暴露的人體皮膚上的空氣溫度「感覺」。<br>當溫度為65°F或更高時，「感覺」(Feels)值表示計算的熱指數。  當溫度低於65°F時，「感覺似」值表示計算的風寒。<br>範圍–140到140。 攝氏度溫度 | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 溫度感覺像華氏] | 一個明顯的溫度。 它代表了風寒或熱指數共同影響暴露的人體皮膚上的空氣溫度「感覺」。<br>當溫度為65°F或更高時，「感覺」(Feels)值表示計算的熱指數。  當溫度低於65°F時，「感覺似」值表示計算的風寒。<br>範圍–140到140。 溫度（華氏度） | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 自上午7點以來的最高溫度] | 當地時間早上7點以來的最高溫度。 攝氏度溫度 | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 自華氏上午7點以來的最高溫度] | 當地時間早上7點以來的最高溫度。 溫度（華氏度） | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 最低溫度持續24小時] | 過去24小時的最低氣溫。  24小時期間是參考請求時間（現在）。  攝氏度溫度 | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 最低溫度持續24小時華氏度] | 過去24小時的最低氣溫。  24小時期間是參考請求時間（現在）。  溫度（華氏度） | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 風向] | 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.current.windDirection` |
| [!UICONTROL 陣風時速] | 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 陣風時速] | 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.current.windGust.`milesPerHour |
| [!UICONTROL 風速公里/小時] | 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 每小時風速] | 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.current.windSpeed.milesPerHour` |

## 預測天氣 {#forecast}

根據特定時間點的位置，使用者的預測天氣。

| 欄位 | 說明 | XDM路徑 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 一天的天氣預報。 指定日的午夜至午夜每日最高溫度。 攝氏度溫度 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 一天的天氣預報。 指定日的午夜至午夜每日最高溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 一天的天氣預報。 指定日的午夜至午夜每日最低溫度。 攝氏度溫度 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 一天的天氣預報。 指定日的午夜至午夜每日最低溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 一天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 一天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 一天的天氣預報。 白天的天氣資訊。 有降水的可能性（百分比）。 | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 一天的天氣預報。 白天的天氣資訊。 可能降落的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 一天的天氣預報。 白天的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 一天的天氣預報。 白天的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 一天的天氣預報。 白天的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 一天的天氣預報。 白天的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 一天的天氣預報。 白天的天氣資訊。 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 一天的天氣預報。 白天的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 一天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 一天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 一天的天氣預報。 白天的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 攝氏度溫度 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 一天的天氣預報。 白天的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 一天的天氣預報。 白天的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 攝氏度溫度 | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 一天的天氣預報。 白天的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 一天的天氣預報。 白天的天氣資訊。 雷暴影響某個區域的概率指數。 0(無雷擊至5（嚴重雷擊風險高）。 | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 一天的天氣預報。 白天的天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 一天的天氣預報。 白天的天氣資訊。 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 一天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 一天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 一天的天氣預報。 白天的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 一天的天氣預報。 白天的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 一天的天氣預報。 夜間的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 一天的天氣預報。 夜間的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第1天預報夜間降水機會] | 一天的天氣預報。 夜間的天氣資訊。 有降水的可能性（百分比）。 | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 一天的天氣預報。 夜間的天氣資訊。 可能降落的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 一天的天氣預報。 夜間的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 一天的天氣預報。 夜間的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 一天的天氣預報。 夜間的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 一天的天氣預報。 夜間的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 一天的天氣預報。 夜間的天氣資訊。 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 一天的天氣預報。 夜間的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 一天的天氣預報。 夜間的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 一天的天氣預報。 夜間的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 一天的天氣預報。 夜間的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 攝氏度溫度 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 一天的天氣預報。 夜間的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 一天的天氣預報。 夜間的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 攝氏度溫度 | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第1天預報夜間氣溫風寒華氏] | 一天的天氣預報。 夜間的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 溫度（華氏度） | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第1天預測夜雷指數] | 一天的天氣預報。 夜間的天氣資訊。 雷暴影響某個區域的概率指數。 0(無雷擊至5（嚴重雷擊風險高）。 | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 第1天預測夜間UV指數] | 一天的天氣預報。 夜間的天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 第1天預報夜間風向] | 一天的天氣預報。 夜間的天氣資訊。 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 第1天預報夜間陣風每小時] | 一天的天氣預報。 夜間的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第1天預報夜間陣風每小時] | 一天的天氣預報。 夜間的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第1天預報夜間每小時風速] | 一天的天氣預報。 夜間的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第1天預報夜間風速英里/小時] | 一天的天氣預報。 夜間的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第1天預測QPF英吋] | 一天的天氣預報。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 第1天預測QPF毫米] | 一天的天氣預報。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 第1天預報QPF雪公分] | 一天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第1天預測QPF雪英吋] | 一天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 第2天預測日曆日氣溫最高攝氏度] | 兩天的天氣預報。 指定日的午夜至午夜每日最高溫度。 攝氏度溫度 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第2天預測日曆日氣溫最高華氏度] | 兩天的天氣預報。 指定日的午夜至午夜每日最高溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第2天預測日曆日氣溫最低攝氏度] | 兩天的天氣預報。 指定日的午夜至午夜每日最低溫度。 攝氏度溫度 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第2天預測日曆日溫度最低華氏度] | 兩天的天氣預報。 指定日的午夜至午夜每日最低溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第2天預測日雲覆蓋英里] | 兩天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 第2天預測日雲覆蓋公里] | 兩天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第2天預報日降水機會] | 兩天的天氣預報。 白天的天氣資訊。 有降水的可能性（百分比）。 | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 第2天預報日降水類型] | 兩天的天氣預報。 白天的天氣資訊。 可能降落的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 第2天預測天QPF英吋] | 兩天的天氣預報。 白天的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 第2天預測天QPF毫米] | 兩天的天氣預報。 白天的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 第2天預報天QPF雪公分] | 兩天的天氣預報。 白天的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第2天預測天QPF雪英吋] | 兩天的天氣預報。 白天的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第2天預測日相對濕度] | 兩天的天氣預報。 白天的天氣資訊。 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 第2天預測天雪範圍] | 兩天的天氣預報。 白天的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 第2天預測天氣溫Celsius] | 兩天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 第2天預測天溫度華氏度] | 兩天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第2天預測天溫度熱指數Celsiu] | 兩天的天氣預報。 白天的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 攝氏度溫度 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天預測日溫度熱指數華氏] | 兩天的天氣預報。 白天的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天預報天氣溫風寒攝氏] | 兩天的天氣預報。 白天的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 攝氏度溫度 | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第2天預報天氣溫風寒華氏] | 兩天的天氣預報。 白天的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天預測天雷數指數] | 兩天的天氣預報。 白天的天氣資訊。 雷暴影響某個區域的概率指數。 0(無雷擊至5（嚴重雷擊風險高）。 | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 第2天預測日UV指數] | 兩天的天氣預報。 白天的天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 第2天預報日風向] | 兩天的天氣預報。 白天的天氣資訊。 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 第2天預報日每小時陣風公里] | 兩天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第2天預報日陣風英里/小時] | 兩天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第2天預報日風速公里/小時] | 兩天的天氣預報。 白天的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天預報日風速英里/小時] | 兩天的天氣預報。 白天的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第2天預報夜間雲覆蓋英里] | 兩天的天氣預報。 夜間的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 第2天預報夜間雲覆蓋公里] | 兩天的天氣預報。 夜間的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第2天預報夜間降水機會] | 兩天的天氣預報。 夜間的天氣資訊。 有降水的可能性（百分比）。 | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 第2天預報夜間降水類型] | 兩天的天氣預報。 夜間的天氣資訊。 可能降落的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 第2天預報夜QPF英吋] | 兩天的天氣預報。 夜間的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 第2天預測夜QPF毫米] | 兩天的天氣預報。 夜間的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 第2天預報夜QPF雪公分] | 兩天的天氣預報。 夜間的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第2天預報夜QPF雪英吋] | 兩天的天氣預報。 夜間的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第2天預測夜間相對濕度] | 兩天的天氣預報。 夜間的天氣資訊。 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 第2天預報夜間積雪範圍] | 兩天的天氣預報。 夜間的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 第2天預測夜間氣溫攝氏度] | 兩天的天氣預報。 夜間的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 第2天預測夜間氣溫華氏度] | 兩天的天氣預報。 夜間的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第2天預報夜間溫度熱指數Clisus] | 兩天的天氣預報。 夜間的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 攝氏度溫度 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天預測夜間溫度熱指數華氏] | 兩天的天氣預報。 夜間的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天預報夜間氣溫風寒攝氏度] | 兩天的天氣預報。 夜間的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 攝氏度溫度 | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第2天預報夜間氣溫風降溫華氏] | 兩天的天氣預報。 夜間的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 溫度（華氏度） | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天預測夜雷指數] | 兩天的天氣預報。 夜間的天氣資訊。 雷暴影響某個區域的概率指數。 0(無雷擊至5（嚴重雷擊風險高）。 | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 第2天預測夜間UV指數] | 兩天的天氣預報。 夜間的天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 第2天預報夜間風向] | 兩天的天氣預報。 夜間的天氣資訊。 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 第2天預報夜間陣風每小時] | 兩天的天氣預報。 夜間的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第2天預報夜間陣風每小時] | 兩天的天氣預報。 夜間的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第2天預報夜間每小時風速] | 兩天的天氣預報。 夜間的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天預報夜間風速英里/小時] | 兩天的天氣預報。 夜間的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第2天預測QPF英吋] | 兩天的天氣預報。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 第2天預測QPF毫米] | 兩天的天氣預報。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 第2天預報QPF雪公分] | 兩天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第2天預測QPF雪英吋] | 兩天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 第3天預測日曆日氣溫最高攝氏度] | 三天的天氣預報。 指定日的午夜至午夜每日最高溫度。 攝氏度溫度 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第3天預測日曆日氣溫最高華氏度] | 三天的天氣預報。 指定日的午夜至午夜每日最高溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第3天預測日曆日氣溫最低攝氏度] | 三天的天氣預報。 指定日的午夜至午夜每日最低溫度。 攝氏度溫度 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第3天預測日曆日溫度最低華氏度] | 三天的天氣預報。 指定日的午夜至午夜每日最低溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第3天預測日雲覆蓋英里] | 三天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 第3天預測日雲覆蓋公里] | 三天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第3天預報天降水機會] | 三天的天氣預報。 白天的天氣資訊。 有降水的可能性（百分比）。 | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 第3天預報日降水類型] | 三天的天氣預報。 白天的天氣資訊。 可能降落的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 第3天預測天QPF英吋] | 三天的天氣預報。 白天的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 第3天預測天QPF毫米] | 三天的天氣預報。 白天的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 第3天預報天QPF雪公分] | 三天的天氣預報。 白天的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第3天預報天QPF雪英吋] | 三天的天氣預報。 白天的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第3天預測日相對濕度] | 三天的天氣預報。 白天的天氣資訊。 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 第3天預測天雪範圍] | 三天的天氣預報。 白天的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 第3天預測天氣溫Celsius] | 三天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 第3天預測天溫度華氏度] | 三天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第3天預測天溫度熱指數Celsiu] | 三天的天氣預報。 白天的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 攝氏度溫度 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天預測天溫度熱指數華氏] | 三天的天氣預報。 白天的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天預報天氣溫風寒攝氏] | 三天的天氣預報。 白天的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 攝氏度溫度 | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第3天預報天氣溫風寒華氏] | 三天的天氣預報。 白天的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天預測天雷指數] | 三天的天氣預報。 白天的天氣資訊。 雷暴影響某個區域的概率指數。 0(無雷擊至5（嚴重雷擊風險高）。 | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 第3天預測日UV指數] | 三天的天氣預報。 白天的天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 第3天預報日風向] | 三天的天氣預報。 白天的天氣資訊。 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 第3天預報日每小時陣風公里] | 三天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第3天預報日陣風/小時] | 三天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第3天預報日風速公里/小時] | 三天的天氣預報。 白天的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天預報日風速英里/小時] | 三天的天氣預報。 白天的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第3天預報夜間雲覆蓋英里] | 三天的天氣預報。 夜間的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 第3天預報夜間雲覆蓋公里] | 三天的天氣預報。 夜間的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第3天預報夜間降水機會] | 三天的天氣預報。 夜間的天氣資訊。 有降水的可能性（百分比）。 | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 第3天預報夜間降水類型] | 三天的天氣預報。 夜間的天氣資訊。 可能降落的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 第3天預報夜QPF英吋] | 三天的天氣預報。 夜間的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 第3天預報夜QPF毫米] | 三天的天氣預報。 夜間的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 第3天預報夜QPF雪公分] | 三天的天氣預報。 夜間的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第3天預報夜QPF雪英吋] | 三天的天氣預報。 夜間的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第3天預測夜間相對濕度] | 三天的天氣預報。 夜間的天氣資訊。 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 第3天預報夜間積雪] | 三天的天氣預報。 夜間的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 第3天預測夜間氣溫攝氏度] | 三天的天氣預報。 夜間的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 第3天預報夜間氣溫華氏度] | 三天的天氣預報。 夜間的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第3天預報夜間溫度熱指數Clisus] | 三天的天氣預報。 夜間的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 攝氏度溫度 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天預測夜間溫度熱指數華氏] | 三天的天氣預報。 夜間的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天預報夜間氣溫風寒攝氏度] | 三天的天氣預報。 夜間的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 攝氏度溫度 | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第3天預報夜間氣溫風降溫華氏] | 三天的天氣預報。 夜間的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 溫度（華氏度） | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天預測夜雷指數] | 三天的天氣預報。 夜間的天氣資訊。 雷暴影響某個區域的概率指數。 0(無雷擊至5（嚴重雷擊風險高）。 | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 第3天預測夜間UV指數] | 三天的天氣預報。 夜間的天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 第3天預報夜間風向] | 三天的天氣預報。 夜間的天氣資訊。 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 第3天預報夜間陣風每小時] | 三天的天氣預報。 夜間的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第3天預報夜間陣風每小時] | 三天的天氣預報。 夜間的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第3天預報夜間每小時風速] | 三天的天氣預報。 夜間的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天預報夜間風速英里/小時] | 三天的天氣預報。 夜間的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第3天預測QPF英吋] | 三天的天氣預報。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 第3天預測QPF毫米] | 三天的天氣預報。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 第3天預報QPF雪公分] | 三天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第3天預測QPF雪英吋] | 三天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 第5天預測日曆日氣溫最高攝氏度] | 五天的天氣預報。 指定日的午夜至午夜每日最高溫度。 攝氏度溫度 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第5天預測日曆日氣溫最高華氏度] | 五天的天氣預報。 指定日的午夜至午夜每日最高溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第5天預測日曆日氣溫最低攝氏度] | 五天的天氣預報。 指定日的午夜至午夜每日最低溫度。 攝氏度溫度 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第5天預測日曆日溫度最低華氏度] | 五天的天氣預報。 指定日的午夜至午夜每日最低溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第5天預測日雲覆蓋英里] | 五天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 第5天預測日雲覆蓋公里] | 五天的天氣預報。 白天的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第5天預報日降水機會] | 五天的天氣預報。 白天的天氣資訊。 有降水的可能性（百分比）。 | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 第5天預報日降水類型] | 五天的天氣預報。 白天的天氣資訊。 可能降落的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 第5天預測天QPF英吋] | 五天的天氣預報。 白天的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 第5天預測天QPF毫米] | 五天的天氣預報。 白天的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 第5天預報天QPF雪公分] | 五天的天氣預報。 白天的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第5天預報天QPF雪英吋] | 五天的天氣預報。 白天的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第5天預測日相對濕度] | 五天的天氣預報。 白天的天氣資訊。 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 第5天預測天雪範圍] | 五天的天氣預報。 白天的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 第5天預測天氣溫Celsius] | 五天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 第5天預測天溫度華氏度] | 五天的天氣預報。 白天的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第5天預報日溫度熱指數Clusios] | 五天的天氣預報。 白天的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 攝氏度溫度 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天預測日溫度熱指數華氏] | 五天的天氣預報。 白天的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天預報天氣溫風寒攝氏] | 五天的天氣預報。 白天的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 攝氏度溫度 | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第5天預報天氣溫風寒華氏] | 五天的天氣預報。 白天的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天預測天雷鳴指數] | 五天的天氣預報。 白天的天氣資訊。 雷暴影響某個區域的概率指數。 0(無雷擊至5（嚴重雷擊風險高）。 | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 第5天預測日UV指數] | 五天的天氣預報。 白天的天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 第5天預報日風向] | 五天的天氣預報。 白天的天氣資訊。 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 第5天預報日每小時陣風公里] | 五天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第5天預報日陣風英里/小時] | 五天的天氣預報。 白天的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第5天預報日風速公里/小時] | 五天的天氣預報。 白天的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天預報日風速英里/小時] | 五天的天氣預報。 白天的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第5天預報夜間雲覆蓋英里] | 五天的天氣預報。 夜間的天氣資訊。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 第5天預報夜間雲覆蓋公里] | 五天的天氣預報。 夜間的天氣資訊。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第5天預報夜間降水機會] | 五天的天氣預報。 夜間的天氣資訊。 有降水的可能性（百分比）。 | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 第5天預報夜間降水類型] | 五天的天氣預報。 夜間的天氣資訊。 可能降落的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 第5天預報夜QPF英吋] | 五天的天氣預報。 夜間的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 第5天預報夜QPF毫米] | 五天的天氣預報。 夜間的天氣資訊。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 第5天預報夜QPF雪公分] | 五天的天氣預報。 夜間的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第5天預報夜QPF雪英吋] | 五天的天氣預報。 夜間的天氣資訊。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第5天預測夜間相對濕度] | 五天的天氣預報。 夜間的天氣資訊。 空氣的相對濕度，定義為空氣中水蒸氣量與在恆定溫度下使空氣達到飽和所需的蒸氣量之比。 相對濕度總是以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 第5天預報夜間積雪範圍] | 五天的天氣預報。 夜間的天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 第5天預報夜間氣溫攝氏度] | 五天的天氣預報。 夜間的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 攝氏度溫度 | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 第5天預報夜間氣溫華氏度] | 五天的天氣預報。 夜間的天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 溫度（華氏度） | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第5天預報夜間溫度熱指數Clisus] | 五天的天氣預報。 夜間的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 攝氏度溫度 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天預報夜間溫度熱指數華氏] | 五天的天氣預報。 夜間的天氣資訊。 根據溫度和濕度暴露的人所感受到的溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天預報夜間氣溫風寒攝氏度] | 五天的天氣預報。 夜間的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 攝氏度溫度 | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第5天預報夜間氣溫風降溫華氏] | 五天的天氣預報。 夜間的天氣資訊。 溫度，就像根據溫度和風速暴露的人感受到的溫度。 溫度（華氏度） | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天預測夜雷指數] | 五天的天氣預報。 夜間的天氣資訊。 雷暴影響某個區域的概率指數。 0(無雷擊至5（嚴重雷擊風險高）。 | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 第5天預測夜間UV指數] | 五天的天氣預報。 夜間的天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 第5天預報夜間風向] | 五天的天氣預報。 夜間的天氣資訊。 風從中吹出的磁風方向以一定程度表示。 磁方向從0到359度不等，其中0°表示北、90°表示東、180°表示南、270°表示西等。<br>範圍 — 0&lt;=wind_dire_deg&lt;=350,10度間隔。 | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 第5天預報夜間陣風每小時] | 五天的天氣預報。 夜間的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時風速 | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第5天預報夜間陣風每小時] | 五天的天氣預報。 夜間的天氣資訊。 此資料欄位包含有關平均風速的突然和暫時變化的資訊。 報告總是顯示在觀測期間記錄的最大陣風速度。 如果顯示「風速」，則此為必要的顯示欄位。 陣風的速度可以以每小時英里或每小時公里來表示。 每小時以英里計的風速 | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第5天預報夜間每小時風速] | 五天的天氣預報。 夜間的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天預報夜間風速英里/小時] | 五天的天氣預報。 夜間的天氣資訊。 風被視為向量；因此，風必須有方向和大小（速度）。 在當前條件下報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第5天預測QPF英吋] | 五天的天氣預報。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以英吋計的降水 | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 第5天預測QPF毫米] | 五天的天氣預報。 12或24小時內的預測可測降水量（液體或液體當量）。 以毫米計。 以毫米為單位的降水 | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 第5天預報QPF雪公分] | 五天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第5天預測QPF雪英吋] | 五天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天預測日曆日氣溫最高攝氏度] | 天氣預報七天。 指定日的午夜至午夜每日最高溫度。 攝氏度溫度 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第7天預測日曆日氣溫最高華氏度] | 天氣預報七天。 指定日的午夜至午夜每日最高溫度。 溫度（華氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第7天預測日曆日氣溫最低攝氏度] | 天氣預報七天。 指定日的午夜至午夜每日最低溫度。 攝氏度溫度 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第7天預測日曆日溫度最低華氏度] | 天氣預報七天。 指定日的午夜至午夜每日最低溫度。 溫度（華氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第7天預測雲覆蓋英里] | 天氣預報七天。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 第7天預報雲封面公里] | 天氣預報七天。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 第7天預測QPF英吋] | 天氣預報七天。 24小時內預測可測降水量（液體或液體當量）。 以英吋計的降水 | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 第7天預測QPF毫米] | 天氣預報七天。 24小時內預測可測降水量（液體或液體當量）。 以毫米為單位的降水 | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 第7天預報QPF雪公分] | 天氣預報七天。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第7天預測QPF雪英吋] | 天氣預報七天。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天預測UV指數] | 天氣預報七天。 12小時預測期間的最大UV索引。 | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 第7天預報風向] | 天氣預報七天。 以磁記號表示的平均風向。 | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 第7天預報風速公里/小時] | 天氣預報七天。 12小時預測期內最大持續風速的預測。<br>風被視為向量；因此，風必須有方向和大小（速度）。 預報中報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第7天預報風速每小時英里] | 天氣預報七天。 12小時預測期內最大持續風速的預測。<br>風被視為向量；因此，風必須有方向和大小（速度）。 預報中報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第10天預測日曆日溫度最大值Celsius] | 十天的天氣預報。 指定日的午夜至午夜每日最高溫度。 攝氏度溫度 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第10天預測日曆日氣溫最高華氏度] | 十天的天氣預報。 指定日的午夜至午夜每日最高溫度。 溫度（華氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第10天預測日曆日氣溫最低攝氏度] | 十天的天氣預報。 指定日的午夜至午夜每日最低溫度。 攝氏度溫度 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第10天預測日曆日溫度最低華氏度] | 十天的天氣預報。 指定日的午夜至午夜每日最低溫度。 溫度（華氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第10天預測雲覆蓋英里] | 十天的天氣預報。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 第10天預測雲覆蓋公里] | 十天的天氣預報。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 第10天預測QPF英吋] | 十天的天氣預報。 24小時內預測可測降水量（液體或液體當量）。 以英吋計的降水 | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 第10天預測QPF毫米] | 十天的天氣預報。 24小時內預測可測降水量（液體或液體當量）。 以毫米為單位的降水 | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 第10天預報QPF雪公分] | 十天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第10天預測QPF雪英吋] | 十天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 第10天預測UV指數] | 十天的天氣預報。 12小時預測期間的最大UV索引。 | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 第10天預報風向] | 十天的天氣預報。 以磁記號表示的平均風向。 | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 第10天預報風速公里/小時] | 十天的天氣預報。 12小時預測期內最大持續風速的預測。<br>風被視為向量；因此，風必須有方向和大小（速度）。 預報中報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第10天預報風速英里/小時] | 十天的天氣預報。 12小時預測期內最大持續風速的預測。<br>風被視為向量；因此，風必須有方向和大小（速度）。 預報中報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第14天預測日曆日氣溫最高攝氏度] | 十四天的天氣預報。 指定日的午夜至午夜每日最高溫度。 攝氏度溫度 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第14天預測日曆日氣溫最高華氏度] | 十四天的天氣預報。 指定日的午夜至午夜每日最高溫度。 溫度（華氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第14天預測日曆日氣溫最低攝氏度] | 十四天的天氣預報。 指定日的午夜至午夜每日最低溫度。 攝氏度溫度 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第14天預測日曆日溫度最低華氏度] | 十四天的天氣預報。 指定日的午夜至午夜每日最低溫度。 溫度（華氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第14天預測雲覆蓋英里] | 十四天的天氣預報。 白天平均雲覆蓋率以百分比表示。 以英里為單位的距離。 | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 第14天預報雲封面公里] | 十四天的天氣預報。 白天平均雲覆蓋率以百分比表示。 距離（以公里為單位）。 | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 第14天預測QPF英吋 | 十四天的天氣預報。 24小時內預測可測降水量（液體或液體當量）。 以英吋計的降水 | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 第14天預測QPF毫米] | 十四天的天氣預報。 24小時內預測可測降水量（液體或液體當量）。 以毫米為單位的降水 | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 第14天預報QPF雪公分] | 十四天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪公分 | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第14天預測QPF雪英吋] | 十四天的天氣預報。 預測12或24小時預報期內可測降水量為雪。 以公分計。 降雪量（英吋） | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 第14天預測UV指數] | 十四天的天氣預報。 12小時預測期間的最大UV索引。 | `weather.forecast.day14Forecast.uvIndex` |
| 第14天預報風向 | 十四天的天氣預報。 以磁記號表示的平均風向。 | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 第14天預報風速公里/小時] | 十四天的天氣預報。 12小時預測期內最大持續風速的預測。<br>風被視為向量；因此，風必須有方向和大小（速度）。 預報中報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時風速 | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第14天預報風速英里/小時] | 十四天的天氣預報。 12小時預測期內最大持續風速的預測。<br>風被視為向量；因此，風必須有方向和大小（速度）。 預報中報告的風資訊相當於10分鐘的平均風速。 風速的突然或短暫變化被稱為「風刮」，並報告在單獨的資料場中。 風向總是被表示為「從風吹來」，意思是北風從北向南吹。 如果你在北風中面對北風，風就會吹向你。 朝南，北風在你後面。 每小時以英里計的風速 | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 觸發器 {#triggers}

觸發器根據各種輸入來定義語義天氣條件。

| 欄位 | 說明 | XDM路徑 |
| --- | ---- | --- |
| [!UICONTROL 產品觸發器] | 指出何種條件適合促進某些類別產品的銷售。  它們會對應至整數點。 您可從IBM取得完整清單。 | `weather.productTriggers` |
| [!UICONTROL 相對觸發器] | 人類感知的相對條件。 熱或冷。 它們會對應至整數點。 您可從IBM取得完整清單。 | `weather.relativeTriggers` |
| [!UICONTROL 惡劣天氣觸發] | 表明各種惡劣天氣，如颶風或過度降雨。 | `weather.severeTriggers` |