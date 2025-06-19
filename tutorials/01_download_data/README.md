# Tutorial: Download Dendritic Consortium Data

This tutorial demonstrates how to download public data from the Dendritic Consortium dataset stored on AWS S3 using the AWS CLI and Python.

## Downloading a file

This example downloads a TIFF file from our public S3 bucket and saves it to your current directory using Python. Be sure to install the required Python packages:

```
pip install boto3 tifffile matplotlib pandas
```

```python
import boto3
from botocore import UNSIGNED
from botocore.client import Config

s3 = boto3.client('s3', config=Config(signature_version=UNSIGNED))
bucket = 'dendriticconsortium'
key = 'single_sample_image.tif'
filename = key

s3.download_file(bucket, key, filename)
print(f'Download complete: {filename}')
```

Or using AWS CLI:
```
aws s3 cp s3://dendriticconsortium/single_sample_image.tif . --no-sign-request
```