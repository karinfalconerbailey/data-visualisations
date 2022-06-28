---
follows: data
id: litvis
---

@import "../lectures/css/datavis.less"

# GLOBAL LEVELS OF AIR POLLUTION

{(whoami|} 
Karin Falconer-Bailey | karin.falconer-bailey@city.ac.uk {|whoami)}

While there are debates around the time which the climate change movement began, it is undeniable that within the past decade we have seen significant amounts of discussion regarding the Earth's environmental changes. The United States Environment Protection Agency (EPA) identifies the two umbrella sources of climate change as "*human drivers*" and "*natural drivers*" (EPA, 2022). Under human drivers, we have occurrences such as deforestation and road construction while natural drivers are accounted for by natural disasters, the sun's intensity, and so forth. Air pollution, both a natural and human driver, has an interchangeable relationship with climate change. In the sense that air pollutants contribute to climate change, and climate change worsens the quality of air.

This study focuses on data mainly sourced from *Our World in Data*, separately sourcing the global indoor and outdoor air pollution CSV file and the regional indoor and outdoor air pollution CSV file. This was pre-processed in Microsoft Excel to better its readability for creating data visualisations. Such visualisations have been conducted with the aim of answering the following research questions. 

{(questions|}

1. How does pollution differ within each region from 1990 to 2019?

2. Across the years, is there a consistency in the regions that display the highest levels of air pollution?

3. Does it appear that more countries have become conscious of climate change and thus, their contributions to air pollution?

{|questions)}

