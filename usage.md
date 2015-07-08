
Potential Usage examples:

Data Units
---
The initial build has TSV data in their SI/database units: elev and stage (m), flow (cms), precip (mm), storage (m3)

Location metadata (elevation) is in feet. (i.e. the elevation of UVD is 420' MSL.

Timeseries Query
--
in-progress functionality is to build out the startdt and enddt variables. Future 
{
  "timeseries" : [["tsid1","units1","interval1"], ["tsid2","units2","interval2"], ["tsid3","units3","interval3"]],
  "p_base_parameter_id": ["Elev","Flow","Stage","Stor","Precip"]
  "back": "ISO-8601", //referenced from enddt, or datetime.now() if nothing specified. Valid values are 1d-7d.
  }

getjson?timeseries=[["CHJ Q","cfs","Daily"], ["CHJ.Flow.Inst.1Day.0.CBT-REV","kcfs"], ["12437990 00060","cfs"]]

General Abstract Query
--
General abstract queries allow the end user to provide keywords. The service will return hydroJSON timeseries objects with the data they want.

getjson?query=["CHJ Avg Day Flow", "ANAW Temp"]

User can provide a list of queries. Each Query string performs an intersect operation. The result is a union of each query string.

getjson?query=["CHJ Daily Avg Flow", "ANAW Temp"]

Catalog Query
--
getjson?catalog=["CHJ Daily Avg Flow"]

Most Recent Value Query
--
getjson?mostrecent=[["12437990",  "cfs"]]

units and interval are optional parameters
TODO: Include specification for default units, DECODES spec will be used as an inital cut (Ktarbet)

Reference Implementation
---
DB -> ETL -> (SQLITE) -> Reference implementation (USACE/USBR)
