```
Donuts: Summary % of Total = 

VAR Height = 26
VAR Width = 128
VAR Radius = (height/2) - 2.5
VAR Circle = 2*PI()* radius
VAR Callout = FORMAT( [Summary: % of Total], "0.0%;-0.0%")
VAR Filled = IF( [Summary: % of Total] >= 0,([Summary: % of Total] *Circle),0)
VAR Grey = (1-[Summary: % of Total]) * Circle 
VAR Offset = 0.25*Circle
VAR Sort = IF([Summary: % of Total] <0, 1000+ABS([Summary: % of Total]), 10000+ [Summary: % of Total])

RETURN
IF(
  NOT(ISBLANK([Summary: % of Total])) && ( ISINSCOPE('Dim: Tickets'[distance]) || ISINSCOPE('Dim: Events'[name]) ), 
  "data:image/svg+xml;utf8, 
  <svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 " & Width & " " & Height & "' >
   /*" & Sort & "*/ 
  <rect width='120' height='26' style='fill:rgba(0,0,255,0);stroke-width:2;stroke:'/>
  <circle class='background' cx='" & Radius + 20 & "' cy='50%' r='" & Radius & "' fill='transparent' stroke='hashtag#dde1e3' stroke-width='5' />
  <circle class='segment' cx='" & Radius + 20 & "' cy='50%' r='" & Radius & "' fill='transparent' stroke='hashtag#2589BD' stroke-width='5' stroke-dasharray='" & Filled & " " & Grey & "' stroke-dashoffset='" & offset & "'></circle>
  <style>
   .percent {
   font: normal 16pt Segoe UI;
   }
   </style>
  <text x='" & Radius*10 + 16 & "' y='60%' class='percent' text-anchor='end' fill='#666666' alignment-baseline='middle' >" & Callout &"</text>
  </svg>"
)
```