{(visualization|}

```elm {v}
regionData =
    dataFromColumns []
     << dataColumn "Entity" (strColumn "Entity" regionTable |> strs)
     << dataColumn "Year" (numColumn "Year" regionTable |> nums)
     << dataColumn "Type of pollution" (strColumn "Type of pollution" regionTable |> strs)
     << dataColumn "Rate of death (per 100,000)" (numColumn "Rate of death (per 100,000)" regionTable |> nums) 

encRegion =
    encoding
        << position X
            [ pName "Year", pTemporal, pAxis [ axTicks True, axDomain False ] ]
        << position Y
            [ pName "Rate of death (per 100,000)", pQuant, pAxis [ axTicks False, axDomain False ], pTitle "" ]
        << column 
            [ fName "Type of pollution", fHeader [ hdTitle "Air pollution deaths by region (1990 - 2019)" ]
            ]
        << color
            [ mCondition (prParamEmpty "mySelection")
                [ mName "Entity", mScale [ scScheme "browns" [] ] ]
                [ mStr "blue" ]
            ]
        << opacity
            [ mCondition (prParamEmpty "mySelection")
                [ mNum 1 ]
                [ mNum 0.1]
            ]
        << tooltips
            [ [ tName "Year", tQuant ]
                , [ tName "Rate of death (per 100,000)", tQuant ]
            , [ tName "Entity" ]
            ]
```

```elm {l=hidden v interactive}
regionSelect : Spec
regionSelect =
    let
        ps =
            params            
                << param "mySelection" [ paSelect sePoint [ seFields [ "Entity" ] ]
                , paBindLegend "click"
                ]       
    in
    toVegaLite
        [ width 200, height 200, regionData [], ps [], encRegion [], area [ maInterpolate miMonotone ]  ]
```

```elm {l=hidden}
parameters =
    params
        << param "yearSlider"
            [ paValue (dataObject [ ( "Year", num 1990 ) ])
            , paSelect sePoint []
            , paBind (ipRange [ inName "Year", inMin 1990, inMax 2019, inStep 1 ])
            ]
        << param "Zoom" [ paValue (num 100), paBind (ipRange [ inName "Zoom", inMin 100, inMax 300, inStep 10  ]) ]              
        << param "cenLambda" [ paValue (num 0), paBind (ipRange [ inName "λ", inMin -150, inMax 150, inStep 1 ]) ]
        << param "cenPhi" [ paValue (num 0), paBind (ipRange [ inName "𝜙", inMin -90, inMax 90, inStep 5 ]) ]
```

```elm {l=hidden}
pollutionData : List DataColumn -> Data
pollutionData =
            dataFromColumns []
                << dataColumn "Entity" (strColumn "Entity" geoTable |> strs)
                << dataColumn "Year" (numColumn "Year" geoTable |> nums)
                << dataColumn "Indoor deaths" (numColumn "Indoor deaths" geoTable |> nums)
                << dataColumn "Outdoor deaths" (numColumn "Outdoor deaths" geoTable |> nums)
```
```elm {l=hidden v interactive}
choropleth01 : Spec
choropleth01 =
    let        
        cfg =
            configure
                << configuration (coView [ vicoStroke Nothing ])
                << configuration (coLegend [ lecoOrient loBottomLeft, lecoOffset -40 ])

        countryData =
            dataFromUrl "https://gicentre.github.io/data/geoTutorials/world-110m.json" [ topojsonFeature "countries1" ] 
       
        proj =
            projection [ prType equirectangular, prNumExpr "Zoom" prScale, prCenterExpr "cenLambda" "cenPhi" ]

        trans =
            transform
                << lookup "Entity" countryData "properties.name" (luAs "geo")
                << filter (fiExpr "isValid(datum.geo)")
                << filter (fiSelection "yearSlider")

        enc =
            encoding
                << shape [ mName "geo", mGeo ]
                << color [ mName "Indoor deaths", mQuant, mTitle "Indoor deaths", mScale [ scScheme "browns" [] ] ]
                << tooltips [ [ tName "Entity", tTitle "Entity" ],[ tName "Indoor deaths", tQuant, tTitle "Rate of indoor deaths (per 100,000)" ] ]

    in
    toVegaLite [ width 600, height 250, title "Indoor air pollution deaths by country" [ tiOffset 10 ], cfg [], countryData, trans [], enc [], parameters [], proj, pollutionData [], geoshape [] ]
```

```elm {l=hidden v interactive}
choropleth02 : Spec
choropleth02 =
    let        
        cfg =
            configure
                << configuration (coView [ vicoStroke Nothing ])
                << configuration (coLegend [ lecoOrient loBottomLeft, lecoOffset -40 ])

        countryData =
            dataFromUrl "https://gicentre.github.io/data/geoTutorials/world-110m.json" [ topojsonFeature "countries1" ] 
        
        proj =
            projection [ prType equirectangular, prNumExpr "Zoom" prScale, prCenterExpr "cenLambda" "cenPhi"  ]

        trans =
            transform
                << lookup "Entity" countryData "properties.name" (luAs "geo")
                << filter (fiExpr "isValid(datum.geo)")
                << filter (fiSelection "yearSlider")

        enc2 =
            encoding
                << shape [ mName "geo", mGeo ]
                << color [ mName "Outdoor deaths", mQuant, mTitle "Outdoor deaths", mScale [ scScheme "browns" [] ] ]
                << tooltips [ [ tName "Entity", tTitle "Entity" ],[ tName "Outdoor deaths", tQuant, tTitle "Rate of outdoor deaths (per 100,000)" ] ]
    in
    toVegaLite [ width 600, height 250, title "Outdoor air pollution deaths by country"  [ tiOffset 10 ], cfg [], countryData, trans [], enc2 [], parameters [], proj, pollutionData [], geoshape [] ]
```

{|visualization)}

