```
Bar: Repeat Customers =

VAR MAXActual = [Repeat Customers]
VAR MAXTarget = [Total Customers]
VAR AXISRANGE = MAXX(
    {
        MAXActual,
        MAXTarget
    },
    [Value]
)
VAR PERCENTAGEFILL = MAXActual/AXISRANGE*326

VAR FillColor = 
SWITCH( 
    TRUE(),
    [New Customers] < [Repeat Customers], "#2589BD", 
    [New Customers] = [Repeat Customers], "#5C5C5C",
    "#8C2C35"
)

RETURN
"data:image/svg+xml;utf8," & "
    <svg width='328' height='26' viewBox='0 0 328 12' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' overflow='visible'>
        <rect id='fill' x='0' y='0' rx='4' width='328' height='8' fill='#E6E6E6' ></rect>
        <rect id='fill' x='0' y='0' rx='4' width="& "'"& PERCENTAGEFILL &"'"&" height='8' fill='"&FillColor&"' ></rect>
    </svg>
"
```
