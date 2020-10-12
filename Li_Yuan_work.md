
# Table of Content:
* [Li Yuan's second week work](#2)
* [Li Yuan's third week work](#3)
    * [Pandas convert](#31)
    * [MdTraj convert](#32)

<a id='2'></a>
# Li Yuan's second week work 

This is a set of basic examples of the usage and outputs of the various individual functions included in. There are generally three types of functions:

+ Functions that perform searches and return lists of PDB IDs
+ Functions that get information about specific PDB IDs
+ Other general-purpose lookup functions

The list of supported search types, as well as the different types of information that can be returned for a given PDB ID, is large (and growing) and is enumerated in the docstrings of pypdb.py. The PDB allows a very wide range of different types of queries, and so any option that is not currently available can likely be implemented based on the structure of the query types that have already been implemented. Please submit feedback and pull requests on GitHub.

### I didn't find any funcion in that package pypdb we can use to extract seqres and atom, so I only use get_pdb_file() function from that package to get the file and write my own function to do that.

### Preamble

We import this package pypdb and prepare some other things.


```python
%pylab inline
from IPython.display import HTML

## Import from local directory
import sys
sys.path.insert(0, '../pypdb')
from pypdb import *

## Import from installed package
# from pypdb import *

import pprint

%load_ext autoreload
%autoreload 2
```

    Populating the interactive namespace from numpy and matplotlib


## This function I wrote is to extract only the seqres as a list


```python
def get_seqres(pdb_id):
    """ Return the seqres sequence of a pdb file
    
    >>> get_seqres('4Z0L')
    >>> get_seqres('4lza')
    """
    pdb_file = get_pdb_file(pdb_id, filetype='pdb', compression=False) 
    # using a get_pdb_file() function from pypdb package to return a file with format 'pdb'.
    file1 = pdb_file.splitlines()
    # split this long string into list by \n.
    list_se = []
    for line in file1:
        if line[:6] == "SEQRES":
            list_se.append(line)
    return(list_se)
```


```python
get_seqres('4lza')[:20]
```




    ['SEQRES   1 A  195  MSE HIS HIS HIS HIS HIS HIS SER SER GLY VAL ASP LEU          ',
     'SEQRES   2 A  195  GLY THR GLU ASN LEU TYR PHE GLN SER MSE THR LEU GLU          ',
     'SEQRES   3 A  195  GLU ILE LYS MSE MSE ILE ARG GLU ILE PRO ASP PHE PRO          ',
     'SEQRES   4 A  195  LYS LYS GLY ILE LYS PHE LYS ASP ILE THR PRO VAL LEU          ',
     'SEQRES   5 A  195  LYS ASP ALA LYS ALA PHE ASN TYR SER ILE GLU MSE LEU          ',
     'SEQRES   6 A  195  ALA LYS ALA LEU GLU GLY ARG LYS PHE ASP LEU ILE ALA          ',
     'SEQRES   7 A  195  ALA PRO GLU ALA ARG GLY PHE LEU PHE GLY ALA PRO LEU          ',
     'SEQRES   8 A  195  ALA TYR ARG LEU GLY VAL GLY PHE VAL PRO VAL ARG LYS          ',
     'SEQRES   9 A  195  PRO GLY LYS LEU PRO ALA GLU THR LEU SER TYR GLU TYR          ',
     'SEQRES  10 A  195  GLU LEU GLU TYR GLY THR ASP SER LEU GLU ILE HIS LYS          ',
     'SEQRES  11 A  195  ASP ALA VAL LEU GLU GLY GLN ARG VAL VAL ILE VAL ASP          ',
     'SEQRES  12 A  195  ASP LEU LEU ALA THR GLY GLY THR ILE TYR ALA SER ALA          ',
     'SEQRES  13 A  195  LYS LEU VAL GLU SER LEU GLY GLY ILE VAL ASP SER ILE          ',
     'SEQRES  14 A  195  ILE PHE LEU THR GLU LEU THR PHE LEU ASP GLY ARG LYS          ',
     'SEQRES  15 A  195  LYS LEU ASP GLY TYR ASP ILE ILE SER LEU ILE LYS PHE          ',
     'SEQRES   1 B  195  MSE HIS HIS HIS HIS HIS HIS SER SER GLY VAL ASP LEU          ',
     'SEQRES   2 B  195  GLY THR GLU ASN LEU TYR PHE GLN SER MSE THR LEU GLU          ',
     'SEQRES   3 B  195  GLU ILE LYS MSE MSE ILE ARG GLU ILE PRO ASP PHE PRO          ',
     'SEQRES   4 B  195  LYS LYS GLY ILE LYS PHE LYS ASP ILE THR PRO VAL LEU          ',
     'SEQRES   5 B  195  LYS ASP ALA LYS ALA PHE ASN TYR SER ILE GLU MSE LEU          ']




```python
get_seqres('4Z0L')[:20]
```




    ['SEQRES   1 A  587  ALA ASN PRO CYS CYS SER ASN PRO CYS GLN ASN ARG GLY          ',
     'SEQRES   2 A  587  GLU CYS MET SER THR GLY PHE ASP GLN TYR LYS CYS ASP          ',
     'SEQRES   3 A  587  CYS THR ARG THR GLY PHE TYR GLY GLU ASN CYS THR THR          ',
     'SEQRES   4 A  587  PRO GLU PHE LEU THR ARG ILE LYS LEU LEU LEU LYS PRO          ',
     'SEQRES   5 A  587  THR PRO ASN THR VAL HIS TYR ILE LEU THR HIS PHE LYS          ',
     'SEQRES   6 A  587  GLY VAL TRP ASN ILE VAL ASN ASN ILE PRO PHE LEU ARG          ',
     'SEQRES   7 A  587  SER LEU ILE MET LYS TYR VAL LEU THR SER ARG SER TYR          ',
     'SEQRES   8 A  587  LEU ILE ASP SER PRO PRO THR TYR ASN VAL HIS TYR GLY          ',
     'SEQRES   9 A  587  TYR LYS SER TRP GLU ALA PHE SER ASN LEU SER TYR TYR          ',
     'SEQRES  10 A  587  THR ARG ALA LEU PRO PRO VAL ALA ASP ASP CYS PRO THR          ',
     'SEQRES  11 A  587  PRO MET GLY VAL LYS GLY ASN LYS GLU LEU PRO ASP SER          ',
     'SEQRES  12 A  587  LYS GLU VAL LEU GLU LYS VAL LEU LEU ARG ARG GLU PHE          ',
     'SEQRES  13 A  587  ILE PRO ASP PRO GLN GLY SER ASN MET MET PHE ALA PHE          ',
     'SEQRES  14 A  587  PHE ALA GLN HIS PHE THR HIS GLN PHE PHE LYS THR ASP          ',
     'SEQRES  15 A  587  HIS LYS ARG GLY PRO GLY PHE THR ARG GLY LEU GLY HIS          ',
     'SEQRES  16 A  587  GLY VAL ASP LEU ASN HIS ILE TYR GLY GLU THR LEU ASP          ',
     'SEQRES  17 A  587  ARG GLN HIS LYS LEU ARG LEU PHE LYS ASP GLY LYS LEU          ',
     'SEQRES  18 A  587  LYS TYR GLN VAL ILE GLY GLY GLU VAL TYR PRO PRO THR          ',
     'SEQRES  19 A  587  VAL LYS ASP THR GLN VAL GLU MET ILE TYR PRO PRO HIS          ',
     'SEQRES  20 A  587  ILE PRO GLU ASN LEU GLN PHE ALA VAL GLY GLN GLU VAL          ']



### This function I wrote is to extract only the atom sequence as a list


```python
def get_atom(pdb_id):
    """ Return the atom sequence of a pdb file
    
    >>> get_atom('4Z0L')
    >>> get_atom('4lza')
    """
    pdb_file = get_pdb_file(pdb_id, filetype='pdb', compression=False)
    # using a get_pdb_file() function from pypdb package to return a file with format 'pdb'.
    file1 = pdb_file.splitlines()
    list_atom = []
    for line in file1:
        if line[:4] == "ATOM":
            list_atom.append(line)
    return(list_atom)
```


```python
get_atom('4Z0L')[:10]
```




    ['ATOM      1  N   ALA A  33     113.744  17.524  85.910  1.00 75.99           N  ',
     'ATOM      2  CA  ALA A  33     114.749  17.116  86.884  1.00 76.70           C  ',
     'ATOM      3  C   ALA A  33     115.677  18.275  87.231  1.00 73.52           C  ',
     'ATOM      4  O   ALA A  33     116.176  18.367  88.354  1.00 75.48           O  ',
     'ATOM      5  CB  ALA A  33     115.548  15.934  86.358  1.00 78.19           C  ',
     'ATOM      6  N   ASN A  34     115.906  19.154  86.261  1.00 67.98           N  ',
     'ATOM      7  CA  ASN A  34     116.747  20.327  86.469  1.00 63.43           C  ',
     'ATOM      8  C   ASN A  34     116.113  21.264  87.492  1.00 60.58           C  ',
     'ATOM      9  O   ASN A  34     115.006  21.756  87.287  1.00 61.30           O  ',
     'ATOM     10  CB  ASN A  34     116.983  21.058  85.144  1.00 63.09           C  ']




```python
get_atom('4lza')[:10]
```




    ['ATOM      1  N   THR A   0     -27.785   5.217 -21.426  1.00 50.53           N  ',
     'ATOM      2  CA  THR A   0     -27.459   5.049 -19.974  1.00 49.41           C  ',
     'ATOM      3  C   THR A   0     -25.949   5.130 -19.667  1.00 46.13           C  ',
     'ATOM      4  O   THR A   0     -25.572   5.789 -18.699  1.00 44.22           O  ',
     'ATOM      5  CB  THR A   0     -28.153   3.815 -19.346  1.00 51.85           C  ',
     'ATOM      6  OG1 THR A   0     -27.919   3.787 -17.932  1.00 52.21           O  ',
     'ATOM      7  CG2 THR A   0     -27.688   2.516 -19.989  1.00 53.52           C  ',
     'ATOM      8  N   LEU A   1     -25.087   4.511 -20.480  1.00 43.20           N  ',
     'ATOM      9  CA  LEU A   1     -23.681   4.942 -20.481  1.00 42.39           C  ',
     'ATOM     10  C   LEU A   1     -23.615   6.356 -21.059  1.00 43.21           C  ']



<a id='3'></a>
# Li Yuan's third week work

<a id='31'></a>
## We first used pandas to convert a list into dataframe 

### First we used split() to split each string in the list returned by get_atom() function 


```python
import pandas as pd
```


```python
def get_atom(pdb_id):
    """ Return the atom sequence of a pdb file as a pandas dataframe
    
    >>> get_atom('4Z0L')
    >>> get_atom('4lza')
    """
    pdb_file = get_pdb_file(pdb_id, filetype='pdb', compression=False)
    # using a get_pdb_file() function from pypdb package to return a file with format 'pdb'.
    file1 = pdb_file.splitlines()
    list_atom = []
    for line in file1:
        if line[:4] == "ATOM":
            list_atom.append(line)
    list_s_atom = [s.split() for s in list_atom]
    # split each string in a list by white spaces
    df = pd.DataFrame(list_s_atom)
    # use DataFrame function to convert a list to dataframe
    df["id"] = pdb_id
    # add one id column to exsiting dataframe
    return(df)
```


```python
get_atom("4lza").head(11)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ATOM</td>
      <td>1</td>
      <td>N</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-27.785</td>
      <td>5.217</td>
      <td>-21.426</td>
      <td>1.00</td>
      <td>50.53</td>
      <td>N</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ATOM</td>
      <td>2</td>
      <td>CA</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-27.459</td>
      <td>5.049</td>
      <td>-19.974</td>
      <td>1.00</td>
      <td>49.41</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ATOM</td>
      <td>3</td>
      <td>C</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-25.949</td>
      <td>5.130</td>
      <td>-19.667</td>
      <td>1.00</td>
      <td>46.13</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ATOM</td>
      <td>4</td>
      <td>O</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-25.572</td>
      <td>5.789</td>
      <td>-18.699</td>
      <td>1.00</td>
      <td>44.22</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ATOM</td>
      <td>5</td>
      <td>CB</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-28.153</td>
      <td>3.815</td>
      <td>-19.346</td>
      <td>1.00</td>
      <td>51.85</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ATOM</td>
      <td>6</td>
      <td>OG1</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-27.919</td>
      <td>3.787</td>
      <td>-17.932</td>
      <td>1.00</td>
      <td>52.21</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ATOM</td>
      <td>7</td>
      <td>CG2</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-27.688</td>
      <td>2.516</td>
      <td>-19.989</td>
      <td>1.00</td>
      <td>53.52</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ATOM</td>
      <td>8</td>
      <td>N</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-25.087</td>
      <td>4.511</td>
      <td>-20.480</td>
      <td>1.00</td>
      <td>43.20</td>
      <td>N</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ATOM</td>
      <td>9</td>
      <td>CA</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-23.681</td>
      <td>4.942</td>
      <td>-20.481</td>
      <td>1.00</td>
      <td>42.39</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ATOM</td>
      <td>10</td>
      <td>C</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-23.615</td>
      <td>6.356</td>
      <td>-21.059</td>
      <td>1.00</td>
      <td>43.21</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ATOM</td>
      <td>11</td>
      <td>O</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-22.738</td>
      <td>7.137</td>
      <td>-20.688</td>
      <td>1.00</td>
      <td>41.35</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
  </tbody>
</table>
</div>



## Second we want to put a couple of pdb entries into one dataframe.


```python
def get_some_atom(L):
    """ Take a list with returning some atom parts of pdb files into one dataframe 
    
    >>> get_some_atom(["4lza", "4Z0L"])
    """
    frames = [get_atom(l) for l in L]
    return(pd.concat(frames))
```

## We test this function with a list ["4lza", "4Z0L]


```python
get_some_atom(["4lza", "4Z0L"])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ATOM</td>
      <td>1</td>
      <td>N</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-27.785</td>
      <td>5.217</td>
      <td>-21.426</td>
      <td>1.00</td>
      <td>50.53</td>
      <td>N</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ATOM</td>
      <td>2</td>
      <td>CA</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-27.459</td>
      <td>5.049</td>
      <td>-19.974</td>
      <td>1.00</td>
      <td>49.41</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ATOM</td>
      <td>3</td>
      <td>C</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-25.949</td>
      <td>5.130</td>
      <td>-19.667</td>
      <td>1.00</td>
      <td>46.13</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ATOM</td>
      <td>4</td>
      <td>O</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-25.572</td>
      <td>5.789</td>
      <td>-18.699</td>
      <td>1.00</td>
      <td>44.22</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ATOM</td>
      <td>5</td>
      <td>CB</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-28.153</td>
      <td>3.815</td>
      <td>-19.346</td>
      <td>1.00</td>
      <td>51.85</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ATOM</td>
      <td>6</td>
      <td>OG1</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-27.919</td>
      <td>3.787</td>
      <td>-17.932</td>
      <td>1.00</td>
      <td>52.21</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ATOM</td>
      <td>7</td>
      <td>CG2</td>
      <td>THR</td>
      <td>A</td>
      <td>0</td>
      <td>-27.688</td>
      <td>2.516</td>
      <td>-19.989</td>
      <td>1.00</td>
      <td>53.52</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ATOM</td>
      <td>8</td>
      <td>N</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-25.087</td>
      <td>4.511</td>
      <td>-20.480</td>
      <td>1.00</td>
      <td>43.20</td>
      <td>N</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ATOM</td>
      <td>9</td>
      <td>CA</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-23.681</td>
      <td>4.942</td>
      <td>-20.481</td>
      <td>1.00</td>
      <td>42.39</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ATOM</td>
      <td>10</td>
      <td>C</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-23.615</td>
      <td>6.356</td>
      <td>-21.059</td>
      <td>1.00</td>
      <td>43.21</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ATOM</td>
      <td>11</td>
      <td>O</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-22.738</td>
      <td>7.137</td>
      <td>-20.688</td>
      <td>1.00</td>
      <td>41.35</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>11</th>
      <td>ATOM</td>
      <td>12</td>
      <td>CB</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-22.743</td>
      <td>4.008</td>
      <td>-21.257</td>
      <td>1.00</td>
      <td>41.94</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>12</th>
      <td>ATOM</td>
      <td>13</td>
      <td>CG</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-21.985</td>
      <td>2.915</td>
      <td>-20.487</td>
      <td>1.00</td>
      <td>42.50</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>13</th>
      <td>ATOM</td>
      <td>14</td>
      <td>CD1</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-21.338</td>
      <td>1.957</td>
      <td>-21.475</td>
      <td>1.00</td>
      <td>44.31</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>14</th>
      <td>ATOM</td>
      <td>15</td>
      <td>CD2</td>
      <td>LEU</td>
      <td>A</td>
      <td>1</td>
      <td>-20.939</td>
      <td>3.448</td>
      <td>-19.508</td>
      <td>1.00</td>
      <td>39.42</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>15</th>
      <td>ATOM</td>
      <td>16</td>
      <td>N</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-24.561</td>
      <td>6.684</td>
      <td>-21.950</td>
      <td>1.00</td>
      <td>45.78</td>
      <td>N</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>16</th>
      <td>ATOM</td>
      <td>17</td>
      <td>CA</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-24.686</td>
      <td>8.048</td>
      <td>-22.484</td>
      <td>1.00</td>
      <td>47.90</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>17</th>
      <td>ATOM</td>
      <td>18</td>
      <td>C</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-24.917</td>
      <td>9.038</td>
      <td>-21.356</td>
      <td>1.00</td>
      <td>43.00</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>18</th>
      <td>ATOM</td>
      <td>19</td>
      <td>O</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-24.419</td>
      <td>10.162</td>
      <td>-21.404</td>
      <td>1.00</td>
      <td>42.03</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>19</th>
      <td>ATOM</td>
      <td>20</td>
      <td>CB</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-25.804</td>
      <td>8.178</td>
      <td>-23.531</td>
      <td>1.00</td>
      <td>53.41</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>20</th>
      <td>ATOM</td>
      <td>21</td>
      <td>CG</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-25.853</td>
      <td>9.566</td>
      <td>-24.175</td>
      <td>1.00</td>
      <td>60.62</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>21</th>
      <td>ATOM</td>
      <td>22</td>
      <td>CD</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-26.624</td>
      <td>9.630</td>
      <td>-25.488</td>
      <td>1.00</td>
      <td>72.10</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>22</th>
      <td>ATOM</td>
      <td>23</td>
      <td>OE1</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-27.176</td>
      <td>8.594</td>
      <td>-25.927</td>
      <td>1.00</td>
      <td>73.33</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>23</th>
      <td>ATOM</td>
      <td>24</td>
      <td>OE2</td>
      <td>GLU</td>
      <td>A</td>
      <td>2</td>
      <td>-26.676</td>
      <td>10.734</td>
      <td>-26.086</td>
      <td>1.00</td>
      <td>76.05</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>24</th>
      <td>ATOM</td>
      <td>25</td>
      <td>N</td>
      <td>GLU</td>
      <td>A</td>
      <td>3</td>
      <td>-25.666</td>
      <td>8.603</td>
      <td>-20.347</td>
      <td>1.00</td>
      <td>41.47</td>
      <td>N</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>25</th>
      <td>ATOM</td>
      <td>26</td>
      <td>CA</td>
      <td>GLU</td>
      <td>A</td>
      <td>3</td>
      <td>-25.920</td>
      <td>9.409</td>
      <td>-19.167</td>
      <td>1.00</td>
      <td>43.73</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>26</th>
      <td>ATOM</td>
      <td>27</td>
      <td>C</td>
      <td>GLU</td>
      <td>A</td>
      <td>3</td>
      <td>-24.644</td>
      <td>9.647</td>
      <td>-18.363</td>
      <td>1.00</td>
      <td>40.11</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>27</th>
      <td>ATOM</td>
      <td>28</td>
      <td>O</td>
      <td>GLU</td>
      <td>A</td>
      <td>3</td>
      <td>-24.351</td>
      <td>10.791</td>
      <td>-18.014</td>
      <td>1.00</td>
      <td>39.46</td>
      <td>O</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>28</th>
      <td>ATOM</td>
      <td>29</td>
      <td>CB</td>
      <td>GLU</td>
      <td>A</td>
      <td>3</td>
      <td>-26.999</td>
      <td>8.769</td>
      <td>-18.294</td>
      <td>1.00</td>
      <td>51.67</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>29</th>
      <td>ATOM</td>
      <td>30</td>
      <td>CG</td>
      <td>GLU</td>
      <td>A</td>
      <td>3</td>
      <td>-28.420</td>
      <td>9.010</td>
      <td>-18.782</td>
      <td>1.00</td>
      <td>59.54</td>
      <td>C</td>
      <td>4lza</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>17862</th>
      <td>ATOM</td>
      <td>17866</td>
      <td>C</td>
      <td>SER</td>
      <td>D</td>
      <td>579</td>
      <td>117.038</td>
      <td>37.003</td>
      <td>23.117</td>
      <td>1.00</td>
      <td>43.44</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17863</th>
      <td>ATOM</td>
      <td>17867</td>
      <td>O</td>
      <td>SER</td>
      <td>D</td>
      <td>579</td>
      <td>116.636</td>
      <td>37.790</td>
      <td>22.260</td>
      <td>1.00</td>
      <td>42.16</td>
      <td>O</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17864</th>
      <td>ATOM</td>
      <td>17868</td>
      <td>CB</td>
      <td>SER</td>
      <td>D</td>
      <td>579</td>
      <td>116.247</td>
      <td>36.940</td>
      <td>25.494</td>
      <td>1.00</td>
      <td>51.78</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17865</th>
      <td>ATOM</td>
      <td>17869</td>
      <td>OG</td>
      <td>SER</td>
      <td>D</td>
      <td>579</td>
      <td>116.200</td>
      <td>35.525</td>
      <td>25.465</td>
      <td>1.00</td>
      <td>52.65</td>
      <td>O</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17866</th>
      <td>ATOM</td>
      <td>17870</td>
      <td>N</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>117.259</td>
      <td>35.718</td>
      <td>22.871</td>
      <td>1.00</td>
      <td>40.53</td>
      <td>N</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17867</th>
      <td>ATOM</td>
      <td>17871</td>
      <td>CA</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>116.947</td>
      <td>35.138</td>
      <td>21.573</td>
      <td>1.00</td>
      <td>38.81</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17868</th>
      <td>ATOM</td>
      <td>17872</td>
      <td>C</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>115.529</td>
      <td>34.573</td>
      <td>21.571</td>
      <td>1.00</td>
      <td>43.20</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17869</th>
      <td>ATOM</td>
      <td>17873</td>
      <td>O</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>115.046</td>
      <td>34.084</td>
      <td>20.549</td>
      <td>1.00</td>
      <td>42.35</td>
      <td>O</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17870</th>
      <td>ATOM</td>
      <td>17874</td>
      <td>CB</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>117.966</td>
      <td>34.058</td>
      <td>21.207</td>
      <td>1.00</td>
      <td>35.80</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17871</th>
      <td>ATOM</td>
      <td>17875</td>
      <td>CG</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>119.316</td>
      <td>34.604</td>
      <td>20.828</td>
      <td>1.00</td>
      <td>36.39</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17872</th>
      <td>ATOM</td>
      <td>17876</td>
      <td>CD1</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>119.425</td>
      <td>35.824</td>
      <td>20.182</td>
      <td>1.00</td>
      <td>33.90</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17873</th>
      <td>ATOM</td>
      <td>17877</td>
      <td>CD2</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>120.474</td>
      <td>33.903</td>
      <td>21.122</td>
      <td>1.00</td>
      <td>36.79</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17874</th>
      <td>ATOM</td>
      <td>17878</td>
      <td>CE1</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>120.664</td>
      <td>36.334</td>
      <td>19.831</td>
      <td>1.00</td>
      <td>31.61</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17875</th>
      <td>ATOM</td>
      <td>17879</td>
      <td>CE2</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>121.716</td>
      <td>34.409</td>
      <td>20.775</td>
      <td>1.00</td>
      <td>33.85</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17876</th>
      <td>ATOM</td>
      <td>17880</td>
      <td>CZ</td>
      <td>PHE</td>
      <td>D</td>
      <td>580</td>
      <td>121.810</td>
      <td>35.625</td>
      <td>20.129</td>
      <td>1.00</td>
      <td>31.90</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17877</th>
      <td>ATOM</td>
      <td>17881</td>
      <td>N</td>
      <td>ASN</td>
      <td>D</td>
      <td>581</td>
      <td>114.863</td>
      <td>34.651</td>
      <td>22.720</td>
      <td>1.00</td>
      <td>46.01</td>
      <td>N</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17878</th>
      <td>ATOM</td>
      <td>17882</td>
      <td>CA</td>
      <td>ASN</td>
      <td>D</td>
      <td>581</td>
      <td>113.467</td>
      <td>34.239</td>
      <td>22.817</td>
      <td>1.00</td>
      <td>48.70</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17879</th>
      <td>ATOM</td>
      <td>17883</td>
      <td>C</td>
      <td>ASN</td>
      <td>D</td>
      <td>581</td>
      <td>112.585</td>
      <td>35.332</td>
      <td>23.416</td>
      <td>1.00</td>
      <td>46.12</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17880</th>
      <td>ATOM</td>
      <td>17884</td>
      <td>O</td>
      <td>ASN</td>
      <td>D</td>
      <td>581</td>
      <td>113.068</td>
      <td>36.218</td>
      <td>24.120</td>
      <td>1.00</td>
      <td>43.82</td>
      <td>O</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17881</th>
      <td>ATOM</td>
      <td>17885</td>
      <td>CB</td>
      <td>ASN</td>
      <td>D</td>
      <td>581</td>
      <td>113.335</td>
      <td>32.948</td>
      <td>23.633</td>
      <td>1.00</td>
      <td>55.75</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17882</th>
      <td>ATOM</td>
      <td>17886</td>
      <td>CG</td>
      <td>ASN</td>
      <td>D</td>
      <td>581</td>
      <td>113.953</td>
      <td>33.056</td>
      <td>25.015</td>
      <td>1.00</td>
      <td>63.15</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17883</th>
      <td>ATOM</td>
      <td>17887</td>
      <td>OD1</td>
      <td>ASN</td>
      <td>D</td>
      <td>581</td>
      <td>114.397</td>
      <td>34.124</td>
      <td>25.432</td>
      <td>1.00</td>
      <td>69.07</td>
      <td>O</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17884</th>
      <td>ATOM</td>
      <td>17888</td>
      <td>ND2</td>
      <td>ASN</td>
      <td>D</td>
      <td>581</td>
      <td>113.977</td>
      <td>31.942</td>
      <td>25.736</td>
      <td>1.00</td>
      <td>65.78</td>
      <td>N</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17885</th>
      <td>ATOM</td>
      <td>17889</td>
      <td>N</td>
      <td>VAL</td>
      <td>D</td>
      <td>582</td>
      <td>111.289</td>
      <td>35.262</td>
      <td>23.126</td>
      <td>1.00</td>
      <td>46.70</td>
      <td>N</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17886</th>
      <td>ATOM</td>
      <td>17890</td>
      <td>CA</td>
      <td>VAL</td>
      <td>D</td>
      <td>582</td>
      <td>110.341</td>
      <td>36.268</td>
      <td>23.591</td>
      <td>1.00</td>
      <td>43.77</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17887</th>
      <td>ATOM</td>
      <td>17891</td>
      <td>C</td>
      <td>VAL</td>
      <td>D</td>
      <td>582</td>
      <td>109.996</td>
      <td>36.082</td>
      <td>25.066</td>
      <td>1.00</td>
      <td>44.77</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17888</th>
      <td>ATOM</td>
      <td>17892</td>
      <td>O</td>
      <td>VAL</td>
      <td>D</td>
      <td>582</td>
      <td>110.051</td>
      <td>34.970</td>
      <td>25.592</td>
      <td>1.00</td>
      <td>45.92</td>
      <td>O</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17889</th>
      <td>ATOM</td>
      <td>17893</td>
      <td>CB</td>
      <td>VAL</td>
      <td>D</td>
      <td>582</td>
      <td>109.039</td>
      <td>36.239</td>
      <td>22.764</td>
      <td>1.00</td>
      <td>45.04</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17890</th>
      <td>ATOM</td>
      <td>17894</td>
      <td>CG1</td>
      <td>VAL</td>
      <td>D</td>
      <td>582</td>
      <td>109.314</td>
      <td>36.646</td>
      <td>21.323</td>
      <td>1.00</td>
      <td>40.74</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
    <tr>
      <th>17891</th>
      <td>ATOM</td>
      <td>17895</td>
      <td>CG2</td>
      <td>VAL</td>
      <td>D</td>
      <td>582</td>
      <td>108.404</td>
      <td>34.858</td>
      <td>22.819</td>
      <td>1.00</td>
      <td>47.16</td>
      <td>C</td>
      <td>4Z0L</td>
    </tr>
  </tbody>
</table>
<p>20524 rows × 13 columns</p>
</div>



## Next we want to put all ids into one dataframe

### We used get_all() to list all pdb entries. 


```python
len(get_all())
```




    169681



### We found there was 169681 entries in the current PDB  DataBase.

### We used concat() function to merge all the dataframe of each pdb entry into one huge dataframe.


```python
frames = [get_atom(id) for id in get_all()[:2]]
pd.concat(frames)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ATOM</td>
      <td>1</td>
      <td>O5'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-4.549</td>
      <td>5.095</td>
      <td>4.262</td>
      <td>1.00</td>
      <td>28.71</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ATOM</td>
      <td>2</td>
      <td>C5'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-4.176</td>
      <td>6.323</td>
      <td>3.646</td>
      <td>1.00</td>
      <td>27.35</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ATOM</td>
      <td>3</td>
      <td>C4'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-3.853</td>
      <td>7.410</td>
      <td>4.672</td>
      <td>1.00</td>
      <td>24.41</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ATOM</td>
      <td>4</td>
      <td>O4'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-4.992</td>
      <td>7.650</td>
      <td>5.512</td>
      <td>1.00</td>
      <td>22.53</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ATOM</td>
      <td>5</td>
      <td>C3'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-2.713</td>
      <td>7.010</td>
      <td>5.605</td>
      <td>1.00</td>
      <td>23.56</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ATOM</td>
      <td>6</td>
      <td>O3'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-1.379</td>
      <td>7.127</td>
      <td>5.060</td>
      <td>1.00</td>
      <td>21.02</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ATOM</td>
      <td>7</td>
      <td>C2'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-2.950</td>
      <td>7.949</td>
      <td>6.756</td>
      <td>1.00</td>
      <td>23.73</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ATOM</td>
      <td>8</td>
      <td>O2'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-2.407</td>
      <td>9.267</td>
      <td>6.554</td>
      <td>1.00</td>
      <td>23.93</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ATOM</td>
      <td>9</td>
      <td>C1'</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-4.489</td>
      <td>7.917</td>
      <td>6.825</td>
      <td>1.00</td>
      <td>20.60</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ATOM</td>
      <td>10</td>
      <td>N1</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-4.931</td>
      <td>6.902</td>
      <td>7.826</td>
      <td>1.00</td>
      <td>19.25</td>
      <td>N</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ATOM</td>
      <td>11</td>
      <td>C2</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-4.838</td>
      <td>7.263</td>
      <td>9.158</td>
      <td>1.00</td>
      <td>16.72</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>11</th>
      <td>ATOM</td>
      <td>12</td>
      <td>O2</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-4.287</td>
      <td>8.308</td>
      <td>9.505</td>
      <td>1.00</td>
      <td>15.49</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>12</th>
      <td>ATOM</td>
      <td>13</td>
      <td>N3</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-5.367</td>
      <td>6.448</td>
      <td>10.085</td>
      <td>1.00</td>
      <td>15.96</td>
      <td>N</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>13</th>
      <td>ATOM</td>
      <td>14</td>
      <td>C4</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-5.978</td>
      <td>5.310</td>
      <td>9.736</td>
      <td>1.00</td>
      <td>16.84</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>14</th>
      <td>ATOM</td>
      <td>15</td>
      <td>N4</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-6.592</td>
      <td>4.588</td>
      <td>10.676</td>
      <td>1.00</td>
      <td>19.14</td>
      <td>N</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>15</th>
      <td>ATOM</td>
      <td>16</td>
      <td>C5</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-6.059</td>
      <td>4.907</td>
      <td>8.376</td>
      <td>1.00</td>
      <td>17.68</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>16</th>
      <td>ATOM</td>
      <td>17</td>
      <td>C6</td>
      <td>C</td>
      <td>A</td>
      <td>1</td>
      <td>-5.522</td>
      <td>5.732</td>
      <td>7.461</td>
      <td>1.00</td>
      <td>17.68</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>17</th>
      <td>ATOM</td>
      <td>18</td>
      <td>P</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>-0.178</td>
      <td>6.220</td>
      <td>5.647</td>
      <td>1.00</td>
      <td>24.85</td>
      <td>P</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>18</th>
      <td>ATOM</td>
      <td>19</td>
      <td>OP1</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>0.915</td>
      <td>6.451</td>
      <td>4.671</td>
      <td>1.00</td>
      <td>25.96</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>19</th>
      <td>ATOM</td>
      <td>20</td>
      <td>OP2</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>-0.948</td>
      <td>4.954</td>
      <td>5.664</td>
      <td>1.00</td>
      <td>24.57</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>20</th>
      <td>ATOM</td>
      <td>21</td>
      <td>O5'</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>0.435</td>
      <td>6.502</td>
      <td>7.097</td>
      <td>1.00</td>
      <td>24.10</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>21</th>
      <td>ATOM</td>
      <td>22</td>
      <td>C5'</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>1.020</td>
      <td>7.793</td>
      <td>7.281</td>
      <td>1.00</td>
      <td>19.66</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>22</th>
      <td>ATOM</td>
      <td>23</td>
      <td>C4'</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>1.034</td>
      <td>8.184</td>
      <td>8.738</td>
      <td>1.00</td>
      <td>17.99</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>23</th>
      <td>ATOM</td>
      <td>24</td>
      <td>O4'</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>-0.290</td>
      <td>8.244</td>
      <td>9.222</td>
      <td>1.00</td>
      <td>17.23</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>24</th>
      <td>ATOM</td>
      <td>25</td>
      <td>C3'</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>1.724</td>
      <td>7.167</td>
      <td>9.617</td>
      <td>1.00</td>
      <td>18.98</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>25</th>
      <td>ATOM</td>
      <td>26</td>
      <td>O3'</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>3.130</td>
      <td>7.395</td>
      <td>9.564</td>
      <td>1.00</td>
      <td>18.39</td>
      <td>O</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>26</th>
      <td>ATOM</td>
      <td>27</td>
      <td>C2'</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>1.152</td>
      <td>7.607</td>
      <td>10.934</td>
      <td>1.00</td>
      <td>17.33</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>27</th>
      <td>ATOM</td>
      <td>28</td>
      <td>C1'</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>-0.273</td>
      <td>7.853</td>
      <td>10.599</td>
      <td>1.00</td>
      <td>15.44</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>28</th>
      <td>ATOM</td>
      <td>29</td>
      <td>N1</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>-1.070</td>
      <td>6.635</td>
      <td>10.823</td>
      <td>1.00</td>
      <td>14.48</td>
      <td>N</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>29</th>
      <td>ATOM</td>
      <td>30</td>
      <td>C2</td>
      <td>DC</td>
      <td>A</td>
      <td>2</td>
      <td>-1.417</td>
      <td>6.355</td>
      <td>12.130</td>
      <td>1.00</td>
      <td>13.03</td>
      <td>C</td>
      <td>100D</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>418</th>
      <td>ATOM</td>
      <td>460</td>
      <td>N1</td>
      <td>DC</td>
      <td>B</td>
      <td>23</td>
      <td>14.637</td>
      <td>21.541</td>
      <td>22.637</td>
      <td>1.00</td>
      <td>5.21</td>
      <td>N</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>419</th>
      <td>ATOM</td>
      <td>461</td>
      <td>C2</td>
      <td>DC</td>
      <td>B</td>
      <td>23</td>
      <td>15.618</td>
      <td>22.342</td>
      <td>22.078</td>
      <td>1.00</td>
      <td>6.76</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>420</th>
      <td>ATOM</td>
      <td>462</td>
      <td>O2</td>
      <td>DC</td>
      <td>B</td>
      <td>23</td>
      <td>16.700</td>
      <td>21.866</td>
      <td>21.792</td>
      <td>1.00</td>
      <td>6.72</td>
      <td>O</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>421</th>
      <td>ATOM</td>
      <td>463</td>
      <td>N3</td>
      <td>DC</td>
      <td>B</td>
      <td>23</td>
      <td>15.317</td>
      <td>23.677</td>
      <td>21.932</td>
      <td>1.00</td>
      <td>10.02</td>
      <td>N</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>422</th>
      <td>ATOM</td>
      <td>464</td>
      <td>C4</td>
      <td>DC</td>
      <td>B</td>
      <td>23</td>
      <td>14.115</td>
      <td>24.232</td>
      <td>22.250</td>
      <td>1.00</td>
      <td>7.10</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>423</th>
      <td>ATOM</td>
      <td>465</td>
      <td>N4</td>
      <td>DC</td>
      <td>B</td>
      <td>23</td>
      <td>13.904</td>
      <td>25.543</td>
      <td>22.033</td>
      <td>1.00</td>
      <td>0.00</td>
      <td>N</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>424</th>
      <td>ATOM</td>
      <td>466</td>
      <td>C5</td>
      <td>DC</td>
      <td>B</td>
      <td>23</td>
      <td>13.108</td>
      <td>23.372</td>
      <td>22.777</td>
      <td>1.00</td>
      <td>7.82</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>425</th>
      <td>ATOM</td>
      <td>467</td>
      <td>C6</td>
      <td>DC</td>
      <td>B</td>
      <td>23</td>
      <td>13.414</td>
      <td>22.064</td>
      <td>22.930</td>
      <td>1.00</td>
      <td>4.87</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>426</th>
      <td>ATOM</td>
      <td>468</td>
      <td>P</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>15.967</td>
      <td>16.347</td>
      <td>24.405</td>
      <td>1.00</td>
      <td>28.28</td>
      <td>P</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>427</th>
      <td>ATOM</td>
      <td>469</td>
      <td>OP1</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>16.200</td>
      <td>14.964</td>
      <td>23.832</td>
      <td>1.00</td>
      <td>27.79</td>
      <td>O</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>428</th>
      <td>ATOM</td>
      <td>470</td>
      <td>OP2</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>15.043</td>
      <td>16.312</td>
      <td>25.587</td>
      <td>1.00</td>
      <td>22.79</td>
      <td>O</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>429</th>
      <td>ATOM</td>
      <td>471</td>
      <td>O5'</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>17.290</td>
      <td>17.159</td>
      <td>24.722</td>
      <td>1.00</td>
      <td>28.58</td>
      <td>O</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>430</th>
      <td>ATOM</td>
      <td>472</td>
      <td>C5'</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>18.246</td>
      <td>17.920</td>
      <td>23.998</td>
      <td>1.00</td>
      <td>16.71</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>431</th>
      <td>ATOM</td>
      <td>473</td>
      <td>C4'</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>18.914</td>
      <td>18.907</td>
      <td>24.951</td>
      <td>1.00</td>
      <td>12.60</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>432</th>
      <td>ATOM</td>
      <td>474</td>
      <td>O4'</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>18.372</td>
      <td>20.147</td>
      <td>24.710</td>
      <td>1.00</td>
      <td>5.80</td>
      <td>O</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>433</th>
      <td>ATOM</td>
      <td>475</td>
      <td>C3'</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>18.654</td>
      <td>18.701</td>
      <td>26.432</td>
      <td>1.00</td>
      <td>14.53</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>434</th>
      <td>ATOM</td>
      <td>476</td>
      <td>O3'</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>19.678</td>
      <td>17.873</td>
      <td>27.024</td>
      <td>1.00</td>
      <td>22.51</td>
      <td>O</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>435</th>
      <td>ATOM</td>
      <td>477</td>
      <td>C2'</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>18.593</td>
      <td>20.091</td>
      <td>27.036</td>
      <td>1.00</td>
      <td>12.59</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>436</th>
      <td>ATOM</td>
      <td>478</td>
      <td>C1'</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>18.681</td>
      <td>20.995</td>
      <td>25.860</td>
      <td>1.00</td>
      <td>8.49</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>437</th>
      <td>ATOM</td>
      <td>479</td>
      <td>N9</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>17.627</td>
      <td>22.013</td>
      <td>25.822</td>
      <td>1.00</td>
      <td>10.33</td>
      <td>N</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>438</th>
      <td>ATOM</td>
      <td>480</td>
      <td>C8</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>16.312</td>
      <td>21.854</td>
      <td>26.191</td>
      <td>1.00</td>
      <td>7.57</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>439</th>
      <td>ATOM</td>
      <td>481</td>
      <td>N7</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>15.579</td>
      <td>22.904</td>
      <td>26.013</td>
      <td>1.00</td>
      <td>8.17</td>
      <td>N</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>440</th>
      <td>ATOM</td>
      <td>482</td>
      <td>C5</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>16.467</td>
      <td>23.824</td>
      <td>25.441</td>
      <td>1.00</td>
      <td>5.92</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>441</th>
      <td>ATOM</td>
      <td>483</td>
      <td>C6</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>16.256</td>
      <td>25.159</td>
      <td>25.040</td>
      <td>1.00</td>
      <td>9.51</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>442</th>
      <td>ATOM</td>
      <td>484</td>
      <td>O6</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>15.193</td>
      <td>25.805</td>
      <td>25.110</td>
      <td>1.00</td>
      <td>11.38</td>
      <td>O</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>443</th>
      <td>ATOM</td>
      <td>485</td>
      <td>N1</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>17.380</td>
      <td>25.781</td>
      <td>24.551</td>
      <td>1.00</td>
      <td>9.55</td>
      <td>N</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>444</th>
      <td>ATOM</td>
      <td>486</td>
      <td>C2</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>18.598</td>
      <td>25.147</td>
      <td>24.436</td>
      <td>1.00</td>
      <td>9.22</td>
      <td>C</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>445</th>
      <td>ATOM</td>
      <td>487</td>
      <td>N2</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>19.520</td>
      <td>25.991</td>
      <td>23.890</td>
      <td>1.00</td>
      <td>0.67</td>
      <td>N</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>446</th>
      <td>ATOM</td>
      <td>488</td>
      <td>N3</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>18.851</td>
      <td>23.879</td>
      <td>24.780</td>
      <td>1.00</td>
      <td>1.61</td>
      <td>N</td>
      <td>101D</td>
    </tr>
    <tr>
      <th>447</th>
      <td>ATOM</td>
      <td>489</td>
      <td>C4</td>
      <td>DG</td>
      <td>B</td>
      <td>24</td>
      <td>17.734</td>
      <td>23.301</td>
      <td>25.301</td>
      <td>1.00</td>
      <td>7.73</td>
      <td>C</td>
      <td>101D</td>
    </tr>
  </tbody>
</table>
<p>856 rows × 13 columns</p>
</div>



<a id='32'></a>
## We used mdtraj package to load pdb file into memory from URL

>MDTraj is a python library that allows users to manipulate molecular dynamics (MD) trajectories. Features include:
1. Wide MD format support, including pdb, xtc, trr, dcd, binpos, netcdf, mdcrd, prmtop, and more.
2. Extremely fast RMSD calculations (4x the speed of the original Theobald QCP).
3. Extensive analysis functions including those that compute bonds, angles, dihedrals, hydrogen bonds, secondary structure, and NMR observables.
4. Lightweight, Pythonic API.


```python
import mdtraj as md # import this package
```


```python
pdb = md.load_pdb("https://files.rcsb.org/view/4LZA.pdb")  # load data
```


```python
print(pdb) # print to see how many frames and atoms, residues this file has 
```

    <mdtraj.Trajectory with 1 frames, 2833 atoms, 512 residues, and unitcells>


## We convert this pdb file into topology


```python
topology = pdb.topology
```


```python
table, bonds = topology.to_dataframe()
```


```python
print(table.head(7))
```

       serial name element  resSeq resName  chainID segmentID
    0       1    N       N       0     THR        0          
    1       2   CA       C       0     THR        0          
    2       3    C       C       0     THR        0          
    3       4    O       O       0     THR        0          
    4       5   CB       C       0     THR        0          
    5       6  OG1       O       0     THR        0          
    6       7  CG2       C       0     THR        0          



```python
topology.atom(10)
```




    LEU1-O




```python
topology.atoms
```




    <generator object Topology.atoms at 0x7fe9cd22c390>




```python
[i for i in topology.atoms][:10]
```




    [THR0-N,
     THR0-CA,
     THR0-C,
     THR0-O,
     THR0-CB,
     THR0-OG1,
     THR0-CG2,
     LEU1-N,
     LEU1-CA,
     LEU1-C]




```python
print(table.head(10))
```

       serial name element  resSeq resName  chainID segmentID
    0       1    N       N       0     THR        0          
    1       2   CA       C       0     THR        0          
    2       3    C       C       0     THR        0          
    3       4    O       O       0     THR        0          
    4       5   CB       C       0     THR        0          
    5       6  OG1       O       0     THR        0          
    6       7  CG2       C       0     THR        0          
    7       8    N       N       1     LEU        0          
    8       9   CA       C       1     LEU        0          
    9      10    C       C       1     LEU        0          



```python
atom = pdb.atom_slice(range(2833))
```


```python
print(atom)
```

    <mdtraj.Trajectory with 1 frames, 2833 atoms, 512 residues, and unitcells>



```python
atom.xyz
```




    array([[[-2.7785,  0.5217, -2.1426],
            [-2.7459,  0.5049, -1.9974],
            [-2.5949,  0.513 , -1.9667],
            ...,
            [-0.6332, -1.3026, -0.3481],
            [-0.8265, -1.4563, -0.0902],
            [-2.8824,  1.244 , -0.1084]]], dtype=float32)




```python
[i for i in topology.bonds][:10]
```




    [Bond(THR0-CA, THR0-C),
     Bond(THR0-C, THR0-O),
     Bond(THR0-CA, THR0-CB),
     Bond(THR0-N, THR0-CA),
     Bond(THR0-CB, THR0-CG2),
     Bond(THR0-CB, THR0-OG1),
     Bond(THR0-C, LEU1-N),
     Bond(LEU1-CA, LEU1-C),
     Bond(LEU1-C, LEU1-O),
     Bond(LEU1-CA, LEU1-CB)]


