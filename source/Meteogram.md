# Meteogram

In this example we describe how to plot the hourly evolution of 2-m temperature and precipitation for a given place. 

```python
import xarray as xr
import h5netcdf
import datetime
import s3fs
import cartopy.crs as ccrs
import matplotlib.pyplot as plt
```

We define the forecast initialization date, latitude and longitude of interest: 

```python
latitude = -40
longitude = -50

start_year = 2022
start_month = 3
start_day = 21
start_hour = 0
```

We read the forecast :

```python
START_DATE = datetime.datetime(start_year, start_month, start_day, start_hour)

fs = s3fs.S3FileSystem(anon=True)

files = fs.glob(f'smn-ar-wrf/DATA/WRF/DET/{FECHA_INI:%Y/%m/%d/%H}/WRFDETAR_01H_{FECHA_INI:%Y%m%d_%H}_*.nc')

ds_list = []
for s3_file in files:
    print(s3_file)
    f = fs.open(s3_file)
    ds_tmp = xr.open_dataset(f, decode_coords = 'all', engine = 'h5netcdf')
    ds_list.append(ds_tmp)

ds = xr.combine_by_coords(ds_list, combine_attrs = 'drop_conflicts')
```

```python
# Searching the closest gridpoint to the selected lat-lon 
data_crs = ccrs.LambertConformal(central_longitude = ds.CEN_LON, 
                                 central_latitude = ds.CEN_LAT, 
                                 standard_parallels = (ds.TRUELAT1, ds.TRUELAT2))
x, y = data_crs.transform_point(longitude, latitude, src_crs=ccrs.PlateCarree())

# Extraction of the value at the chosen gridpoint
pronostico = ds.sel(dict(x = x, y = y), method = 'nearest')

# Se obtiene la serie de temperatura a 2 m, precipitación acumulada y de fechas
T2 = pronostico['T2']
PP = pronostico['PP']
fechas = pronostico['time']

# Inicio la figura
fig, ax = plt.subplots(figsize = (10, 8))
# Duplico el eje x
ax2 = ax.twinx()
# Grafico la precipitación en barras
ax.bar(fechas, PP, color = 'blue', width = 0.03, label = 'Precip. Acum.')
# Grafico la tempertura con una linea
ax2.plot(fechas, T2, color = 'red', label = 'Temp. 2 m', linewidth = 3)
# Defino las etiquetas de los ejes
ax.set_xlabel('Fecha')
ax2.set_ylabel('T 2m (°C)')
ax.set_ylabel('PP (mm)')
# Defino el título de la figura
plt.title(f'Temperatura a 2 m y precipitacion acumulada \n lat = {latitud:0.2f}, lon = {longitud:0.2f}')
# Grafico la leyenda
fig.legend(loc = 'upper right')
# Ajusto el gráfico al tamaño de la figura
plt.tight_layout()
```
    
![png](../figuras/fig_meteograma.png)
    
Para descargar la notebook acceder al siguiente [link](../notebooks/Meteograma.ipynb)
