# PITTSBURGH BUILDING BENCHMARKING PROJECT: PROCESS LOG
### City Planning Department’s Division of Sustainability and Resilience
### Summer, 2019

**July 1-10, 2019: Data cleaning (Round 1)**
- Decided how to organize Energy Star Portfolio Manager source data (.csv) in Excel
  - Separate workbooks (no tabs importable to ArcGIS) 😊
    - Year (and/or) 😊 
    - Building type ☹ 
  - Single workbook ☹ 
    - Would have to import updated file every year ☹ 

*Data cleaning protocol for created datasets* 
- Cleaning protocol for “2017ComplianceMapData”
    - Move original file into ‘Data’ folder in ArcGIS project directory
    - Standardize data fields across all tabs
      - PBBID_1 – Pittsburgh Building Benchmarking ID
      - PBBID_2 – Campus Building Benchmarking ID
      - PARCEL_ID_1
      - PARCEL_ID_2
      - TYPE
      - BUILDING_NAME
      - ENTITY_NAME
        - New field encompassing “Business Name” and “Campus” fields
  - OWNER
  - ADDRESS_1
      - Create using function =concatenate([STREET_NUMBER],” “,[STREET_NAME]
    - STREET_NUMBER
    - STREET_NAME
    - CITY
    - ZIP
    - COMPLIANCE STATUS
    - COMMENTS
  - Merge all tabs into single worksheet (one year’s data)
  -	Find/replace all occurrences of “#N/A” to empty (null) cells
  -	Find/replace all occurrences of “Exempted” and “#NA” in “BUILDING_NAME” field to empty (null) cells
  -	Eliminate all unnecessary spaces and <BR> in “ENTITY_NAME” and “OWNER” fields
  -	Eliminate COMMENTS field
  -	Save file as “[Original file name]_Cleaned” (.csv)
  -	Archive original source files
-	Cleaning protocol for “Final_Building_Benchmarking”
  -	Rename PIN as PARCEL_ID_1
  -	Create new field named PARCEL_ID_2 to the right of PARCEL_ID_1
  -	For any records containing multiple Parcel IDs, cut/paste second Parcel ID into PARCEL_ID_2 column
  -	Create new field named ADDRESS_1 to the left of AddressFull (column J)
  -	Use formula =LEFT(J2,(FIND("Pittsburgh",J2,1)-1)) to extract address street number and name
  -	Rename PBBID as PBBID_1
  -	Rename Campus PBBID as PBBID_2
  -	Rename Property owner as OWNER
  -	Rename Building name as BUILDING_NAME
  -	Rename Type as TYPE
  -	Rename Compliance status as COMPLIANCE_STATUS
  -	Use find/replace function to delete all occurrences of “Â” in AddressFull and ADDRESS_1 columns
  -	Find/replace all occurrences of “NA” to empty (null) cells
  -	Save file as “[Original file name]_Cleaned” (.csv)
  -	Archive original source files

*Data cleaning protocol for exported datasets*
-	Cleaning protocol for “overview (12)” 
  -	Move original file into ‘Data’ folder in ArcGIS project directory
  -	Delete any title (non-header) rows outside of data table or convert to data table fields
  -	Keep all existing data fields
  -	Add field: PBBID but leave empty
  -	Add field: PARCEL_ID_1 using “Final_Building_Benchmarking_Cleaned” data table
    -	Not all records match. Export to ArcGIS or Access to join tables
  -	Save file as “CityBuildingEnergyData_Cleaned” (.csv)
  -	Archive original source file

-	Cleaning protocol for “Data Request_Pittsburgh Benchmarking Compliance Report-Year 2 (2)” 
  -	Move original file into ‘Data’ folder in ArcGIS project directory
  -	Delete any title (non-header) rows outside of data table or convert to data table fields
  -	Keep all existing data fields
  -	Add field: PARCEL_ID_1 using “2017ComplianceMapData” data table
  -	Add missing PBBID by cross-referencing Compliance Data
  -	Standardize data fields across all tabs (if applicable)
  -	Delete extraneous tabs or merge all tabs into single worksheet representing one year’s data (if applicable)
  -	Rename field “Pittsburgh Building Benchmarking ID” to “PBBID_1” (PBBID_1 will serve as the join field in ArcGIS for merging with compliance data table )
  -	Find/replace all occurrences of “Not Applicable: Standalone Property”, “NA”, “Not Available”, and “None” to empty (null) cells
  -	Save file as “[Original file name]_Cleaned” (.csv)
  -	Archive original source file
-	Import cleaned data into ArcGIS project: PittsburghBenchmarkingMap
-	Emailed Geoffrey Arnold (geoffrey.arnold@pittsburghpa.gov) from I&P about data cleaning protocol for Compliance data
  -	Received file “Final_Building_Benchmarking” 
-	Emailed Seth Fitzsimmons (seth@mojodna.net) from City Energy Project about data cleaning protocol for Energy Star Portfolio Manager data.
  -	Referred to Jim Stanley (jim@stamen.com) at Stamen
  -	Referred to Eric Brelsford (ebrelsford@stamen.com) at Stamen
 
*Protocol for Access*
-	Create a new database in Access. Save database as “Pittsburgh_Building_Benchmarking”
-	Import data tables from Excel (files must be in .xls format)
  -	Final_Building_Benchmarking 
  -	Data Request_Pittsburgh Benchmarking Compliance Report-Year 2 (2) 
  -	Allegheny County Parcels
  -	Allegheny County Buildings
  -	Allegheny County Addresses
-	In import box, make the following selections:
  -	Click ‘Browse’ and select location of source data (‘Data” folder of ArcGIS project directory). Select the option “import the source data into a new table in the current database” (this is the default selection). Click OK.
  -	Click box for “First row contains column headings.” Click next.
  -	In the Field Options window, make no selections or changes. Click next.
  -	Select option “Let Access add primary key.” Click next.
  -	Name your table and click Finish.
  -	Do not save import steps.
-	Create data table schematic

**July 19, 2019 – QA/QC: Data consistency check**
-	Copy/paste Address and Property Name fields into separate tabs by data set pairs
  -	2017 PM + 2018 PM
  -	2017 PM + Cartegraph
  -	2018 PM + Cartegraph
-	First, check for internal duplicates (false positives) for both the Address and Property Name Fields. 
-	Second, check for external duplicates (true positives) for both the Address and Property Name Fields.
-	Third, verify internal duplicates are also external duplicates and note any reconciled records (true positives)
-	Fourth, 

**July 22-24, 2019 – QA/QC on City building data sets**
-	In Excel, compare 2017-2018 Portfolio Manager (PM) data sets with Cartegraph data set to identify inaccuracies in address and property name fields. 
  -	Goal: Make all addresses and property names match corresponding records in Cartegraph data set.
-	Copy relevant records from each data set into a new Excel workbook and save file as “2017-2018 PM_Categraph Data Duplicate Check.”
-	Use conditional formatting to identify internal duplicates in each data set separately for both the address and property name fields. Provide tallies on the side.
-	In separate tabs, pair the data sets as follows:
  -	2017 PM data + Cartegraph
  -	2018 PM data + Cartegraph
  -	2017 PM data + 2018 PM data
-	In the tabs for each data set pair, use conditional formatting to identify external duplicates (i.e., matching records) for both the address and property name fields. Provide tallies on the side.
  -	Disambiguate true matches (external duplicates) from false matches (internal duplicates)
-	Check all records in the 2017 and 2018 PM data sets that don’t match a record in the Cartegraph. Make a list of these records in a Word document.
  -	Check for errors in the address and property name fields that might explain these non-matching records and correct names as necessary. 
  -	Create a copy of the Excel file. Save as “2017-2018 PM_Categraph Data Duplicate Check2.”
  -	Find/replace all occurrences of street, avenue, boulevard, drive, lane, and road in 2017-2018 PM data and change to st, ave, blvd, dr, ln, and rd to match Cartegraph records.
  -	Be careful of road names that contain the word “road” and correct any inadvertent changes (e.g., Broadway, etc.)
-	Repeat steps above to identify duplicates and recalculate tallies. 
-	Revise list in Word accordingly. 
-	Optional: Use the UPPER function to populate a new field “ADDRESS” with the address names transcribed to all caps to match the Cartegraph records (e.g., =upper(B2)). 

**July 29, 2019 – 2017-2018 City Building Energy Data cleaning**
-	Use data cleaning protocol for exported data sets to clean 2017 City Building Energy Data (original file name: “overview 2017”)
  -	Save “overview 2017” as “2017 City Building Energy Data.” Archive original file.
  -	Join “2017 City Building Energy Data” to “”
    -	Only 5-10% match on Address field between data sets ☹ 
  -	Can’t match on Address – only 10-15% match with Pittsburgh Address map layer
  -	Parcels…? 
    - Will likely be multiple buildings on a single parcel, have to disambiguate with Google Maps and assign unique ID to differentiate (BL_ID)
    -	Simplest solution to matching problem is to have a linking table matching PBBID to OBJECTID from building footprint layer.
    -	Alternatively create a new building map layer for any building falling under benchmarking ordinance (maybe using Mapbox building map layer for Pittsburgh or following their protocol) and assign buildings something like PBBID, but at right level of granularity (BL_ID, UBID?). Another linking table connecting PBBID to BL_ID/UBID.
  -	PBBID – City Buildings don’t have PBBID

**July 30-Aug. 2, 2019 – Create 2017 Covered Building List map layer**
-	Import 2017ComplianceMapData_Cleaned_Test csv file into project geodatabase. Rename the data table Covered_Buildings_2017.
-	Use definition query to exclude any record where Parcel_ID_1 is null. This action should result in 648 remaining records.
-	Join Covered_Buildings_2017 data table to Pittsburgh Parcels map layer. Unclick box for “keep all target features” in order to execute an inner join. This action should result in 627 records. Rename resulting map layer “2017CoveredBuildings_Parcels.”
-	Create a copy of PittsburghBuildings map layer and rename it CoveredBuildings2017.
-	Run spatial join on CoveredBuilding2017 and 2017CoveredBuildings_Parcels map layers. This will add the Parcel_ID_1, Type, PBBID, and Address1 attributes to the CoveredBuildings2017 map layer. This results in 1,010 records.
  -	Eventually you should do this with the CMU buildings also.
  -	Use a one to one join and then manually eliminate records for smaller buildings
    -	Can covered buildings be filtered using feature attributes, e.g., polygon area? 
-	Use Add Geometry Attributes tool and calculate Geodesic area in square meters
-	Use Minimum Bounding Geometry tool to exclude records below 50,000 square meters (?)
-	See http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-statistics-toolbox/calculate-areas.htm
-	Use definition query to filter out records with no matching address in the covered building list. This action should result in 815 records. Use gradient fill to color code records by building type.
-	Import Cartegraph Facilities map layer into project geodatabase. Rename map layer “CityFacilities.” This map layer contains 406 records.
-	Make a copy of the CityFacilties map layer. Run a spatial join between the CityFacilities and CoveredBuildings_2017_SpatiaJoin map layers. Unclick box for “keep all target features” in order to execute an inner join. This action should result in 406 records. Name the resulting layer “CityFacilities_SpatialJoin.”
  -	Spatial Join results in very few joins. Problem may be with type of spatial join (looking for complete overlap or enclosure?) or incompatible geographic coordinate settings.
    -	See https://pro.arcgis.com/en/pro-app/help/mapping/properties/geographic-coordinate-system-transformation.htm and https://pro.arcgis.com/en/pro-app/help/mapping/properties/specify-a-coordinate-system.htm
  -	2017CoveredBuildings_Parcels map layer include BlockLot ID which can be joined to Facilities map layer (no BlockLot ID in Geoffrey’s Cartegraph data; no PIN in Facilities map layer)
    -	Alternatively, try using Address field
-	Flag: Building footprints map layer includes unique records for internal courtyards and other non-structures. This will overrepresent the number of buildings in the covered buildings list and distort the way buildings display in Mapbox, etc. Solution: Delete these records and/or interior polygon features.
-	Flag: Does join operation (one to one vs. one to many have directionality? E.g., does changing the order of the target and join data set have any effect on the join operation?

**Aug. 5, 2019 – QC Covered Buildings List map layer**
-	In 4298_CoveredBuildingList worksheet in Excel, use concatenation function to create new field containing full address of covered building.
-	Use find/replace to eliminate all redundant spaces.
-	Save edited file as CoveredBuildingList_Cleaned. Save a copy as a .csv file.
-	Import CoveredBuildingList_Cleaned table into ArcGIS project geodatabase. Name the table Covered_Building_List.
-	Join Covered_Building_List table to a copy of the PittsburghAddresses map layer. Name the resultant map layer CoveredBuildingsList_Addresses.
-	Make a copy of CoveredBuildingsList_Addresses map layer. Use spatial join to identify with records intersect with CoveredBuilding footprint.
-	Run a find unmatched to identify which records do not intersect a CoveredBuilding footprint. Name the resultant map layer UnmatchedAddresses. Use an 8 pt red circle to represent unmatched addresses. 
-	Use color coding to distinguish matching records between relevant map layers:
  -	AddressCvdBldgs_Intersect (green circle, 6 pt) – Intersecting records between CoveredBuildingsList_Addresses and CoveredBuildings2017_SpatialJoin map layers. 
  -	AddressPittBldgs_Intersect (orange circle, 6 pt) – Intersecting records between CoveredBuildingsList_Addresses and PittsburghBuildings map layers.
  -	UnmatchedAddresses (red circle, 6 pt) – Non-intersecting records between CoveredBuildingsList_Addresses and PittsburghBuildings or CoveredBuildings2017_SpatialJoin map layers. 
-	Refer to red circles to identify covered buildings with no corresponding record in the CoveredBuildings2017_SpatialJoin map layer. Highlight these records in the CoveredBuildingList_Cleaned worksheet in Excel. Create a new sheet in workbook containing only (35) unmatched records.
-	Check unmatched records one by one to determine reason for no match. Delete any false positives. 

**Aug. 15-20, 2019 – Join 2017-2018 PM data to Facilities.csv table**
-	Clean Facilities.csv. Rename Facilities_Cleaned and archive original file.
-	In Excel, update all property name and address fields for overview2017 and overview2018 data sets.
-	Add X,Y data using Facilities.csv as the source data file. Keep the default coordinate system. Name the resulting point layer “FacilitiesCentroids.”
-	Import cleaned overview2017 and 2018 data tables into the ArcGIS project geodatabase. Name the tables PublicFacillities_2017PM and PublicFacilities_2018PM.
-	Inner join the FacilitiesCentroids map layer (406 records) with the PublicFacilities_2017PM and PublicFacilities_2018PM data tables (154 records). This action should result in 153 records. Name the resulting map layers CityFacilities_2017PM_Join and CityFacilities_2018PM_Join, respectively. 
-	Export CityFacilities_2017PM_Join and CityFacilities_2018PM_Join to project geodatabase.

*Join Troubleshoot*
-	Inner join between Facilities_Centroids map layer (406 records) and overview2017 and 2018 data (154 records) should yield 152 records (2 unmatched). Name resulting layers FacilitiesCentroids_2017PM_Join and FacilitiesCentroids_2018PM_Join.
  -	Result: Action results in only 146 records. 9 records unmatched. 8 of these are partially unmatched while the remaining 1 record (Schenley Museum) is completely unmatched. 
    -	Test 1: Fix property name and/or address fields in respective data sets. All 8 partial errors are in the address field. Correct these 8 records, run inner join. 
-	Result: Even with all the address fields corrected, still yields only 146 records when joined on Property Name field. Near perfect join (null record for Boat Safety Building) between Centroid and Centroid_PM2017_Join layers. Problem seems to be with Overview2017 layer. 
  -	Test 1b: Try inner join on address field.
    -	Result: This results in 0 records returned. 
-	Test 1c: In Excel, use Proper function to convert Centroids Addresses to proper capitalization format. Rerun inner join using Address field.
  -	Result: This results in 168 records returned. This likely owes to duplicate address names (without street number).
  -	Test 1d: Rerun inner join on Property Name field.
	Result: This results in 153 records. (If records are missing, be sure to check for internal duplicates creating false matches and capitalization.)

-	Inner spatial join between PittsburghBuildings (116,120 records records) map layer CityFacilities_2017PM_Join and CityFacilities_2018PM_Join (153 records each). Action should result in 153 records. Name resulting layers CityBuildings_2017PM and CityBuildings_2018PM, respectively. 
  -	Action results in 139 records (153-139 = 14 missing records).
    - Missing records include:
      - Arlington Field Lights Building	0 Sterling St
      - Arlington Gym	2201 Salisbury St
      - Brighton Heights Senior Center	3515 Mcclure Ave
      - Firehouse 30	916 Steuben St
      - Fowler Recreation Center	2438 Wilson Ave
      - Medic 03 Police Zone 06	312 S Main St
      - Medic 10	2800 Shadeland Ave
      - Public Works Frick Park Office Building	1 English Ln
      - River Safety Boathouse	<Null>
      - Riverview Pool Building	 Riverview Dr
      - Schenley Park Pool Building	10026 Overlook Dr
      - Schenley Park Skating Rink Building	10341 Overlook Dr
      - West Penn Pool Building	470 Paulowna St
      - West Penn Pool Entrance Building	470 Paulowna St

-	If necessary, use Calculate field to convert Total GHG Emissions data type from text to double (numeric).
-	If necessary, use Calculate field to convert Site and Source EUI fields from text to double (numberic).
-	Export CityBuildings_2017PM and CityBuildings_2018PM into project geodatabase.
-	Change symbology to graduated colors using Total GHG emissions field and 6 classes Orange-Red (Natural Breaks, Jenks).
-	Perform inner join between Facilities shapefile (406 records) and CityFacilities_2017PM and CityFacilities_2018PM (154 records each). Actions results in 153 records. Name the resulting layer CityBuildings_2017PM_Supplement. 
-	Export CityBuildings_2017PM_Supplement and CityBuildings_2018PM_Supplement map layers to project geodatabase.
-	Change symbology to graduated colors using Total GHG emissions field and 6 classes Orange-Red (Natural Breaks, Jenks).
-	Move CityBuildings_2017PM_Supplement and CityBuildings_2018PM_Supplement map layers just below CityBuildings_2017 and CityBuildings_2017 map layers. 
  -	Optional: Use definition query to only display 14 missing buildings listed above.

**Aug. 21, 2019 – Visualize City Buildings Energy Use in Mapbox**
-	Use Features to JSON tool to convert CityBuildings_2017PM_Supplement and CityBuildings_2018PM_Supplement map layers into GeoJSON files. Check the box for Project to WGS_1984. Names the resulting files PublicFacilities_2017PM_ WGS1984 and PublicFacilities_2018PM_WGS1984, respectively.
-	In Mapbox, upload the PublicFacilities_2017PM_ WGS1984 and PublicFacilities_2018PM_WGS1984 data sets and export them as tiles.
-	Use Features to JSON tool to convert CMU_Buildings, CoveredBuildings2017_SpatialJoin, and PittsburghParks map layers into GeoJSON files. Check the box for Project to WGS_1984. Names the resulting CMU_Buildings_WGS1984, CoveredBuildings2017_WGS1984, and PittsburghParks_WGS1984, respectively.
-	In Mapbox, upload the CMU_Buildings_WGS1984, CoveredBuildings2017_WGS1984, and PittsburghParks_WGS1984 data sets and export them as tiles.
-	Create a new Style using the Light template. In the new Style, add two copies of the PublicFacilities_2017PM_ WGS1984 and PublicFacilities_2018PM_WGS1984 tiles. 

**Aug. 22, 2019 – Add CMU energy use map layer to ArcGIS project**
-	Restore SummarizeWithin data tables / map layers from SustainableCampus project geodatabase.
-	In Excel, filter the aggregate CO2e emissions data for all CMU buildings for FY 2014-2018. Save each year as a csv file using the naming convention CMU_Buildings_[FY] for all FY 2014-2018. 
-	Import CMU_Buildings_[FY] data tables into the ArcGIS project geodatabase. 
-	Join CMU_Buildings_[FY] ( records) to the CMU_Buildings map layer (105 records).
 
**Aug. 26-Aug. 30, 2019 – Change base metric to percent change from 2017 baseline**
-	Plan which fields to include. 
  -	Building ID (all applicable)  Primary key
    -	Object ID (CMU)
    -	BL_ID (CMU)
    -	PBBID (Energy Star Portfolio Manager)
  -	Property Name (Energy Star Portfolio Manager)
      -	Public/Municipal – Cartegraph
      -	Municipal MOU Partners – 
      -	CMU – 
      -	U Pitt – 
      -	Private/Commercial – 
      -	Multi-family/residential – 
  -	Parcel ID / PIN / Map Block Lot
  -	Total CO2e emissions by year (metric tons CO2e)
      -	2017 (baseline)
      -	Etc.
  -	Change in CO2e from 2017 baseline (metric tons CO2e)
  -	Percent change in CO2e from 2017 baseline
  -	Emissions intensity (kgCO2e/ft²)
      -	2017 (baseline)
      -	Etc.
  -	Change in Emissions Intensity from 2017 baseline (kgCO2e/ft²)
  -	Percent change in Emissions Intensity from 2017 baseline (kgCO2e/ft²)
  -	Site EUI (unit)
      -	2017 (baseline)
      -	Etc.
  -	Change in Site EUI from 2017 baseline (unit?)
  -	Percent change in Site EUI from 2017 baseline
  -	Source EUI (unit?)
      -	2017 (baseline)
      -	Etc.
  -	Change in Source EUI from 2017 baseline (unit?)
  -	Percent change in Source EUI from 2017 baseline
  -	Compliance Status
  -	Area (sq ft)	
-	Create master model with external links to more complete source data (lock external sheets, but include in same master workbook)
-	Each field should link to a seminal source determined by use case [Create table]
  -	PBBID --> Energy Star Portfolio Manager (Flore created)
  -	BL_ID --> Carnegie Mellon University Facilities Management Services
  -	OBJECTID --> Allegheny County?
  -	Campus ID --> Energy Star Portfolio Manager (Flore created)?
  -	ADDRESS_1 --> Allegheny County? 
  -	ADDRESS_2  
  -	PARCEL_ID / PIN --> Allegheny County?
  -	MAP_BLOCK_LOT --> Allegheny County?
  -	Cartegraph
  -	COMPLIANCE_STATUS --> Covered Building List + Energy Star Portfolio Manager
-	Change all occurrences of “Not Available” and “N/A” in source data to “<Null>” or empty values.

**Sept. 1-4, 2018 – Add Private Building and Public MOU energy use data to Master Covered Building workbook**
-	Note: In the future, don’t bother making a master spreadsheet merging all the different categories of buildings’ energy use data. Just perform a join in ArcGIS from the individual worksheets. This avoids problems with copying and pasting from the source data files after the all years master building list has been compiled.
  -	Alternatively, run a join in ArcGIS and then export the resulting table as a excel worksheet. 
-	Remove record 6461987 (420 Blvd of the Allies) from private buildings worksheet. Entry contains only null values and is duplicated in the Public buildings category.
-	In ArcGIS, run an inner join between the MasterModel table and the 2017 and 2018 Private Building compliance status tables, respectively. This action will serve to add the PBBID and building year fields to the MasterModel table and exclude any non-duplicate records (i.e., records with data missing for either 2017 or 2018). 
-	In ArcGIS, make a copy of the PittsburghAddresses point layer. Clip layer to the CoveredBuildings2017_SpatialJoin map layer. Name the resulting layer PittsburghAddresses_Clip (1,490 records).
-	Join 2017 Covered Building List (814 records) with 2018 Covered Building List ( records). Next, join 
  -	2017 Covered Building List must be:
    -	First, Join between Covered Building List and PittsburghAddresses map layer; and then possibly also
    -	Spatial join between Covered Building List+PittAddresses Join and PittsburghParcels map layer.
    -	From there, I can join the resultant layer with PittBuildings map layer. [This might be your CoveredBuildings2017_SpatialJoin map layer.]
-	Note: For this to work, Covered Building List must match address field with PM data.

**Sept. 6-8, 2019 – Clean Address and Parcel ID fields in master spreadsheet for join**
-	Note: In order to capture the most covered buildings using the available map layers, first use Parcel ID (Pittsburgh Parcels map layer) for course grained filtering, and then use Address (Pittsburgh Addresses map layer) for fine grained filtering. Finally, use a spatial join between the Pittsburgh Buildings map layer and new Address map layer (clipped to Covered Parcels) to get a paired Covered Parcel + Covered Addresses map layer. This method will result in the most accurate set of Covered Buildings.
  -	Establish the primary key for the Covered building list. 
-	Delete record 6366514 (my test office).
Alternative Method
-	Use Google Geocoding API to geocode address field from PM data and Allegheny County Addresses map layer. Use spatial join to join both data sets’ address fields to geographic coordinates (and ultimately, building footprint). 
-	In Excel, create a linking table for both data sets’ address fields so that translation from one data set’s naming convention to the other is quick and efficient.
-	Alternatively, use Google addresses data set instead of Allegheny County data set and use Google Geocoding API to geocode straight from Portfolio Manager Data. Google Maps API Key: AIzaSyCrnbglOYmOxsDUlAGDKP81x1DheAr3Tus
-	In Excel, create a new workbook containing just the Address and Building Name fields from the MasterModel worksheet from the All_Buildings_Percent_Change_From_2017_Baseline_Test workbook. Name the new workbook PM_MasterModel_Geocode. 
-	Use the free online geocoder software BatchGeo to geocode all addresses (you’ll need to break the PM_MasterModel_Geocode data into three smaller worksheets containing 250 or less records each). Open the files and click on the gear icon in the bottom left corner of the map to export your data to Google Earth (exports as a .kml file).
-	Use the free online kml to shp conversion tool MyGeodata Converter to convert the .kml files to shapefiles (.shp).
-	In ArcGIS, import each of the geocoded addresses shapefiles into your project geodatabase. Name the map layers Batch[#]_Geocodes.
-	Use the merge tool to combine the three Batch[#]_Geocodes map layers into a single map layer called PM_Master_Geocodes (690 records). 
-	In the MasterModel spreadsheet in Excel, recalculate all the PERCENT_CHANGE fields to decimal format. 
-	Find/replace all occurrences of <Null> with empty cells.
-	Change all fields containing numbers to number fields. 
-	In ArcGIS, import that MasterModel csv file into the project geodatabase.
-	In the MasterModel table, create a new field called PERCENT_CHANGE_CO2E_NUM (type: long, numeric) and calculate field to convert PERCENT_CHANGE_CO2E from a text to numeric field. 
-	Create a new field CHANGE_TYPE_NUM (type: long, numeric) containing a 1 for PERCENT_CHANGE_CO2E_NUM > 0 and 0 for PERCENT_CHANGE_CO2E_NUM <= 0. Calculate field using the following formula:
= 1 if !PERCENT_CHANGE_CO2E_NUM! > 0 else 0
-	Create a new field CHANGE_TYPE (type: text) containing the text “decrease” for PERCENT_CHANGE_CO2E_NUM <= 0 and “increase” for PERCENT_CHANGE_CO2E_NUM > 0. Calculate field using the following formula:
= “decrease” if !PERCENT_CHANGE_CO2E_NUM! <= 0 else “increase”
-	Inner Join the PM_Master_Geocodes (690 records) with the MasterModel table (690 records) using the ObjectID and Record# fields, respectively. This action should result in 690 records. Name the resulting map layer PM_Master_Geocodes_CO2e_Join.
-	Use inner spatial join to join PM_Master_Geocodes_CO2e_Join (690 records) with PittsburghBuildings map layer ( records). This action results in 501 records. Export the new map layer to the project geodatabase as PM_Master_Geocodes_CO2e_Join. 
-	Add the following definition queries to PM_Master_Geocodes_CO2e_Join. This action results in 340 remaining records.
  -	PERCENT_CHANGE_CO2e is not null; and
  -	PERCENT_CHANGE_CO2e is less than 6428.72; and
  -	PERCENT_CHANGE_CO2e is not equal to 1; and
  -	PERCENT_CHANGE_CO2e is not equal to -1.
-	Use Summarize Within to aggregate records up to the building level (PBBID?).

**Sept. 8, 2019 – Add Master Covered Building data set to the Mapbox Style**
-	In ArcGIS, create a copy of PM_Master_Geocodes_CO2e_Join and remove all definition queries. This action should result in 501 records. Export the layer to the project geodatabase as Master_PM_Geocodes_CO2e. 
-	Rename the PM_Master_Geocodes_CO2e_Join map layer Master_PM_C02e_PerChange.
-	Create a copy of the Master_PM_C02e_PerChange map layer. 
-	Use the Feature to JSON tool to convert the Master_PM_C02e, No_2018_Submission, Null_Values, and Master_PM_Geocodes map layers to GeoJSON files. Make sure the check the box for Project to WGS_1984.
-	In Mapbox, add the newly created GeoJSON files as new data sets. Export data sets as tiles maintaining all the original file names.
-	Create a new Light Style. Add all the newly created tiles.

**Sept. 21, 2019 – Create Benchmarking Data Workflow Guide Sheet**
-	Create a Benchmarking Data Workflow Guide Sheet, including Data Creation and Processing Protocol.

**Oct. 2, 2019 – Add HTML file creation and GitHub Pages initialization instructions to Data Workflow Guide Sheet**
-	Add instructions for HTML file creation with JS Fiddle and site initialization with GitHub and GitHub Pages. 

**Oct. 4, 2019 – Create Task in ArcGIS Pro to encode project workflow**
- Tutorials and examples
  -	https://pro.arcgis.com/en/pro-app/help/tasks/create-a-simple-task.htm
  -	http://proceedings.esri.com/library/userconf/fed17/papers/fed_35.pdf

**Oct. 9, 2019 – Correct records and update Mapbox Style**
-	The energy data is correct for each record, i.e., the PM data is properly matched to the building ID and address. The problem seems to have happened when I joined the master PM data table to the geocode map layer. The geocode map layer was created by importing the 750 or so records from the master PM data into a geocoder and generating XY coordinates, then converting those into a master shapefile (point layer)
 
*FLAGS*
- PBBID only unique identifier for energy data. No direct way to link this identifier to the building footprint layer in GIS. 
  -	PBBID assigned to address field in Portfolio Manager?
  -	Building footprints share one-to-many relationship with addresses
  -	Parcels share a many-to-many relationship with Building footprints
  -	Building footprints share a one-to-many relationship with addresses
- There’s no simple way (that I know of) to get the energy data from the parcels layer to the buildings layer to achieve the desired extrusion effect (we don’t want to extrude the parcels). The solution might be to manually add the parcel data to the building footprint data (watching to avoid many-to-one relationships between the building and parcels layers) and then joining the energy data to the buildings data using the Parcel ID field. 
  -	This would likely have to be a spatial join rather than a regular join, since the two layers don’t share any attributes in common (not address, not building ID, not Parcel ID).
  -	See http://desktop.arcgis.com/en/arcmap/10.3/manage-data/tables/about-joining-and-relating-tables.htm for help
    -	Open to Spatial Join tool
    -	Set Targets Features to “PittsburghBuildings_PBBID_Clip”
    -	Set Join Features to “PittsburghParcels_PBBID_Clip”
    -	For Output Feature Class, type “PittsburghBuildings_Energy_Spatial_Join”
    -	For Join Operation, select “Join one to many”. 
    -	Keep the box checked for “Keep all target features” (outer join default). 
    -	For Match Option, select “Intersect”
    -	For Field map of join features, select… (incomplete)
  -	The operation above increased the number of records from 1,010 to 1,505. This may reflect the many-to-one join operation found certain parcels containing multiple buildings. We want our final data table to contain the same number of records as we have building footprints, not building-parcel combinations.
  -	The operation above also resulted in mostly null values for all the important energy use and performance attributes. Need to be more careful with the joins to preserve the relevant data sets through every step.
    -	Goal: # of records in final data layer = # of unique PBBIDs in Portfolio Manager data (93 records)
    -	First join: Energy data table (93 records) to Compliance data table (926 records)  Yields new data table “ComplianceEnergyJoin”
      -	Outer join = 980 records 😊 
      -	Inner join = 93- records ☹
    -	Second join: “EnergyComplianceJoin” data table (980 records) to PittsburghParcel map layer (628 records)  Yields new map layer “PittsburghParcels_PBBID_Clip”
      -	Outer Join = 628 records ☹
      -	Inner join = ?? records 😊 
    -	Third join: Spatial join between “PittsburghParcels_PBBID_Clip” (628 records) and “PittsburghBuildings_PBBID_Clip” (1010 records)  Yields new data table “” 
      - Outer join = ?? records
      -	Inner join = ?? records
- Address field in two data tables not formatted uniformly
  -	Concatenation not a perfect fix because of:
    -	Differences in capitalization
    -	Some records encompass multiple street numbers (e.g., 435-460; 2400 2500; etc.)
- Does Energy Star Portfolio Manager platform interface with Access?
- Does ArcGIS interface with Access?
  -	Import Access database to ArcGIS? 
  -	Export to Excel, save as .csv, then import to ArcGIS?
- What data format do we need to support query function in map interface?
  -	Access allows queries, Excel doesn’t
  -	ArcGIS allows queries by filter only
  -	Search bar?
- What kind of values do we want for null entries in ArcGIS (per field)?
  -	Empty (null)
  -	NA
- Which functions are executable in Mapbox, which require other software? How do we combine Mapbox features and non-Mapbox features in our public map interface?
  -	Use source code from City Energy Project (see https://github.com/cityenergyproject/seattle)
 	
