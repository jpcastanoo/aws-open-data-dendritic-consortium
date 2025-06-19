# Tutorial: Download and Visualize Dendritic Consortium Data

This tutorial demonstrates how to download and visualize public data from the Dendritic Consortium dataset stored on AWS S3 using the AWS CLI and Python.

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

## Visualizing a TIFF Image

The following example downloads and visualizes a TIFF image from our public S3 bucket using Python. 

```python
import boto3
from botocore import UNSIGNED
from botocore.client import Config
import tifffile
import matplotlib.pyplot as plt
from io import BytesIO

s3 = boto3.client('s3', config=Config(signature_version=UNSIGNED))
key = 'single_sample_image.tif'
response = s3.get_object(Bucket='dendriticconsortium', Key=key)
img = tifffile.imread(BytesIO(response['Body'].read()))

plt.imshow(img, cmap='gray')
plt.axis('off')
plt.show()
```
![Sample Voltage Imaging](tutorials/01_access_data_from_s3/single_sample_image.png)

## Visualizing a electrophysiological data
```
import boto3
from botocore import UNSIGNED
from botocore.client import Config
import pandas as pd
import matplotlib.pyplot as plt
from io import BytesIO

s3 = boto3.client('s3', config=Config(signature_version=UNSIGNED))
key = 'sample_ephys_recording.csv'  # Cambia esto al nombre real del archivo
response = s3.get_object(Bucket='dendriticconsortium', Key=key)
data = pd.read_csv(BytesIO(response['Body'].read()))

plt.plot(data['time'], data['voltage'], color='blue')
plt.xlabel('Time (ms)')
plt.ylabel('Voltage (mV)')
plt.title('Electrophysiology Recording')
plt.grid(True)
plt.tight_layout()
plt.show()
```
