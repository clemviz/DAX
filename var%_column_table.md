# Display Variation % nicely in a column

> Nice to add as a column in a Power BI table

```DAX
Var% Formatted =

VAR _value = [Your Var% Metric]

RETURN Switch (TRUE(),
                _value > 0, FORMAT(_value,"🡵 00.00%"),
                _value < 0, FORMAT(abs(_value),"🡶 (00.00%)"),
                _value = 0, _value
                )
```
*To go further conditional format the increase or decrease in green or red*
