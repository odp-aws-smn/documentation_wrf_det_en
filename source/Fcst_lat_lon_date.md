# Forecast for a given latitude, longitude and date

In this example we show how to obtain the forecast of a specific variable (2-meter temperature for example) for a given latitude, longitude and date.


```python
# We import the necessary libraries
import xarray as xr
import h5netcdf
import datetime
import s3fs
import cartopy.crs as ccrs
```

We define the starting date of the forecast, the desired forecast time, latitude and longitude (March 21, 2022 00 UTC; March 22, 2022 17 UTC; -25; -70):


```python
latitude = -25
longitude = -70

start_year = 2022
start_month = 3
start_day = 21
start_hour = 0

fcst_year = 2022
fcst_month = 3
fcst_day = 22
fcst_hour = 17
```

We define the variable to plot:


```python
var = 'T2'
```

We read the file containing the information we are looking for:


```python
START_DATE = datetime.datetime(start_year, start_month, start_day, start_hour)
FCST_DATE = datetime.datetime(fcst_year, fcst_month, fcst_day, fcst_hour)

# Getting the forecast lead time:
lead_time = int((FCST_DATE - START_DATE).total_seconds()/3600)

s3_file = f'smn-ar-wrf/DATA/WRF/DET/{START_DATE:%Y/%m/%d/%H}/WRFDETAR_01H_{START_DATE:%Y%m%d_%H}_{lead_time:03d}.nc'

fs = s3fs.S3FileSystem(anon=True)

if fs.exists(s3_file):
    f = fs.open(s3_file)
    ds = xr.open_dataset(f, decode_coords = 'all', engine = 'h5netcdf')
else:
    print('The file does not exist')
```


We get the appropriate forecast value:


```python
# Searching the closest gridpoint to the selected lat-lon 
data_crs = ccrs.LambertConformal(central_longitude = ds.CEN_LON, 
                                 central_latitude = ds.CEN_LAT, 
                                 standard_parallels = (ds.TRUELAT1, ds.TRUELAT2))
x, y = data_crs.transform_point(longitude, latitude, src_crs=ccrs.PlateCarree())

# Extraction of the value at the chosen gridpoint
forecast = ds.sel(dict(x = x, y = y, time = FCST_DATE), method = 'nearest')[var]

print(f'The forecast value for the variable {var} at latitude {latitude} and longitude {longitude} is: {forecast.values:0.2f}')
```

    The forecast value for the variable T2 at latitude -25 and longitude -70 is: 27.21

To download this notebook visit the following [link](../notebooks/Fcst_lat_lon_date.ipynb)

