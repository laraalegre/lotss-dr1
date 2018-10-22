
# Intro 

LoTSS-DR1 is the first public data release of the **LOFAR Two-metre Sky Survey** (LoTSS, Shimwell et al. 2017). LoTSS-DR1 (described in Shimwell et al. 2018) surveys the **HETDEX** field.

The source detection in LoTSS-DR1 is performed using the Python Blob Detector and Source Finder Software (**PyBDSF**, Mohan et al. 2015) which fits Gaussians to pixel islands. This generates components rather than true sources. For that reason, the identification of LOFAR radio sources as well as the cross-matching with optical counterparts (Pan-STARRS and WISE) was achieved using a combination of statistical likelihood ratio techniques and visual inspection via a private LOFAR Galaxy Zoo (LGZ) classification project (described in Williams et al. 2018).

The LoTSS-DR1 connection between each raw PyBDSF source and the final optical associations (or lack of association), is explained in a Jupyter notebook (available for download). The input and output catalogues are explained next. 
***

# Catalogues

Here we use the **version 1.2 of the optical and components catalogues, version 0.9 of the raw PyBDSF sources, version 0.99 of the Gaussians catalogue, and version 1.1 of the artifacts catalogue**. All catalogues will be available on LoTSS-DR1 webpage. 

## Input catalogues

* PyBDSF raw catalogue (*LOFAR_HBA_T1_DR1_catalog_v0.9.srl.fixed.fits*)
* PyBDSF components catalogue (*LOFAR_HBA_T1_DR1_merge_ID_v1.2.comp.fits*)
* Optical associations catalogue: Pan-STARRS and WISE (*LOFAR_HBA_T1_DR1_merge_ID_optical_f_v1.2.fits*)
* Artifacts catalogue (*LOFAR_HBA_T1_DR1_merge_ID_v1.1.art.fits*)
* Gaussian catalogue (*LOFAR_HBA_T1_DR1_catalog_v0.99.gaus.fits*)

#### Cleaning the Catalogues

* A source appears in 2 different mosaics and was classified as an artifact in one mosaic and as a source in the other. This source was renamed replacing the last character of the original 'Source_Name' by 'B'. This was done on both **Artifacts catalogue** and **PyBDSF raw catalogue** (the source appears twice on the PyBDSF raw catalogue).
* Duplicated entries were removed from the PyBDSF **components catalogue** (9 duplicated 'Source_Name' and 'Component_Name' refering to the same source).
* A source on the PyBDSF **components catalogue** was removed because it is an artifact ('Component_Name' is on the artifact catalogue).

For more details see notebook **_PyBDSF_DR1_clean_catalogues.ipynb_**.


## PyBDSF-DR1 Associations Catalogue

The notebook **_PyBDSF_DR1_associations.ipynb_**. creates an output table with 3 columns: 

* **pybdsf_name**: original PyBDSF source names (as in the PyBDSF raw catalogue).
* **association_name**: optical name (as in the optical associations catalogue) or lackof association (null). 
* **flag**: category of the sources. 


### Output Flags

| Category                 | Selection                               | Flag  | nr PyBDSF*    | nr optical*   | nr entries |
|:-------------------------|:----------------------------------------|:------|:--------------|---------------|------------|
| Single sources           | Unique PyBDSF-optical correspondence    |   1   | 313161        | 313161        |313161      | 
| Deblending problems      | Not deblended                           |   2   | 0             | 0             |0           |
| Single + not deblended   | combination of flags 1 and 2            |   3   | 13            | 13            |13          |
| Deblended sources        | Multiple PyBDSF-optical correspondences |   4   | 880           | 1750          |1750        |
| Multi-component PyBDSF   | Merged PyBDSF-optical correspondences   |   8   | 9007          | 3565          |9007        |
| Multi + not deblended    | combination of flags 8 and 2            |   10  | 39            | 31            |39          |
| Multi + deblended        | Combination of flags 8 and 4            |   12  | 26            | 30            |30          |
| Artifacts                | Artifact catalogue                      |   16  | 2543          | 0             |2543        |
| Artifacts                | PyBDSF missing in the optical catalogue |   32  | 48            | 0             |48          |
| **TOTAL**                |                   -                     |   -   | 325694        | 318521        |326591      |

(*) Refers to unique values

***

# Sources

The PyBDSF-optical associations comprise 4 main source categories:

* **Multi-component PyBDSF sources**: optical sources composed by Multiple PyBDSF sources
* **Deblended sources**: PyBDSF sources that were deblended into 2 or more optical sources
* **Single sources**: optical sources composed by a single PyBDSF source
* **Artifacts**: PyBDSF sources that are artifacts


