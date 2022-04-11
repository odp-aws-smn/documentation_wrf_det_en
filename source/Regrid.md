# Interpolation to a regular grid 

We  show an example of how to transform a dataset that is in a Lambert conformal projection to a regular grid (equirectangular projection).


```python
# We import the necesssary libraries
import xarray as xr
import h5netcdf
import datetime
import s3fs
import xesmf as xe
```

We define the forecast initialization date and the desired forecast time:



```python
start_year = 2022
start_month = 3
start_day = 21
start_hour = 0

fcst_year = 2022
fcst_month = 3
fcst_day = 21
fcst_hour = 17
```

We read the file containing the information we are looking for:


```python
FCST_DATE = datetime.datetime(start_year, start_month, start_day, start_hour)
START_DATE = datetime.datetime(start_year, start_month, start_day, start_hour)

# Getting the forecast lead time:
leadtime = int((FCST_DATE - START_DATE).total_seconds()/3600)

s3_file = f'smn-ar-wrf/DATA/WRF/DET/{START_DATE:%Y/%m/%d/%H}/WRFDETAR_01H_{START_DATE:%Y%m%d_%H}_{leadtime:03d}.nc'

fs = s3fs.S3FileSystem(anon=True)

if fs.exists(s3_file):
    f = fs.open(s3_file)
    ds = xr.open_dataset(f, decode_coords = 'all', engine = 'h5netcdf')
else:
    print('The file does not exist')
```

We define the target regular grid:


```python
resolution_lat = 0.1
resolution_lon = 0.1
lat_min = -56
lat_max = -19
lon_min = -76
lon_max = -48

new_grid = xe.util.grid_2d(lon_min - resolution_lon/2, lon_max, resolution_lon, 
                           lat_min - resolution_lat/2, lat_max, resolution_lat)

```

Interpolation procedure:


```python
regridder = xe.Regridder(ds, new_grid, 'bilinear')
ds_interpolated = regridder(ds, keep_attrs = True)
```
