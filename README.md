# LoTSS-DR1

PyBDSF associations (HETDEX field)

This jupyter notebook inputs the LoTSS-DR1 catalogues and outputs a table with the correspondence between the raw PyBDSF sources and the final optical associations. 

## Libraries required

pandas, numpy, astropy, unittest

## Catalogues required

- raw pybdsf catalogue 
- pybdsf component catalogue
- optical associations (Pan-STARRS and WISE)
- artifact catalogue

The notebook uses **version 1.2 of the optical and components catalogues, version 0.9 of the raw PyBDSF catalogue, and version 1.1 of the artifacts catalogue**.

## Outputs

- The notebook outputs a catalogue called 'output_table.fits'. The description of the table is explained in the <a href="https://laraalegre.github.io/lotss-dr1/">github page</a>.
- The table is created appending the different source categories throughtout the notebook. A unit test is performed to confirm the correct appending.  
- An output catalogue summary is made in the end of the notebook. 


