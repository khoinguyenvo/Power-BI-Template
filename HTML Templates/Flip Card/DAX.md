```
HTML - BP = 
VAR SourceTable =
FILTER(
    ADDCOLUMNS(
        ALL( Stores[Country] ),
        "@Rank",
        RANK(
            DENSE,
            ALL( Stores[Country] ),
            ORDERBY( 
                [CY Cummulative], DESC,
                Stores[Country], ASC
            )
        ),
        "@Value", [CY Cummulative],
        "@YoYDiff", [YoY Change (Indicator)],
        "@TextColor",
        SWITCH(
            TRUE(),
            CONTAINSSTRING( [YoY Change (Indicator)], [Up Arrow]) , "#44A676",
            CONTAINSSTRING( [YoY Change (Indicator)], [Unchanged Symbol]), "midColor",
            CONTAINSSTRING( [YoY Change (Indicator)], [Down Arrow]), "#D32913"
        )
    ),
    [@Rank] <= 3
)

VAR Formats =
SWITCH(
    SELECTEDVALUE( 'Parameter: Dynamic Sales Measure'[Sort] ),
    0, "#,#",
    1, "#,#",
    2, "$#,#"
)

VAR TitleColor = "#1B2940"
VAR SubtitleColor = "#7D899D"
VAR TextColor = "#273B5C"
VAR BorderColor = "#e3edf0"

VAR Subtitle = 
SWITCH(
    SELECTEDVALUE( 'Parameter: Dynamic Sales Measure'[Sort] ),
    0, "Total Orders Completed",
    1, "Units Sold",
    2, "Net Sales Profit"
)
& ", Current vs Period Year"

VAR HTMLTable =
ADDCOLUMNS(
    SourceTable,
    "@HTML", 
        "<tr style = ' height : 40px '>" &
    IF( [@Rank] <= 2,
        "<td style = 'width: 45% ; text-align:left; font-size: 20px; font-weight: 600; padding-left: 2%; color: "&TextColor&"; border-bottom: 1px solid "&BorderColor&"'>" & Stores[Country] & "</td>" &
        "<td style = 'width: 30% ; text-align:right; font-size: 20px; padding-right: 2%; font-weight: 600; color: "&TextColor&"; border-bottom: 1px solid "&BorderColor&"'>" & FORMAT( [@Value], Formats ) & "</td>" &
        "<td style = 'width: 25% ; text-align:left; font-size: 20px; padding-left: 5%; font-weight: 600; color:" & [@TextColor] &"; border-bottom: 1px solid "&BorderColor&"'>" & [@YoYDiff] & "</td>" &
        "</tr>",
        "<td style = 'width: 45% ; text-align:left; font-size: 20px; font-weight: 600; padding-left: 2%; color: "&TextColor&"'>" & Stores[Country] & "</td>" &
        "<td style = 'width: 30% ; text-align:right; font-size: 20px; padding-right: 2%; font-weight: 600; color: "&TextColor&"'>" & FORMAT( [@Value], Formats ) & "</td>" &
        "<td style = 'width: 25% ; text-align:left; font-size: 20px; padding-left: 5%; font-weight: 600; color:" & [@TextColor] &"'>" & [@YoYDiff] & "</td>" &
        "</tr>"
    )
)

VAR HTMLCode =
"<table>
    <caption style = 'height: 36px; text-align: left; font-weight: 600; font-size: 24px; color:"&TitleColor&"'>"&[Good Icon]&" Best Performance</caption>
    <caption style = 'height: 32px; text-align: left; font-size: 16px; color: "&SubtitleColor&"'>"&Subtitle&"</caption>"
& CONCATENATEX( HTMLTable, [@HTML],, [@Rank], ASC ) &
"</table>"

RETURN HTMLCode
```
