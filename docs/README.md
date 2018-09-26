#  PyBDSF-Optical associations over the HETDEX field

LoTSS-DR1 is the first public data release of the LOFAR Two-metre Sky Survey (LoTSS, Shimwell2017). LoTSS-DR1 (described in Shimwell et al. 2018) surveys the HETDEX field.

> The source detection in LoTSS-DR1 is performed using the Python Blob Detector and Source Finder Software (PyBDSF, mohan2015), by fitting  Gaussians to pixel islands. This generates components rather than true sources. For that reason, the identification of LOFAR radio sources as well as the cross-matching with optical counterparts (Pan-STARRS and WISE) was achieved using a combination of statistical likelihood ratio techniques and visual inspection via a private LOFAR Galaxy Zoo (LGZ) classification project (described in Williams et al. 2018).

Here we present the connection between each of the raw PyBDSF sources and the final optical associations:

* The jupyter notebook can be downloaded <a href="PyBDSF_DR1_associations.ipynb">here</a>. 
* A table with the output of the notebook can be downloaded <a href="output_table.fits">here</a>. 

***

# Catalogues

## Catalogues used (available soon)

* PyBDSF raw catalogue 
* PyBDSF components catalogue
* Optical associations catalogue (Pan-STARRS and All WISE)
* Artifacts catalogue

### Cleaning the Catalogues

* A source was picked on 2 different mosaics (same 'Source_Name') and was classified as an artifact in one mosaic and as a source in other. This source was renamed with the original name followed by 'B'. This was done on both **Artifacts catalogue** and **PyBDSF raw catalogue** (the source appears twice on the PyBDSF raw catalogue).
* Duplicated entries were removed from the PyBDSF **components catalogue** (9 duplicated 'Source_Name' and 'Component_Name' for the same source).
* A source on the PyBDSF **components catalogue** was removed because it is an artifact ('Component_Name' is on the artifact catalogue).

For more details see section `Catalogues` of the notebook.

## Output Catalogue

The notebook creates an output table (`output_table.fits`) with 3 columns: 

* **pybdsf_name**: original PyBDSF source names (as in the PyBDSF raw catalogue)
* **association_name**: optical name (as in the optical associations catalogue) or lackof association (null) 
* **flag**: category of the sources. 

The PyBDSF-optical relation comprises 4 main categories:

* **Deblended sources**: PyBDSF sources that were deblended into 2 or more optical sources
* **Multi-component PyBDSF sources** : optical sources composed by Multiple PyBDSF components
* **Single sources**: optical sources composed by a single PyBDSF
* **Artifacts**: PyBDSF sources that are artifacts

The flags as well as the combination of flags is explained next.

***

# Sources

## Deblended sources

Deblended sources are sources that were originally identified by the PyBDSF software as being only one source and require deblending. 
These sources were sent to a deblending workflow (ID_flag 41) or selected for deblending on Lofar Galaxy Zoo (ID_flag 42). See Williams et al. 2018 for details (available soon). However some of the sources were not actually deblended and some were deblended after association into a bigger source. For that reason, the association between the raw PyBDSF sources and the final optical sources was made through the components catalogue, using the columns 'Deblended_from' (which links directly to the PyBDSF original source names) and the 'Source_Name' (which links directly to the optical source names). 

The total number of Sources that went through a deblending process is :

* Number of PyBDSF components that were deblended: 925
* Number of correspondent optical sources: 1784
* Number of entries on the table: 1822

This corresponds to sources that went through the deblending process only (832 PyBDSF components, 1575 optical sources, `flag 4`, see section 'Deblended sources' of the notebook) and deblended sources where the PyBDSF components were associated after deblending (see Multi-component PyBDSF sources below for more details).

TO CHECK:  (832 PyBDSF components deblended at least into 2 sources makes 1664)


## Multi-component PyBDSF sources

Multi-components PyBDSF sources correspond to optical sources that are composed by more than one PyBDSF component. These were selected from the components catalogue looking for optical sources with more than one PyBDFS component associated (3565 optical sources, 9007 PyBDSFs, `flag 8`, see section 'Multi-component PyBDSF sources' of the notebook).

Additionally, there are sources that were associated with other PyBDSFs after having been through a deblending process (193 optical sources, 209 PyBDSFs, `flag 12`). 


TO CHECK: 

- A total of 3774 optical sources are composed by more than one PyBDSF component and 9868 PyBDSF components make up these 3774 sources. Note that some optical sources can have up to 35 PyBDSF components and also that included in these numbers are the sources that went also through the deblending process (flag = 8 and flag = 12). 
- Check this: A total of 9255 PyBDSF sources are classified as 'multi-components' in the output table.
(but not have been deblended) - I think this number is just a prediction


## Single sources 

A total of 313171 PyBDSF sources are classified as singles sources in the output table. These are PyBDSF sources that have not been deblended, grouped with other PyBDSFs sources, and that are not artifacts. The sources were selected using the components catalogue, looking for unique correspondences between the PyBDFS raw catalogue and the final optical catalogue (313161 objects, `flag 1`, see section 'Single sources' of the notebook); and from sources that were selected for deblending in Lofar Galaxy Zoo (LGZ) but were not actually deblended (10 objects, `flag 3`, see section 'Deblended sources/Sources that do not seem to be deblended' of the notebook).


## Artifacts

There are a total of 2591 PyBDSF sources classified as artifacts in the output table. These were selected from the artifacts catalogue (2543 PyBDSFs, `flag 16`); and from the PyBDSF raw catalogue, corresponding to sources that are missing in the final optical catalogue (48 PyBDSFs, `flag 32`).

***

# Flags

| category                 | selection                               | flag  | n PyBDSF  | n optical |
|:-------------------------|:----------------------------------------|:------|:----------|-----------|
| Single sources           | Unique PyBDSF-optical correspondence    |   1   | 313161    | 313161    |
| Deblending problems      | Not deblended                           |   2   | 0         | 0         |
| Single + not deblended   | combination of flags 1 and 2            |   3   | 10        | 10        |
| Deblended sources        | Multiple PyBDSF-optical correspondences |   4   | 832       | 1575      |
| Multi-component PyBDSF   | Merged PyBDSF-optical correspondences   |   8   | 9007      | 3565      |
| Deblended + Multi-comp.  | Combination of flgas 4 and 8            |   12  | 193       | 209       |
| Artifacts                | Artifact catalogue                      |   16  | 2543      | 2543      |
| Artifacts                | PyBDSF missing in optical catalogue     |   32  | 48        | 48        |

***




