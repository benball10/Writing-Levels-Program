# Program that returns the level of each segment

import numpy as np
import pandas as pd

# Reading in table from Excel
# Excel table must have column titles (Ex: Level 1, Level 2, etc.)
df = pd.read_excel(r"C:\Users\Benjamin Ball\Documents\Python_Example.xlsx", index_col = None)

# Storing row and column lengths
row_count = df.shape[0]
col_count = df.shape[1]

# Adding new column of length row_count
new_array = np.array([0, 0])
new_array.resize(row_count, 1)

# Looping through entire table
i = 0
while i < row_count:
    j = 0
    while j < col_count:
        # Checking for first null value in the row
        if df.isnull().iloc[i][j] == True:
            new_array[i] = j + 1  # Change from "j + 1" to "j" if not including "Level 1" column in Excel
            break
        j += 1
        new_array[i] = col_count + 1
    i += 1

# Adding the column of levels to the end of the original table
df['Level of Segment'] = new_array

# Writing table to new Excel file
df.to_excel(r"C:\Users\Benjamin Ball\Documents\Python_Example2.xlsx", sheet_name = "sheet1", index = False)
