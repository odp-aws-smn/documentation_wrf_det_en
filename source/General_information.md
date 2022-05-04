# General information

The SMN-Arg operationally runs the high-resolution Weather Research and Forecasting (WRF) model for its main weather forecast activities. The version in use now is 4.0 and utilizes the dynamical kernel Advanced Research WRF (ARW) (<a href="https://www2.mmm.ucar.edu/wrf/users/docs/technote/v4_technote.pdf" target="_blank">Skamarock et al., 2019</a>). The model runs with explicitly resolved convection, variable time step and was configured using the following parameterizations: <br />

- Microphysics: WSM6 (one momento - 6 classes)
- Longwave radiation: RRTM
- Shortwave radiation: Dudhia
- Planetary boundary layer: MYJ (Mellor, Yamada, Janjic)
- Land surface model: 4-layer NOAH (0-10 cm, 10-40 cm, 40-100 cm, 1-2 m)

Our 72-h forecasts are set to a 4-km horizontal resolution and 45 vertical levels, with a top level at 10 hPa. Initial and hourly boundary conditions are taken from NCEP-NOAA Global Forecasting System Model (<a href="https://www.emc.ncep.noaa.gov/emc/pages/numerical_forecast_systems/gfs.php" target="_blank">GFS</a>) at 0.25° horizontal resolution. <br />

The domain of the forecast is defined in a Lambert conformal projection and is shown below: <br />

![png](../figuras/dominioWRF4.png)  <br /> *WRF-Arg domain*

More details about the model configuration can be found in this <a href="http://repositorio.smn.gob.ar/handle/20.500.12160/1402" target="_blank">link</a>.
