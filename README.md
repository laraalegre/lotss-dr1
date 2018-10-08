# LoTSS-DR1

PyBDSF associations (HETDEX field) and radio properties

This jupyter notebook 'PyBDSF_DR1_associations.ipynb' inputs the LoTSS-DR1 catalogues and outputs a table with the correspondence between the raw PyBDSF sources and the final optical associations. 

## Libraries required

pandas, numpy, astropy, unittest, future

## Catalogues required

- raw pybdsf catalogue 
- pybdsf component catalogue
- optical associations (Pan-STARRS and WISE)
- artifact catalogue
- gaussian catalogue 

The notebook(s) uses **version 1.2 of the optical and components catalogues, version 0.9 of the raw PyBDSF catalogue, version 1.1 of the artifacts catalogue, and version 0.99 of the gaussian catalogue**.

## Outputs

### Optical associations
- The notebook 'PyBDSF_DR1_associations.ipynb' outputs a catalogue called 'output_table.fits'. The description of the table is explained in the <a href="https://laraalegre.github.io/lotss-dr1/">github page</a>.
- The table is created appending the different source categories throughtout the notebook. A unit test is performed to confirm the correct appending.  
- An output catalogue summary is made in the end of the notebook. 
- There is the option of exporting the cleaned catalogues in the end of the notebook.

### Radio properties
- The notebook 'PyBDSF_DR1_radio_properties.ipynb' outputs a catalogue called 'output_radio.fits', with the radio properties of the sources in the 'output_table.fits', excluding flags: 2, 3, 10, 12 and 32. 
- Flags in this catalogue:
  * Singles: flag 1
  * Deblended sources: flag 2
  * Multi-PyBDSF sources: flag 3
  * Artifacts: flag 4
