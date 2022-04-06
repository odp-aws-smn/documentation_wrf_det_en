# Data structure

La estructura de directorios y nombres de archivos es la siguiente: 

/DATA/WRF/{scheme}/{year}/{month}/{day}/{cycle}/WRFDETAR_{frequency}H_{year}{month}{day}\_{cycle}_{plazo}.nc

Where fields between curly brackets are defined as: <br />

{scheme} = 3 capital letters indicate the scheme used, either deteriministic or ensemble (DET o ENS) <br />
{year} = 4-dígit number <br />
{month} = 2-dígit number <br />
{day} = 2-dígit number <br />
{cycle} = 2-dígit number indicating the model run <br />
{frequency} = 2-dígit number indicating the data frequency. At the moment only 01H and 24H are available. <br />
{plazo} = 3-dígit number for lead time.

Examples:
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_01H_20220314_00_000.nc
* /DATA/WRF/DET/2022/03/14/00/WRFDETAR_24H_20220314_00_000.nc
