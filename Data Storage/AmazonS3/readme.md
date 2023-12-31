
# Amazon S3 Overview

## Public Bucket

### Overview
Amazon S3 allows the creation of publicly accessible buckets with customizable access controls.

### Customizing Access
1. **ACL (Access Control List):** Manage bucket access through ACL settings.
2. **Bucket Policy:** Define custom policies to control access permissions.

### S3 Policy Generator
Create and customize policies using the [Amazon S3 Policy Generator](http://awspolicygen.s3.amazonaws.com/policygen.html).

## Lifecycle Bucket

### Overview
Amazon S3 supports a lifecycle model for managing object storage classes.

### Storage Classes
1. **S3 Standard:** Default storage class with low-latency and high-throughput.
2. **S3 Standard-IA:** Infrequent access storage with cost savings.
3. **S3 Intelligent-Tiering:** Automatically adjusts object storage class based on access patterns.
4. **S3 One Zone-IA:** Cost-effective storage in a single availability zone.
5. **S3 Glacier:** Archive storage with retrieval times from minutes to hours.
6. **S3 Glacier Deep Archive:** Lowest-cost archival storage.

### Lifecycle Management
Automate object transition between storage classes using the S3 Management Console.


### Access S3 via boto3 in Python
1.	**Pip install boto3**
2.	**Vim s3_list.py**

#### Credentials 만드는법
* Mkdir ~/.aws
* Vim ~/.aws/config

```ubuntu
setting a region
[default]
Region = ap-northeast
```
* vim ~/.aws/credentials
```ubuntu
[default]
Aws_access_key_id = “~~~”
Aws_secret_access_key = “~~”
아래와 같은 방법으로 확인 가능
cat ~/.aws/config
cat ~/.aws/credentials 
```

### S3에 잇는 bucket name 출력

```python
import boto3
session = boto3.Session(profile_name = 'default') #aws 파일에 있는 profile name
s3 = session.resource('s3')
for bucket in s3.buckets.all():
    print(bucket.name)
```
### S3에 있는 파일 가져오기
```python
import os
import boto3
import time

bucket_name = "jongjun"
folder_name = "2023/"
path = "Cover letter.pdf"
session = boto3.Session(profile_name = 'default')
s3 = session.client('s3')
print(folder_name + os.path.basename(path))
s3.download_file(bucket_name, folder_name + os.path.basename(path), "./" + os.path.basename(path))
```

### S3에 파일 upload
```python
import os
import boto3
import time

bucket_name = "jongjun"
file_name = "Cover letter.pdf"
local_file_path = os.getcwd() + "/" + file_name
target_file_name = "temp_cover.pdf"
session = boto3.Session(profile_name = 'default')
s3 = session.client('s3')

s3.upload_file(local_file_path, bucket_name, target_file_name)
```
                                         
### S3에 있는 file public으로 설정하기

```python
import os
import boto3
import time

bucket_name = "jongjun"
target_file_name = "temp_cover.pdf"

session = boto3.Session(profile_name = 'default')
s3 = session.client('s3')
s3.put_object_acl(ACL = 'public-read', Bucket = bucket_name, Key=target_file_name)
```

### AWS Lambda service
* Severless, event-driven compute service that lets you run code for virtually any type of application or backend service without provisioning or managing servers.
* You can trigger Lambda from over 200 AWS services and SaaS, and only pay for what you use.
* 서버리스란 개발자가 서버를 관리할 필요 없이 애플리케이션을 빌드하고 실행할 수 있도록 하는 클라우드 네이티브 개발 모델이다
* 코드를 계속 실행시키기 보다는 특정한 시기에만 실행시키는 경우에 Lambda를 사용하면 유용하다.
*	서버 띄우지 않고 간단한 코드를 실행시키고 싶은 경우
*	특정 기간 또는 특정 주기로 코드를 실행시켜야 하는 경우
*	트리거가 실행될때만 코드를 실행시키고 싶은 경우



