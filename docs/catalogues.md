# Catalogues

Here we use the **version 1.2 of the optical and components catalogues, version 0.9 of the raw PyBDSF sources, version 0.99 of the Gaussians catalogue, and version 1.1 of the artifacts catalogue**. All catalogues are available on LoTSS-DR1 webpage. 

## Input catalogues

* <a href="https://www.lofar-surveys.org/public/LOFAR_HBA_T1_DR1_catalog_v1.0.srl.fits">Radio source catalogue<a> (PyBDSF raw catalogue) (*LOFAR_HBA_T1_DR1_catalog_v0.9.srl.fixed.fits*) 
* <a href="https://www.lofar-surveys.org/public/LOFAR_HBA_T1_DR1_merge_ID_v1.2.comp.fits">PyBDSF components catalogue<a> (*LOFAR_HBA_T1_DR1_merge_ID_v1.2.comp.fits*) 
*  <a href="https://www.lofar-surveys.org/public/LOFAR_HBA_T1_DR1_merge_ID_optical_f_v1.2b_restframe.fits">HETDEX associations and optical IDs catalogue<a>(*LOFAR_HBA_T1_DR1_merge_ID_optical_f_v1.2.fits*)
* Artifacts catalogue (*LOFAR_HBA_T1_DR1_merge_ID_v1.1.art.fits*)
* Gaussian catalogue (*LOFAR_HBA_T1_DR1_catalog_v0.99.gaus.fits*)

#### Cleaning the Catalogues

* A source appears in 2 different mosaics and was classified as an artifact in one mosaic and as a source in the other. This source was renamed replacing the last character of the original 'Source_Name' by 'B'. This was done on both **Artifacts catalogue** and **PyBDSF raw catalogue** (the source appears twice on the PyBDSF raw catalogue).
* Duplicated entries were removed from the PyBDSF **components catalogue** (9 duplicated 'Source_Name' and 'Component_Name' refering to the same source).
* A source on the PyBDSF **components catalogue** was removed because it is an artifact ('Component_Name' is on the artifact catalogue).

For more details see notebook **_PyBDSF_DR1_clean_catalogues.ipynb_**.
