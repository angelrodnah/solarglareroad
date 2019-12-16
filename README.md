# solarglareroad
Version 1.0 12/6/2019

This is a geographic analysis that calculates the road segments that are vulnerable to solar glare, in the hope that accidents caused by direct sun glare, when the sun is only a few degrees off the direction of travel, in both the horizontal and vertical angles, can be avoided, either by scheduling delivery travel at other times, or by posting signs along the roadway as warnings. The slope and direction of the road are compared at every 5 minute interval, for every 100m road segment in the study area to the horizontal and vertical angle of the sun. 

The number of calculations are large and the use of jupyter notebooks with spatial panda dataframes are used. All attribute calculations are done within pandas when possible, with only a small amount of calculations required from the ArcGIS Pro libraries, which are primarly needed for the import and export of the elevation and featureclass data, and the calculation of the elevation values at the end of each road segment, and the roadsegment bearing. The astronomy python library has the functions needed to find the position of the sun, for a particular day, time, and lat/long coordinate position. The rest of the script is simply a set of logic to set up and manage the calculations in an effecient manner. 

ArcGIS Pro 2.4 is needed, along with a modified python environment to add in the astronomy libary. For the given study area, a local elevation raster and the streets featureclass are the only inputs, along with the day of the year that is being studied. The output is a featureclass of road segements that are vulnerable to solar glare, alond with added attribures for the vertical and horizontal angles that were calculated.

In ArcGIS Pro obtain some 3D street centerline featureclass data for your study area, and a rough elevation raster local tif that covers that same area.  You could export this from the ArcGIS Living Atlas Terrain layer or obtain it elsewhere. The elevation area can be larger of course. Also obtain the single lat long coordinate for the roughly the center of your study area in decimal degrees. Choose one day of the year on which to perform the analysis.  

This analysis could be expanded to be done every day of the year, and for multiple study areas, with additional scripting and data management. The current study area analysis presented here uses one coordinate location to get the sun position for all the roads in that area in order to vastly simply the analysis time. If you feel the area is too large for one sun position, break your study area in grids and groups of streets for each grid, and obtain a center point for each grid. Write your own logic to loop through each of these study areas, using each center point and streets selection as the input. The analysis is also only for one day of the year. If you want to do more than one day, just run the entire analysis for additional days, for each study area. 

The analysis is done completely in Jupiter notebooks using the ArcGIS Pro python environment on the local computer. However, you will need to add the astropy astronomy library to your ArcGIS Pro python environment. I am using ArcGIS Pro 2.4.2.  Clone your python environment in ArcGIS Pro and add astropy to the clone, and use this new environment. (Project/python/manage environments/clone Choose the cloned environment as the active one, and add the library called astropy).  

Possible errors and messages:
In several tools you might get this a tool validator license warning which you can ignore. You might also get an error with the astropy site that tries to reach out to get some tables from a .mil website. You can see the code in the function can be altered to use interpolated tables instead or offline mode.

To see the result add to Pro and set up a time slider and you can see the road segments affected by solar glare. 3D enhanced road geometry is an additional bonus output. Added is a zip file containing a geodatabase for sample output for the City of Falls church for several times of the year. You will need to provide your own input data for your study area.