{(insights|}

**Research question 01** 

**Note**: All mentions of the death rate or rate of death are measured per 100,000.

To begin the analysis of the above visualisations and display their effectiveness, I will proceed by answering question 01 *How does pollution differ within each region from 1990 to 2019?*

By simply directing attention to the first two categories within the air pollution observation: air pollution (total) and indoor, it is evident that there is a negative relationship between the rate of death and the year. In other words, the rate of death decreases within each region as the year progresses. Among the remaining death rates caused by the pollutants outdoor and the outdoor ozone pollution, less of a noticeable fluctuation is present from 1990 to 2019. Instead, all regional changes across almost three decades are very minimal.

*African region* | The overall total of air pollution for the region of Africa in 1990 began at 232.28 per hundred thousand, with the majority of its composition deriving from indoor pollution (201.93). Over the course of 29 years, Africa exhibits a 36 percent decline in its total air pollution to 148.27. The continent's indoor air pollution decreased by 49 percent, and outdoor air pollution experienced a slight increase from 29.83 to 43.97 (47.4 percent). 

*Eastern Mediterranean region* | Eastern Mediterranean region holds the second-highest air pollution total of the remaining 5 regions; with a 1990 death rate of 204.33, marginally behind the rate of the African region. In 2019, it was observed that total air pollution decreased to 140.19, indoor air pollution rates of death declined by 87.16 deaths per 100,000, and outdoor pollution appreciated slightly by 20 deaths per 100,000.

*European region* & *Region of the Americas* | Both the European region and the Region of the Americas are in close proximity, in relation to all forms of air pollution exhibited in the first visualisation. In 1990, the European region displays an air pollution total of 72.88 which drops by approximately 50 percent in 2019. Similarly, the Region of the Americas presents a slightly lower starting rate of 56.56 declining to 23.93 - a reduction of 57.69 percent.

*South-East Asian region* | Among all regions, South-East Asia obtained the highest number of air pollution related deaths in 1990. While the number of deaths was measured at 252.94 per hundred thousand, this steadily decreased to 147.17 in 2019.

*Western Pacific region* | The Western Pacific region too shows evidence of change from 1990 to 2019. Total air pollution decreased by 60 percent, deaths caused by indoor air pollution showed an impeccable reduction by a near 90 percent and outdoor air pollution showed a 2 percent increase in the rates of death per 100,000.

The outdoor ozone pollution exhibits no notable change across all regions.

**Research question 02**

This section focuses on the second question of research, *'Across the years, is there a consistency of the regions that display the highest levels of air pollution?'*

As the 29-year time duration of which air pollution across regions has been measured, it is inevitable that each region has experienced some extent of fluctuation in its levels of air pollution. 

**Air pollution (total)**

In the 1990s, the leading region which obtained the highest amounts of deaths was South-East Asia. This was followed by Africa, the Western Pacific, the Eastern Mediterranean, Europe and lastly the Region of the Americas. However, this experienced a slight change over the years and in 2019, Africa became the leading region, followed by South-East Asia, the Eastern Mediterranean, and the Western Pacific region. Europe and the Americas maintained their positions.

**Indoor air pollution**

Again, Africa was dominant in the 1990s and in 2019 with the highest rate of deaths caused by indoor air pollutants. This was followed by South-East Asia, the Western Pacific, the Eastern Mediterranean, the region of the Americas and ensuing Europe. In 2019, the only two regions which altered their positions were the Western Pacific and the Eastern Mediterranean.

**Outdoor air pollution**

Outdoor air pollution presents results unlike the previous two categories.

The Eastern Mediterranean region attained the utmost proportion of deaths per 100,000 in the 1990s and in 2019. This was followed by the Western Pacific region, then Europe, South-East Asia, The Americas, ensued by Africa.

*Question 2 summary*
^^^elm{m=(tableSummary 6 rankTable)}^^^

```elm {l=hidden}
rankTable : Table
rankTable =
    """Region,APT(1990),APT(2019),IAP(1990),IAP(2019),OAP(1990),OAP(2019)
    Africa,2,1,1,1,6,4
    Eastern Meditteranean,4,3,4,3,1,1
    Europe,5,5,6,6,3,5
    The Americas,6,6,5,5,5,6
    South-East Asia,1,2,2,2,4,2
    Western Pacific,3,4,3,4,2,3"""
        |> fromCSV
```
*APT - Air pollution total*
*IAP - Indoor air pollution*
*OAP - Outdoor air pollution*

**Research question 03**

Here, the final research question is discussed, 'Does it appear that more countries have become conscious of climate change and thus, lowering their contributions to air pollution?'

From the indoor air pollution choropleth, through the use of the tooltip, we can instantly identify which countries exhibit the highest rates of deaths from indoor and outdoor air pollution.

**Indoor air pollution**

In 1990, these countries were: Niger, the Central African Republic, Ethiopia, Afghanistan, Myanmar, Cambodia, Somalia, Laos, and the Solomon Islands. In 2019, it is drastically evident that the above-listed countries reduced their contributions to indoor air pollution. While others have completely shifted out of the *red zone*, others such as the Solomon Islands, Somalia, and the Central African Republic continued to display high levels of deaths.

**Outdoor air pollution**

In regard to outdoor air pollution in 1990, there are two countries that are distinguishable: Egypt and the United Arab Emirates. Over the 29-years, outdoor air pollution becomes somewhat significantly worse among countries in the region of Africa, and South-East Asia. Egypt’s rate of death merely decreases by 15 per 100,000. Uzbekistan experiences a sizable increase along with many surrounding countries.

While there is a fluctuation between which countries exhibit greater contributions to air pollution, the increases are very minimal.

{|insights)}

