# Data format

Files follow a format much used to organize multi-dimensional scientific data, the **NetCDF** (Network Common Data Form). In particular, this data follow the [CF](http://cfconventions.org/) convention. For more information on this format see this [link](https://docs.unidata.ucar.edu/netcdf-c/current/index.html).

**Map projection:** <br />
Model grid is represented in a [*Lambert conformal*](https://www2.mmm.ucar.edu/wrf/users/docs/user_guide_V3/user_guide_V3.9/users_guide_chap3.html)  projection. The center of the model grid is located at -35° latitude and -65° longitude, and the spatial resolution is approximately 4 km.

**Dimensions:**<br />
|Dimension   |Value   |
|---|---|
| time  |1   |
|y   |1249   |
|x   |999   |

**Variables:**<br />
|Variable   |Description   |Unit   |Precision   |
|---|---|---|---|
|PP   |Accumulated precipitation in a given time period   |mm   |float32   |
|HR2   |2-meter relative humidity   |%   |float32   |
|T2   |2-meter temperature (\*)   |°C   |float32   |
|dirViento10   |10-meter wind direction    |°   |float32   |
|magViento10   |10-meter wind speed (\*)   |m/s   |float32   |
|Tmax   |Daily maximum temperature (\*)   |°C   |float32   |
|Tmin   |Daily minimum temperature (\*)   |°C   |float32   |

(\*) Variables debiased using surface observations. For more information about the methodology see [Cutraro y otros, 2020](http://hdl.handle.net/20.500.12160/1405). In case of failure in the debiasing procedure, raw data will be presented instead.

For the minimum temperature (Tmin) of a given day, the value corresponds to a temperature registered between 00 and 12Z. For the maximum temperature (Tmax) of a given day, the value corresponds to a temperature registered between 12Z and 00Z of the following day.

For example, the file WRFDETAR_24H_20220314_00_001.nc includes data from the 00Z forecasting cycle for the first forecast plazo  (first day) and contains the forecast minimum temperature for day 20220315 between 00Z and 12Z, while forecast maximum temperature for the same day will be found between 12Z and 00Z of the following day.

Por ejemplo, el archivo WRFDETAR_24H_20220314_00_001.nc que contiene los datos del ciclo 00Z para el primer plazo de pronóstico (1° día) tendrá la temperatura mínima pronosticada para el día 20220315 entre las 00Z y las 12Z y la temperatura máxima pronosticada para el día 20220315 entre las 12Z y las 00Z del día siguiente.

Para el caso de la PP válida para el día X en el plazo P, el valor corresponde a la precipitación acumulada pronosticada entre el plazo P-1 y P.

Por ejemplo, el archivo WRFDETAR_01H_20220314_00_036.nc que contiene los datos del ciclo 00Z para el plazo 36 de pronóstico tendrá la precipitación acumulada pronosticada válida para 20220315 entre las 11Z y las 12Z.

**Variables de coordenadas:**<br />
|Variable   |Descripción   |Unidad   |Precisión   |
|---|---|---|---|
|time   |Tiempo   |Horas desde el inicio del ciclo de pronóstico   |int   |
|y   |Coordenada y   |Metros desde el centro de la proyección   |float32   |
|x   |Coordenada x   |Metros desde el centro de la proyección   |float32   |
|lat   |Latitud   |° (convención entre 90° y -90°)   |float32   |
|lon   |Longitud   |° (convención entre -180° y 180°)   |float32   |




