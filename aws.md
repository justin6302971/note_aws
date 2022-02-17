``` bash

# setup credentials
aws configure list-profiles

# cp bucket files to local
aws s3 cp <remote_bucket_dir_path> <local_dir_path> --recursive
# remote_bucket_dir_path sample:  s3://dev-email-store/logs/

#cp bucket files  with certain profile and file name filters
aws s3 cp <remote_bucket_file_path> <local_dir_path> --recursive --exclude "*" --include "structuredLog-*" --recursive  --profile log-bucket 
# remote_bucket_file_path sample: s3://dev-koobits-log-store/logs/structuredLog.json

# list bucket files
aws s3 ls <remote_bucket_dir_path>

# remove bucket files
aws s3 rm <remote_bucket_dir_path> --recursive    

```