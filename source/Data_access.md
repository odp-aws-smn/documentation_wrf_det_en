# Data access

Data are available at the **AWS portal**: [https://registry.opendata.aws/smn-ar-wrf/](https://registry.opendata.aws/smn-ar-wrf/)

Downloading can be carried out in different ways:

**URL adress**<br />
Files can be download by simply going to the following link: [https://smn-ar-wrf.s3-us-west-2.amazonaws.com/index.html](https://smn-ar-wrf.s3-us-west-2.amazonaws.com/index.html)

**AWS CLI**<br /> 
This procedure makes use of routines proper to AWS. For more information regarding their use visit the following [link](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).<br />
Here, we present two examples, to download an individual file and to download files from an entire directory:  <br />
```bash
#!/usr/bin/env bash

# to download the file with the second forecast hour from the 00 UTC cycle for March 21, 2022 to the output_path: 
aws s3 cp --no-sign-request s3://smn-ar-wrf/DATA/WRF/DET/2022/03/21/00/WRFDETAR_01H_20220321_00_002.nc output_path

# to download all forecast times for the 00 UTC cycle for March 21, 2022 to the output_path:
aws s3 cp --no-sign-request s3://smn-ar-wrf/DATA/WRF/DET/2022/03/21/00/ --recursive output_path
```

**Python**<br />
This can be done using the library [s3sf](https://pypi.org/project/s3fs/). <br />
For example, to download an individual file we may write: <br />
```python
import s3fs
# to download the file with the second forecast hour from the 00 UTC cycle for March 21, 2022
s3_file = 's3://smn-ar-wrf/DATA/WRF/DET/2022/03/21/00/WRFDETAR_01H_20220321_00_002.nc'
fs = s3fs.S3FileSystem(anon=True)
data = fs.get(s3_file)
```
