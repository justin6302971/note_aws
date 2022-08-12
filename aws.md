

## linux
``` bash
# get system version
uname -v


sudo du -x / | sort -n | tail -40

#du shows the disk usage of files, folders, etc. in the default kilobyte size

 #shows disk usage in human-readable format for all directories and subdirectories
du -h
#  shows disk usage for all files
du -a

#provides total disk space used by a particular file or directory
du -s 

 # https://www.tecmint.com/commands-to-collect-system-and-hardware-information-in-linux/

#installed docker and check running container counts
docker ps -q | wc -l

# linux server for ecs
 ssh -i "server.pem" <ip>


```

## profile
``` bash

aws configure --profile <profile_name>

# setup credentials
aws configure list-profiles

# https://support.huaweicloud.com/intl/en-us/trouble-ecs/ecs_trouble_0352.html

```

## s3
``` bash

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

## dynamodb
``` bash

# check table locally
aws dynamodb list-tables --endpoint-url http://localhost:8000

```

## ec2

``` bash

aws ec2 describe-instances --filters "Name=tag:Name,Values=<name>" --profile <profile>


aws ec2 start-instances --instance-ids <id1> <id2> --profile <profile>

aws ec2 stop-instances --instance-ids <id1> <id2> --profile <profile>

aws ec2  reboot-instances --instance-ids <id1> <id2> --profile <profile_name>
```

## ecs
``` bash

aws ecs describe-container-instances --cluster <cluster_name> --container-instances <container_instance_id>  --profile <profile_name>

aws ecs list-container-instances --cluster <cluster_name>--profile <profile_name>

aws ecs describe-services --cluster <cluster_name> --service <service_name> --profile <profile_name>

aws ecs list-task-definitions --family-prefix <task_def_family_name> --sort DESC --status ACTIVE --profile <profile_name>

aws ecs describe-task-definition --task-definition <task_def_name>  --profile <profile_name>


aws ecs register-task-definition --family koob_schedule_pc_process_archive_pc \
--container-definitions "[{\"name\":\"containername\",\"logConfiguration\":{\"logDriver\":\"awslogs\",\"options\":{\"awslogs-group\":\"/groupname\",\"awslogs-region\":\"ap-southeast-1\",\"awslogs-stream-prefix\":\"ecs\"}},\"image\":\"repositoryname\",\"cpu\":0,\"memory\":256,\"essential\":true}]" \
--task-role-arn "arn:aws:iam::111111111:role/testRole" \
--profile <profile_name>

aws ecs list-tasks --cluster <cluster_name> --profile <profile_name>

aws ecs stop-task  --cluster <cluster_name> --task <task_id>  --profile <profile_name>

aws ecs update-service --cluster  <cluster_name> --service  <servuce_name> --desired-count 1  --profile <profile_name>

```

## ecr
```bash
aws ecr describe-registry --profile <profile_name>

aws ecr describe-repositories --profile <profile_name>
```
## iam
```
aws iam list-roles --path-prefix  ecsTaskExecutionRole  --profile <profile_name>

aws iam list-roles   --query 'Roles[*].RoleName'   --output text  --profile <profile_name>
```


## ssm 
``` bash
aws ssm get-parameters --name "/name" --profile <profile_name>

aws ssm describe-parameters --profile <profile_name>

aws ssm delete-parameter --name "/name" --profile <profile_name>


aws ssm put-parameter \
    --name "/name" \
    --value "testvalue" \
    --type "SecureString" \
    --profile <profile_name> \
    --overwrite
```


## logs
```bash

aws logs create-log-group  \
--log-group-name "/ecs/groupname"  \
--profile <profile_name>

aws logs describe-log-groups --log-group-name-prefix "/ecs/groupname"   --profile <profile_name>
aws logs describe-log-streams --log-group-name "/ecs/groupname"   --max-items 5  --profile <profile_name>



aws logs get-log-events \
--log-group-name  "/ecs/groupname" \
--log-stream-name "ecs/groupstreamname" \
--profile <profile_name>

```

## references
1. [official doc](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)