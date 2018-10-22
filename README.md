# LoTSS-DR1

PyBDSF associations (HETDEX field) 

* The notebook PyBDSF_DR1_clean_catalogues.ipynb inputs the LoTSS-DR1 catalogues and exports clean catalogues
* The notebook PyBDSF_DR1_associations.ipynb inputs the cleaned catalogues and outputs a table with the correspondence between the raw PyBDSF sources and the final optical associations 
* Here we use **version 1.2 of the optical and components catalogues, version 0.9 of the raw PyBDSF catalogue, version 1.1 of the artifacts catalogue, and version 0.99 of the Gaussian catalogue**.
* Written in python 3.7
* Libraries required: pandas, numpy, astropy, os, unittest 

## PyBDSF_DR1_clean_catalogues.ipynb 

### Inputs

* PyBDSF raw source catalogue (LOFAR_HBA_T1_DR1_catalog_v0.9.srl.fixed.fits)
* PyBDSF Gaussians catalogue (LOFAR_HBA_T1_DR1_catalog_v0.99.gaus.fits)
* PyBDSF components catalogue (LOFAR_HBA_T1_DR1_merge_ID_v1.2.comp.fits)
* Optical associations catalogue (Pan-STARRS and WISE) (LOFAR_HBA_T1_DR1_merge_ID_optical_f_v1.2.fits)
* Artifacts catalogue (LOFAR_HBA_T1_DR1_merge_ID_v1.1.art.fits)

### Outputs

* Cleaned catalogues: artifacts.fits, optical.fits, components.fits, pybdsf.fits, gaussians.fits


## PyBDSF_DR1_associations.ipynb

### Inputs 

* Cleaned catalogues: artifacts.fits, optical.fits, components.fits, pybdsf.fits, gaussians.fits

### Outputs

* PyBDSF - Optical associations table: 'pybdsf_associations.fits'. 
* The description of the table is explained in the <a href="https://laraalegre.github.io/lotss-dr1/">github page</a>.
* The table is created appending the different source categories throughout the notebook. A unit test is performed to confirm the correct appending.  
* An output catalogue summary is made in the end of the notebook. 
