# LoTSS-DR1

- Whats the notebook about 

PyBDSF associations (HETDEX field)

<a href="PyBDSF_DR1_associations.ipynb">PyBDSF_DR1_associations</a>

***

## Outputs

The notebook creates an output table (`output_table.fits`) with Four main categories:

1.  Deblends: PyBDSF sources that were deblended into 2 or more optical sources
1.  Multi-components: optical sources composed by Multiple PyBDSF components
1.  Singles: optical sources composed by a single PyBDSF
1.  Artifacts: PyBDSF sources that are artifacts

- A combination of flags explain

## Flags 

| category                | origin                      | flag  | n PyBDSF  | n optical |
|:------------------------|:----------------------------|:------|:----------|-----------|
| singles                 | unique PyBDSF - Optical     |   1   | 313161    | 313161    |
| deblend problems        | not deblended               |   2   | 0         | 0         |
| singles + not deblended | combination of flags 1 + 2  |   3   | 10        | 10        |
| deblends                | components catalogue        |   4   | 832       | 1575      |
| multi-components        | components catalogue        |   8   | 9007      | 3565      |
| delblends + multi-comp. | combination of 4 + 8        |   12  | 193       | 209       |
| artifacts               | artifact catalogue          |   16  | 2543      | 2543      |
| artifacts               | PyBDSF missing in optical   |   32  | 48        | 48        |

***

## Catalogues 
### Catalogues used (available soon)

* PyBDSF raw catalogue 
* PyBDSF components catalogue
* Optical associations catalogue (Pan-STARRS and All WISE)
* Artifacts catalogue

### Cleaning the Catalogues

* A source was picked on 2 different mosaics (same `Source_Name`) and was classified as an artifact in one mosaic and as a source in other. This source was renamed with the original name followed by 'B'. This was done on both **Artifacts catalogue** and **PyBDSF raw catalogue** (the source appears twice on the PyBDSF raw catalogue).
* Duplicated entries were removed from the PyBDSF components catalogue (9 duplicated `Source_Name` and `Component_Name` for the same source).
* A source on the PyBDSF components catalogue was removed because it is an artifact (`Component_Name` is on the artifact catalogue).

For more details see section `Catalogues` of the notebook.

***

## Deblended sources

Deblended sources are distint sources that were originally associated by PyBDSF as only one source, i.e. the PyBDSF components from different sources were associated into the same `Source_Name` in the **Compoments Catalogue**.

These sources were sent to a deblend workflow (`ID_flag = 41`) or selected for deblending on LGZ (`ID_flag = 42`). See Williams et al. 2018 (available soon). However some of them were not actually deblended and some were deblended after association into a bigger source. For that reason the association between the raw PyBDSF sources and the final optical sources was made through the components catalogue, using the columns `Deblended_from` (which links directly to the PyBDSF original source names) and the `Source_Name` (which links directly to the optical source names). 

The total number of Sources that went through a deblending process is:

* Number of PyBDSF components that were deblended: 925
* Number of correspondent optical sources: 1784
* Number of entries on the table: 1822	

This corresponds to flag = 4 and flag = 12 on the table. 

However, some of these were not just deblended but also the PyBDSF components associated after deblending (see `Multi-component PyBDSF` below for more details).

The sources that were just delended correspond to 832 PyBDSF components and 1575 optical sources (flag 4, see section `Deblended sources` of the notebook). check this (832 PyBDSF components deblended at least into 2 sources makes 1664)


## Multi-components PyBDSF sources

** flag = 8 **

Multi-components PyBDSF sources correspond to optical sources that are composed by more than one PyBDSF component (`Component_Name` on the component catalogue). These were selected from the components catalogue. 
A total of 3774 optical sources are composed by more than one PyBDSF component and 9868 PyBDSF components make up these 3774 sources. Note that some optical sources can have up to 35 PyBDSF components and also that included in these numbers are the sources that went also through the deblending process (flag = 8 and flag = 12). 

The number of sources that are uniquely 'multi-components' and have not been throught deblending are: 3565 optical sources that correspond to 9007 PyBDSF components. 

- Check this: A total of 9255 PyBDSF sources are classified as 'multi-components' in the output table.
(but not have been deblended) - I think this number is just a prediction



## Single sources 

A total of 313171 PyBDSF sources are classified as `singles` in the output table. Single sources are PyBDSF sources that have not been deblended, grouped with other PyBDSFs sources and are not artifacts. The sources were selected using the components catalogue, looking for unique correspondences between the PyBDFS raw catalogue and the final optical catalogue (313161 objects, flag 1, see section `Single sources` of the notebook); and from sources that were selected for deblending in LGZ but were not actually deblended (10 objects, flag 3, see section `Deblended sources/Sources that do not seem to be deblended` of the notebook).


## Artifacts

There are a total of 2591 PyBDSF sources classified as artifacts in the output table. These were selected from the artifacts catalogue (2543 PyBDSFs, flag 16); and from the PyBDSF raw catalogue, corresponding to sources that are missing in the final optical catalogue (48 PyBDSFs, flag 32).

***



