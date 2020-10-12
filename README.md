# database_construction
This git repo is used to build the workflow for merging two existing databases, protein structure databank and kinetics databank.


## The second week

Problems: how to pull pdb data from URL and extract useful data, like `atom` and `SEQRES`.
Two parts are focus in this week.

1. The first part is to research on the documentation of package `pypdb` which is "A Python API for the RCSB Protein Data Bank". So I looked all the function, find `get_pdb_file()` function which can download specific pdb entry in specific format.
2. The next part is that I didn't find any related function in package `pypdb` which is able to solve our problems. So I wrote my own function using basic way, like list and loop to solve this probelm and get a list of `atom` and `SEQRES` which is what we want.
    
## The third week

Problems: I want to change the list I got into a dataframe which is doable and add columns to include id then merge multiple pdb. file.

This week from 2020.10.11 to 2020.10.12, I worked on how to use `pandas` package to manipulate data, like mergeing two data frames.

1. So I first used `split()` function to convert all the lists I got from last week into a `pandas` dataframs. I used `split()` to split a long string by white space. Then use `pd.DataFrame()` function to convert it. And use `concat()` to merge multiple dataframes.
    
2. I look around `MdTraj` package to do some data manipulation, like loading pdb file into memroy from URL, getting topology strcture to convert atoms into `pandas` dataframe,  using `stom_slice()` to slice atoms by indexs and so on.

