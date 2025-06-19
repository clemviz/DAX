# HTML Contents - Card Templates
*Requirements: Import the custom Visual HTML Content* <br>
*DAX expressions defining the contents of the cards. The style and appearance of the card themselves is done in Power BI.*

### #1
![image](https://github.com/user-attachments/assets/6914c9d6-04e6-434d-81de-3af815152e3e)

##### DAX Expression
```DAX
Card = 
var _value = FORMAT(Opportunity[Metric Value], "£#0,0")
var number = FORMAT([Metric No.],"#0,0")
var font_family = "Calibri" -- font family
var color = "#9696F5" -- Color of the number
return
"<span style='font-family:" & font_family & "; font-size:20px;'><b>" & _value & "</b>" & "<br>" & "<span style='color:" & color & "'>(#" & number & ")</span></span>"
```

**Good for displaying the Value and number together with accentuation of the value.**


