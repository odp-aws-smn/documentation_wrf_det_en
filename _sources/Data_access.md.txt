# Data access

Data are available at the **AWS portal**: <a href="https://registry.opendata.aws/smn-ar-wrf/" target="_blank">https://registry.opendata.aws/smn-ar-wrf/</a>.

Downloading can be carried out in different ways:

**URL adress**<br />
Files can be download by simply going to the following link: <a href="https://smn-ar-wrf.s3-us-west-2.amazonaws.com/index.html" target="_blank">https://smn-ar-wrf.s3-us-west-2.amazonaws.com/index.html</a>.<br />
Data are stored using the Amazon Simple Storage Service (S3). For more information about this tool visit <a href="https://docs.aws.amazon.com/es_es/AmazonS3/latest/userguide/Welcome.html" target="_blank">https://docs.aws.amazon.com/es_es/AmazonS3/latest/userguide/Welcome.html</a>.

**AWS CLI**<br /> 
This procedure makes use of routines proper to the tool AWS Command Line Interface (CLI). For more information regarding their use visit the following <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" target="_blank">link</a>.<br />
Here, we present two examples, to download an individual file and to download files from an entire directory:  <br />
```bash
#!/usr/bin/env bash

# to download the file with the second forecast hour from the 00 UTC cycle for March 21, 2022 to the output_path: 
aws s3 cp --no-sign-request s3://smn-ar-wrf/DATA/WRF/DET/2022/03/21/00/WRFDETAR_01H_20220321_00_002.nc output_path

# to download all forecast times for the 00 UTC cycle for March 21, 2022 to the output_path:
aws s3 cp --no-sign-request s3://smn-ar-wrf/DATA/WRF/DET/2022/03/21/00/ --recursive output_path
```

**Python**<br />
This can be done using the library <a href="https://pypi.org/project/s3fs/" target="_blank">s3sf</a>. <br />
For example, to download an individual file we may write: <br />
```python
import s3fs
# to download the file with the second forecast hour from the 00 UTC cycle for March 21, 2022
s3_file = 's3://smn-ar-wrf/DATA/WRF/DET/2022/03/21/00/WRFDETAR_01H_20220321_00_002.nc'
fs = s3fs.S3FileSystem(anon=True)
data = fs.get(s3_file)
```

**R**<br />
This can be done using the library <a href="https://cran.r-project.org/web/packages/aws.s3/index.html" target="_blank">aws.s3</a>. <br />
For example, to download all the files for 1 day: 
```R
library("aws.s3")
 
# Define the function wrf.download to download the files
wrf.download <- function(wrf.name = wrf.name){
      save_object(
      object = paste0(wrf.name),
      bucket = "s3://smn-ar-wrf/",
      region = "us-west-2",
      file = substring(wrf.name, 28),
      overwrite = TRUE)}

# Define the date of the data
anual = 2022
mes = 9
dia = 3
ciclo = 0
time = "01H"   # Frequency of the forecast of interest 01H or 24H (string format) 

# The input date is converted to string
anual <- sprintf("%04d", anual)
mes <- sprintf("%02d", mes)
dia <- sprintf("%02d", dia)
ciclo <- sprintf("%02d", ciclo)
 
# The names of the files are defined
wrf.names <- get_bucket_df(
    bucket = "s3://smn-ar-wrf/",
    prefix = paste0("DATA/WRF/DET/", anual, "/", mes, "/", dia, "/", ciclo),
    max = Inf,
    region = "us-west-2")
 
wrf.names.rows <- which(grepl(time, wrf.names$Key, fixed = TRUE) == TRUE)
wrf.names <- wrf.names[wrf.names.rows, ]
 
# We run the función wrf.download 
lapply(wrf.names$Key, FUN = wrf.download)

```
