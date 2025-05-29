# Create a Data Dictionary for your report in one DAX expression

'''
Data Dictionary = 
VAR _columns = SELECTCOLUMNS(
    FILTER(
        INFO.VIEW.COLUMNS(),
        [Table] <> "Data Dictionary" && NOT([IsHidden])
    ),
    "Type", "Column",
    "Name", [Name],
    "Description", [Description],
    "Location", [Table],
    "Expression", [Expression]
)

VAR _measures = SELECTCOLUMNS(
    FILTER(
        INFO.VIEW.MEASURES(),
        [Table] <> "Data Dictionary" && NOT([IsHidden])
    ),
    "Type", "Measure",
    "Name", [Name],
    "Description", [Description],
    "Location", [Table],
    "Expression", [Expression]
)

VAR _tables = SELECTCOLUMNS(
    FILTER(
        INFO.VIEW.TABLES(),
        [Name] <> "Data Dictionary" && [Name] <> "Calculations" && NOT([IsHidden])
    ),
    "Type", "Table",
    "Name", [Name],
    "Description", [Description],
    "Location", BLANK(),
    "Expression", [Expression]
)

VAR _relationships = SELECTCOLUMNS(
    INFO.VIEW.RELATIONSHIPS(),
    "Type", "Relationship",
    "Name", [Relationship],
    "Description", BLANK(),
    "Location", [FromTable],
    "Expression", [Relationship]
)

VAR unified_table = UNION(_columns, _measures, _tables, _relationships)

VAR add_number_char = ADDCOLUMNS(unified_table, "DAX_NumbChar", LEN([Expression]))

VAR DAX_heaviness = ADDCOLUMNS(add_number_char, "DAX Expression Heaviness",
SWITCH(TRUE(),
[Type] = "Relationship","No Dax",
[DAX_NumbChar] > 1000, "4-Ultra Heavy",
[DAX_NumbChar] > 500, "3-Heavy",
[DAX_NumbChar] > 150, "2-Medium",
[DAX_NumbChar] > 0, "1-Light",
"No DAX"))

RETURN

DAX_heaviness
'''
