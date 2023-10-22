# HR_Analytics_Pbi

- Created a duplicate file, parameter and functions to manipulate the data
  
- Created Calendar dimension using the blank query :
        = List.Dates
          (#date(2022,1,1),
          365,
          #duration(1,0,0,0))
  
- DAX Measures used :
      Leave% = ([Total Leave Count]/[Total Working days])
      Month = STARTOFMONTH('Master Data'[Date])
      Present% = ([Total Present count]/[Total Working days])
      Total Employees = DISTINCTCOUNT('Master Data'[Emp ID])
      Total Leave Count = sum('Master Data'[Total Leaves])
      Total Present count = sum('Master Data'[Total Days Present])
      Total WFH days = sum('Master Data'[Total WFH])
      Total Working days = 
                            var totaldays = count('Master Data'[Value])
                            var nonworking = CALCULATE(count('Master Data'[Value]), 'Master Data'[Value] in {"WO", "HO"})
                            return
                            totaldays-nonworking
      WFH% = divide([Total WFH days],[Total Working days],0)
  
- DAX Columns "
      Month = STARTOFMONTH('Master Data'[Date])
      Total Days Present = switch(true(),
                          'Master Data'[Value] = "P", 1,
                          'Master Data'[Value] = "HPL", 0.5,
                          'Master Data'[Value] = "WFH", 1,
                          'Master Data'[Value] = "HSL", 0.5,
                          'Master Data'[Value] = "HFFL", 0.5,
                          'Master Data'[Value] = "HLWP", 0.5,
                          'Master Data'[Value] = "HWFH", 0.5,
                          'Master Data'[Value] = "HML", 0.5, 0)
      Total Leaves = switch(true(), 
                          'Master Data'[Value] = "PL", 1,
                          'Master Data'[Value] = "SL", 1,
                          'Master Data'[Value] = "FFL", 1,
                          'Master Data'[Value] = "BL", 1,
                          'Master Data'[Value] = "LWP", 1,
                          'Master Data'[Value] = "BRL", 1,
                          'Master Data'[Value] = "ML", 1,
                          'Master Data'[Value] = "HPL", 0.5,
                          'Master Data'[Value] = "HSL", 0.5,
                          'Master Data'[Value] = "HFFL", 0.5,
                          'Master Data'[Value] = "HLWP", 0.5,
                          'Master Data'[Value] = "HBRL", 0.5,
                          'Master Data'[Value] = "HWFH", 0.5,
                          'Master Data'[Value] = "HML", 0.5,0)
      Total WFH = switch(True(),
                          'Master Data'[Value] = "WFH", 1,
                          'Master Data'[Value] = "HWFH", 0.5, 0)

- Used Line and Clustered Column chart, Slicer, Card, Matrix, Funnel Chart, and Area chart to visualize the data and do data Analysis.
  
- Used Page Navigator to change the pages.
  
- Added Bookmarks for easy navigation.

- Conclusion :
      - More attendance on Tuesdays
      - More leaves and WFH on Fridays
      - More leaves in May
      - More WFH in June
      - Most leaves are Paid, followed by leave without pay and Sick leave
