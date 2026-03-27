# Tableau Cheat Sheet: Business Performance

### 1. Year-Over-Year (YoY) % Change
The manual way to write this (better for custom formatting than Quick Table Calcs).
```sql
// (Current - Previous) / Previous
(SUM([Current Year Sales]) - SUM([Prior Year Sales])) 
/ SUM([Prior Year Sales])
```

### 2. Percent of Total (LOD Style)
Calculate a percentage that stays fixed even if you filter out certain rows.
```sql
// Individual Sales divided by the Total Sales across the whole dataset
SUM([Sales]) / SUM({ FIXED : SUM([Sales]) })
```

### 3. Z-Score (Outlier Detection)
Identify values that are significantly above or below the average.
```sql
// (Value - Average) / Standard Deviation
(SUM([Sales]) - WINDOW_AVG(SUM([Sales]))) 
/ WINDOW_STDEV(SUM([Sales]))
```

### 4. Goal Pacing
Calculate how much of the month has passed vs. how much of the goal is met.
```sql
// % of the month elapsed
DAY(TODAY()) / DAY(DATEADD('day', -1, DATEADD('month', 1, DATETRUNC('month', TODAY()))))
```
