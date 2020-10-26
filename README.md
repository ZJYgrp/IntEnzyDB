**Download html file to view in a browser to have a full better view of jupyter notebook.**

**If you don't wanna downlaod, you can click md file in `code` tab to view part of them within GitHub directly.**

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

## The fourth week

Problems: We want to include all atoms and hetatms into one data frame.

1. I wrote two functions to return all info. 
    * `get_all_atom()` would return all atom, inclduing hetatm, ter, namely the whole part will be returned.                   
    * `get_atom_and_hetatm()` only return atom and hetatm.

2. I wrote a class of one pdb file which has all the methods which can return the desired attribution of one pdb file. And I tested all of them. They worked well.

## The fifth week

Problems: We want to create two tables for each pdb file, one is called general table, another is called atom_htmatm table and merge multiple of them into one longer table.

1. I wrote one function called `get_general_table()` which gets all the desired fields inclduing residue sequences.

2. Another function is called `get_atom_hetatm_table()` which only includes atom and htmatm, this table also joins with another atom mass table, the final table can show each atom mass.

At last, I fixed a bug from the previous week, our `get_missing_residue()` function can accommodate more missing residue types.
