```
Orders Monthly Variance = 
-- IMAGE SIZE
VAR Width = 280
VAR Height = 26

-- CALCULATIONS
VAR ABSVar = [Total Orders] - [PM Orders]
VAR RELVar = DIVIDE( ABSVar, [PM Orders] )
VAR VarianceString = 
SWITCH(
    TRUE(),
    RELVar > 0 || RELVar < 0, FORMAT( ABS( RELVar ), "0%" ) & " " & FORMAT( ABSVar, "+#,#;-#,#" ),
    BLANK()
)
VAR ComparisonString = IF( RELVar > 0 || RELVar < 0, "vs. PM (" & FORMAT([PM Orders],"#,#") & ")", "Unchanged" )
VAR Arrow = 
SWITCH(
    TRUE(),
    RELVar > 0, [Up Arrow (SVG)],
    RELVar = 0, [Em Dash (SVG)],
    RELVar < 0, [Down Arrow (SVG)]
)

VAR Color = 
SWITCH(
    TRUE(),
    RELVar > 0, [Positive Color],
    RELVar = 0, [Grey],
    RELVar < 0, [Negative Color]
)

-- CREATE HTML IMAGE OF MONTH OVER MONTH VARIANCE
VAR HTMLCode = 
"
<div xmlns='http://www.w3.org/1999/xhtml'>
    <span xmlns='http://www.w3.org/1999/xhtml' style='vertical-align: middle; font-size: 14px'>
    "&SUBSTITUTE(Arrow,"fillcolor",Color)&"
    </span>
</div>
"

-- FINAL SVG IMAGE CODE
VAR SVGImage = 
[SVG Header] &
"
<svg width='"&Width&"' height='"&Height&"' viewBox='0 0 "&Width&" "&Height&"' xmlns='http://www.w3.org/2000/svg'>" & [CSS] & "
    <foreignObject x='0' y='4' width='100%' height='100%'>" & HTMLCode & " </foreignObject>
    <g class='text'>
        <text x='28' y='20'>
            <tspan fill='"&Color&"'>"&VarianceString&"</tspan>
            "&[White Space]&
            "<tspan class='details'>"&ComparisonString&"</tspan>
        </text>
    </g>
</svg>
"

RETURN SVGImage
```
