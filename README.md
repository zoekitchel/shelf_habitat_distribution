# shelf_habitat_distribution
How does continental shelf habitat availability change as species shift deeper and/or to higher latitudes?

Somewhat inspired by Elsen and Tingley 2015 https://www.nature.com/articles/nclimate2656?WT.ec_id=NCLIMATE-201508&spMailingID=49170365&spUserID=ODkwMTM2NjQyMAS2&spJobID=723112964&spReportId=NzIzMTEyOTY0S0

Initiated by Hailey Conrad and Becca Selden in 2018. Completed by Zoë Kitchel, and submitted to GCB January 2022. Resubmitted with major revisions to GCB May 2022. 

###Repository Folder Guide

- code
    - Most code is housed in this folder (exceptions are mostly found in Figure folder)
- Figures
    - Figure files, and some code to generate figures when not straightforward
- old_materials
    - intermediate files no longer relevant to final analyses
- output
    - data objects in rds, RData, or CSV format output by code
- raw_data
    - this is where raw data is housed and pulled from
    - includes raw LME, FAO, and bathymetry data  (ETOPO1 (current version used in analyses), ETOPO2 (earlier versions))
    - note that some files are in the .gitignore file because they are too large for github, but they are available on Box at this link: https://rutgers.box.com/s/8n9mm5f0j3s9yo5s4zexbbqkg09otvr9
    
###How to reproduce analyses
    
1. Download ETOPO1 raster in .grd format from here: https://www.ngdc.noaa.gov/mgg/global/relief/ETOPO1/data/bedrock/cell_registered/netcdf/
1. Download continental shelf shapefile in .shp format from here: https://www.bluehabitats.org/?page_id=58
1. Download FAO and LME shapefiles from:
    - FAO: http://www.fao.org/geonetwork/srv/en/main.home?uuid=ac02a460-da52-11dc-9d70-0017f293bd28
    - LME: http://lme.edc.uri.edu/index.php/digital-data/113-lme-polygon-boundaries
1. Follow code/Pull_Bathymetry_Data.Rmd to trim bathymetric raster to 0-2000m on the continental shelf. We ran this step on an HPC because ETOPO1 is so large. 
1. Follow code/depth/bathy_shelf_byLME.Rmd to calculate change in area and classification statistics for each Large Marine Ecosystem with each 15m depth shift. We ran parts of this code on an HPC because the diptest for modality takes quite a bit of memory to run. This code produces:
    - files_back_from_annotate/LME_bathy_statistics.rds
    - output/LME_bathy_statistics_full.rds
    - output/LME_bathy_statistics_full_altskew.rds
1. Follow code/depth/depth_shift_15_meters_spp_loss_gain.Rmd to calculate change in species richness associated with each 15m depth shift. Additionally, this code makes plots of depth versus percent change in species richness for Figure 1 and Figure S10. In this code, we also create Table S2. This code produces:
    - output/LME_bathy_bydepth_complete_15mbins.rds (change in area and richness for each depth band)
    - output/LME_area_spp_change_stats.rds
1. Follow code/latitude/degree_shifts_projected_2degrees.Rmd to calculate change in area and classification statistics for each coastline with each 2 degree latitude shift. We ran parts of this code on an HPC because the diptest for modality takes quite a bit of memory to run. This code also makes latitude area plots in Figures/Figure3_5/latitude_area_plots.RData, coastline maps in Figures/Figure3_5/latitude_2degree_maps.RData, and percent expansion and contraction plots in Figures/Figure6. See Figures/Figure3_5 for final figure code. This code produces:
    - shelf area data tables: output/files_back_from_annotate/eastwest_pacatlind_shelf_areas_2degrees.rds
    - lat versus area mods: output/files_back_from_annotate/eastwest_pacatlind_northsouth_mod.rds
1. Follow code/latitude/degree_shifts_projected_2degrees_richness.Rmd to calculate change in species richness associated with each 15m depth shift. In this code, we also create Table S1. Figures/Figure3_5 for final figure code. This code produces:
    - output/2_degree_latitude/shelf_areas_fullstats.rds (change in area and richness for each latitudinal band)
1. Follow Figures/Figure1/Figure1.Rmd to produce Figure 1. 
1. Follow Figures/Figure2/global_map_regions.Rmd to produce Figure 2. 
1. Follow Figures/Figure3_5/Figure3_5_code.Rmd to produce Figures 3-5.
1. Follow Figures/compiled_plots/Compiled_maps_area_depth.Rmd for Supplemental figures of all LME maps and all LME depth versus area plots. 
1. Follow Figures/Table1.Rmd to produce Table 1. 
1. Follow code/sensitivity/sensitivity_raster_polygon_comparison.Rmd to compare raster to polygon calculations of area. 