{(designJustification|}

**COLOUR**

Not a wide variety of colour schemes and hues appear in the final design of each individual visualisation, instead, a continuous scheme is present across all visualisations. 

Various colour schemes and colour shades were experimented with within the creation of my design. I first began with a complementary colour scheme, using the [Coolors](https://coolors.co/) website to generate my own colour palette. However, due to the nature of the choropleths, I struggled to successfully encode colours to each range. For example, an indoor air pollution death rate between 0 and 50 would be associated with a light shade of red.

Following the study of Stone (2016), I concluded to encode VegaLite's *browns* built-in colour scheme into my visualisations. Although the successful use of colours can "well enhance and clarify a presentation", this was not the sole reason for such a colour scheme (Stone, 2006, pg.1). I have previously studied the connotations and symbolism of colour, and it can be said that brown is positively associated with the earth. Conversely, a negative association is death and therefore, the use of brown appeared fitting for the topic.

In the *area graph*, I too implemented this colour scheme. Though, before engaging in any interaction, a light blue hue is used. This acts to mimic and relay the message of the visualisation, *climate change* and thus, rising sea levels.

**INTERACTION**

Interaction plays a vital role in each visualisation of this study and in fact, there are numerous elements in both visualisations. This stems from Munzer (2014, pg.9), where there is a heavy emphasis on the significance of interactivity in visualisations.

**Area graph**: The air pollution area graph requires the user to hover over the visualisation in order to provide an overview and to be informed of specific outputs of information i.e. year, entity, and the rate of death (per 100,000). Through interaction, the user can either left-click the legend; presenting a singular regional output across all four graphs. Alternatively, the user can combine shift + left-click to select multiple observations across the four graphs. This implementation of interaction corresponds with aspects of Shneiderman's study, one, in particular, being to "enable [a] selection of regions" (Shneiderman, 1996, pg.337). Embedding selection features allow the viewer to extract particular insights they wish to derive by "controlling the contents of the display... by eliminating unwanted items" (Shneiderman, 1996, pg.340).

**Choropleth maps**: Both of the choropleth maps feature the option of selecting a year from 1990 to 2019. While Schneiderman (1996, pg.341) refers to this as *"advanced filtering"*, combined with the addition of the previously discussed hover function, this too relates to Munzer's manipulation of view. The ability to alter the map's scale through zooming into and out of the visualisation, and panning left to right corresponds to two of the three components of navigation: "zooming, panning and translating" (Munzer, 2014, pg.254). Through this, the user is able to lessen how much data they are exposed to, and in the view of Munzer, this approach makes it "very straightforward for users to understand" (Munzer, 2014, pg.299).

**SIZING**

Sizing is an element of composition that can be beneficial in the overall outcome of design. The initial idea for the choropleth maps were to include a miniature map of the opposing design i.e. beside the main map of the indoor air pollution choropleth, there would be a small preview of the outdoor air pollution choropleth. However, this caused issues with other features of the design, such as the ability to manipulate the view. Due to this, I came to consider how I could allow for comparisons between the two maps in another manner. Assigning specific quantities, in this case, width 600 and height 250, allows for both choropleths to be visualised simultaneously. This makes it more convenient for the user as they do not have to "browse through multiple pages or navigate through different selections" (Kirk, 2019, pg.298).

{|designJustification)}

{(validation|}

**BUGS**

Minor bugs have presented themselves in the final outcome of my visualisation. Within the area graph, the x-axis of the 'Year' observation is presented as a decimal as opposed to a whole number, corresponding to the year. Although this does not detract from the graph's legibility, as the tooltip displays the year, this was not the intent of my visualisation and thus, can be classified as a weakness of the design. 

**TIME-SERIES ANALYSIS**

Given the nature of my datasets, it was important that I selected suitable methods of visualisation. Although time-series analysis was displayed for the regional dataset, it was not displayed for the data presented in the choropleths, and only a spatial analysis was provided. Despite the number of observations, I believe that my design would have benefitted from further temporal analysis. When the user selects a year, the other information falls into an *out of sight out of mind* state. According to Andrienko et al. (2013, pg.260), spatial analysis "offers only very limited opportunities for temporal analysis" and thus, "it is necessary to combine spatial displays with temporal displays such as time graphs".

**HUMAN IN THE LOOP & COMPUTER IN THE LOOP**

All of my visualisations acknowledge the importance of the human in the loop and the computer in the loop, incorporating both practices. While inputting a series of commands form a visualisation, acting as the *computer in the loop*, my design requires human interference to make comparisons and decipher exactly what is being presented. In this case, the computer in the loop has been designed to "augment human capabilities, rather than completely replace the human in the loop" (Munzer, 2014, pg.3). I have too used *computer in the loop* and *human in the loop* to acknowledge the problems identified by the computer (as shown previously in the **BUGS** section), and conduct visualisations which coincide with my questions of research. 

{|validation)}

{(references|}

1.	Andrienko, G., Andrienko, N., Bak, P., Keim, D., Wrobel, S. (2013) Visual Analytics of Movement. Springer-Verlag : Berlin, Heidelberg, pg.260.

2.	Elliot, A., Fairchild, M., Franklin, A. (2015) Handbook of Color Psychology. Cambridge Press.

3.	Elliot, J. A. and Maier, A. M. (2013) Color Psychology: Effects of Perceiving Color on Psychological Functioning in Humans, *Annual Review of Psychology*. doi: 10.1146/annurev-psych-010213-115035

4.	EPA (2022) Causes of climate change, EPA. Available at: https://www.epa.gov/climatechange-science/causes-climate-change (Accessed 15th April 2022)

5.	Franconeri, S., Padilla, L., Shah, P., Zacks, J. and Hullman, J. (2021) The science of visual data communication: What works, Psychological Science in the Public Interest, 22(3), pg.110-161. doi:10.1177/15291006211051956

6.	Gleicher, M. et al. (2011) Visual comparison for information visualization, Information Visualization, 10(4), pg. 289–309. doi: 10.1177/1473871611416549 

7.	Kirk, A. (2019) Data Visualisation: A Handbook For Data Driven Design, 2nd edition. Sage Publications, pg. 277-285.

8.	Munzner, T. (2014) Visualization analysis and design. CRC Press, pg.1-4,9,243-254,299.

9.	Shneiderman, B. (1996) The Eyes Have It: A Task by Data Type Taxonomy for Information Visualisations, Proceedings of the IEEE Symposium on Visual Languages, pg.337,340-341.

10.	Stone, M. (2006) Choosing Colors for Data Visualisation, Perceptual Edge, pg.1

{|references)}