## Multi-component PyBDSF sources

Multi-components PyBDSF sources correspond to optical sources that are composed by more than one PyBDSF source. These were selected from the components catalogue searching for optical sources with more than one PyBDFS component associated (9007 PyBDSFs, 3565 optical sources, `flag 8`, see section 'Multi-component PyBDSF sources' of the notebook).

Notes: 
* Around 2/3 of the total number of optical sources are made up of 2 PyBDSF sources and 1/3 of more than 2 PyBDSF sources. The number of PyBDSF sources can go up to 35 to make up one optical source.
  * Sources made up of 2 PyBDSF sources: 2489 optical sources, 4978 PyBDSFs.
  * Sources made up of more than 2 PyBDSF sources: 1076 optical sources, 4029 PyBDSFs.
* The total number of multi-component PyBDSF sources rises to 9046 PyBDSFs, 3596 optical (3596 entries) if we consider sources that have the 'Deblended_from' column but just have an optical source correspondence. These correspond to 39 PyBDSFs, 31 optical sources, 39 entries on the table, `flag 10`. See section 'Deblended sources/Sources that were not deblended/MULTIPLE PyBDSF COMPONENTS'.
* Additionally, there are sources that were associated with other PyBDSFs after having been through a deblending process (`flag 12`), which are explained in the 'Deblended sources'. 

## Deblended sources

Deblended sources are sources that were originally identified by PyBDSF as being only one source and required deblending. 
These sources were sent to a deblending workflow (ID_flag 41) or selected for deblending on LGZ (ID_flag 42). See Williams et al. 2018 for details. However, some of the sources were not actually deblended and some were deblended after association into a bigger source. For that reason, the association between the raw PyBDSF sources and the final optical sources was made through the components catalogue, using the columns 'Deblended_from' (which links directly to the PyBDSF original source names) and the 'Source_Name' (which links directly to the optical source names). 

PyBDSF sources that went through the deblending process only: 880 PyBDSF sources, 1750 optical sources, `flag 4`, 1750 entries on the table. 

Notes: 
* Most of the PyBDSF sources were deblended into to 2 optical sources but 12 were deblended into 3 optical sources.
* The total number of deblended sources ( `flag 4` and  `flag 12`) is 883 PyBDSF sources (23 PyBDSFs common to both flags), making up a total of 1780 optical sources.

### Sources that were both deblended and have multi PyBDSF components

Deblended sources where multiple PyBDSF components were associated after deblending (30 optical sources, 26 PyBDSFs, `flag 12`, 30 entries on the table. The selection of these sources is made in the section 'Deblended sources' of the notebook.

Notes: 
* When a PyBDSF source has flag 12 and is deblended into 2 or 3 optical sources (which happens only for 2 and 1 PyBDSFs respectively), it shares only an optical source with another PyBDSF with flag 10. The remaining 23 PyBSDFs flagged with 12 share an optical source with another PyBDSF flagged with 4. 
* The number of optical sources in this group correspond to the 23 PyBDSF linked to 23 optical sources, and 3 PyBDSFs to 7 optical sources (PyDBSFs deblended into more than 2 optical sources as mentioned before).



## Single sources 

A total of 313174 PyBDSF sources are classified as single sources in the output table. These are PyBDSF sources that have not been deblended, grouped with other PyBDSF sources, and that are not artifacts. The sources were selected using the components catalogue, looking for unique correspondences between the PyBDFS raw catalogue and the final optical catalogue (313161 objects, `flag 1`, see section 'Single sources' of the notebook); and from sources that were selected for deblending in LGZ but were not actually deblended (13 objects, `flag 3`, see section 'Deblended sources/Sources that were not deblended/SINGLES').


## Artifacts

There are a total of 2591 PyBDSF sources classified as artifacts in the output table. These were selected from the artifacts catalogue (2543 PyBDSFs, `flag 16`); and from the PyBDSF raw catalogue, corresponding to sources that are missing in the final optical catalogue (48 PyBDSFs, `flag 32`).

***

# Downloads 

* The jupyter notebook used to clean the catalogues can be downloaded <a href="https://github.com/laraalegre/lotss-dr1/blob/master/PyBDSF_DR1_clean_catalogues.ipynb">here</a>
* The jupyter notebook used to perform the associations can be downloaded <a href="https://github.com/laraalegre/lotss-dr1/blob/master/PyBDSF_DR1_associations.ipynb">here</a>. 
* A table with the output of the notebook can be downloaded <a href="https://github.com/laraalegre/lotss-dr1/blob/master/pybdsf_associations.fits">here</a>. 
