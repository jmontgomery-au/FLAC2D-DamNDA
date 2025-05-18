# Nonlinear Deformation Analysis of Dams using FLAC2D
These files are meant to demonstrate the basic process for performing a nonlinear deformation analysis (NDA) using FLAC2D with a focus on earthen dams subject to seismic liquefaction. The input files are intended to work with both perpetual (v9.0) and the latest subscription (currently v9.3) versions of FLAC2D. The analysis approach follows the basic framework described by [USSD (2022)](https://www.researchgate.net/publication/365614343_Analysis_of_Seismic_Deformations_of_Embankment_Dams) and [Boulanger et al. (2015)](https://www.researchgate.net/publication/272818560_Ch_10_Nonlinear_Deformation_Analyses_of_Liquefaction_Effects_on_Embankment_Dams). Input files are provided for the Upper and Lower San Fernando Dams, along with a generic earth dam with a coarse mesh that can be analyzed without a license. 

## Downloading the Files
  1. Download the files for the problem you wish to solve. [Instructions here](https://docs.github.com/en/repositories/working-with-files/using-files/downloading-source-code-archives)
  2. Unzip the files in the folder where you wish to run the simulations.
  3. Make sure you have added the [PM4Sand](https://pm4sand.engr.ucdavis.edu/) and [PM4Silt](https://pm4silt.engr.ucdavis.edu/) models to FLAC. 
  4. Open the project (.prj) file with FLAC2D.
  5. Select input file "0_RunAll" and execute. 

## File Organization
All three simulations follow the same basic analysis approach. A decoupled approach is used to establish initial equilibrium, while a coupled approach is used for the seismic analysis. A post-earthquake stability analysis is also performed using residual strengths in liquefied zones. 

First the model is initialized and the geometry is loaded from a previously exported FLAC2D grid file (see "Import Grid.dat"). Then the simulation is solved in the following stages:<br/>
- 1_BuildRock.dat - Solve for mechanical equilibrium of the elastic bedrock.<br/>
- 2_BuildAlluvium.dat - Solve for mechanical equilibrium of the alluvium layer.<br/>
- 3_IniWT.dat - Solve for initial water table in the foundation. The fluid calculations in this stage are decoupled.<br/> 
- 4_BuildDam.dat - Solve for mechanical equilibrium in the dam by constructing in layers. The construction sequence is defined in the group names. The dam is constructed dry.<br/> 
- 5_AddBerm.dat (Not used for USFD) - Solve for mechanical equilibrium in the berm by constructing in layers. The construction sequence is defined in the group names. The dam is constructed dry.<br/> 
- 6_RaiseRes.dat - Raise the reservoir in stages and solve for fluid and mechanical equilibrium using a decoupled approach.<br/> 
- 7_DynSetup.dat - Switch to dynamic models (PM4Sand and PM4Silt) and solve for mechanical equilibrium.<br/> 
- 8_DynamicShake.dat - Apply earthquake loading and solve for duration of record.<br/> 
- 9_QuietTime.dat - Solve for a period of quiet time after the earthquake to allow vibrations to damp out.<br/>
- 10_ResStrength.dat - Apply post-earthquake strengths and solve for a period of time to determine post-earthquake stability.<br/>

Several other input files are called at different stages of the simulation. Each of these is briefly described below.<br/>
- *.f2grid - Exported grid file containing the gridpoints, zones, and group names for the selected problem.<br/>
-	Import_Grid_*.dat - File to initialize FLAC2D and import previously exported FLAC2D grid file. Seperate files are provided for subscription and perpetual versions.<br/>
-	Static_Properties.dat - File containing the properties used for static equilibrium of all layers except the bedrock (defined in 1_BuildRock.dat).<br/>
-	Static_Functions.dat - File containing several functions used during the static equilibrium phase of the simulation.<br/>
-	Dynamic_Properties.dat - File containing the properties used for dynamic stage of the simulation.<br/>
-	Dynamic_Functions.dat - File containing several functions used during the dynamic stage of the simulation.<br/>
- DynHisLocations.dat - File containing the locations for all histories.<br/>

## A Word of Caution
These files were created as a teaching and research tool and NOT as a template for building an engineering analysis. They are not intended to be used for any purpose other than teaching and academic research. The files are provided without any implied warranty of fitness for any purpose or use whatsoever. Users should seek advice from a licensed professional engineer with experience in performing seismic analyses of dams before using any part of this code for any purpose other than learning.

## Interested in Learning More?
These files were developed by Dr. Jack Montgomery (PE AL). Dr. Montgomery is available for collaborations, individual and group training, technical review, and mentoring in the use of advanced numerical simulations for geotechnical problems, with a focus on earth dams, tailings dams, and landslides. Training programs can be customized to fit the needs and interests of the client with the objective of helping participants improve their modeling skills and build confidence in their results. If you are interested in learning more, please reach out through [email](mailto:jmontgomery@auburn.edu).  

## Acknowledgements
These input files were developed over a long period of time and benefited from discussion and advice from many individuals. Special thanks to Professors Ross Boulanger, Katerina Ziotopoulou, and Richard Armstrong and Dr. Michael Beaty. Portions of the development of these simulations were supported by the California Division of Safety of Dams, the United States Society on Dams, and the Itasca Educational Partnership program.Any opinions, findings, conclusions, or recommendations expressed herein are those of the author and do not necessarily represent the views of these organizations or individuals.

Please send your comments, bugs, issues and suggestions for improvement to Jack Montgomeryat jmontgomery@auburn.edu.
