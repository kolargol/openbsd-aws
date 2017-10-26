# AWS-OpenBSD

AWS playground for OpenBSD kids.

Running whatever is in this repo will propably end up destroying a kitten factory.


## Prerequisites

* shell access to OpenBSD with internet connection available.
* minimum 12GB free space of /tmp (8GB for disk image and ~4GB for temporary files).
* curl, ec2-api-tools, awscli and vmdktool packages installed.
* shell environment variables available.

    export AWS_ACCESS_KEY_ID=YOUR_AWS_ACCES_KEY;  
    export AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_KEY;  

* Identity and Access Management on AWS configured.

> YOUR_AWS_ACCES_KEY and YOUR_AWS_SECRET_KEY should have AmazonEC2FullAccess and AmazonS3FullAccess policies assigned.


## Script usage

```shell
create-ami.sh [-dinsr]
    -d "description"
    -i "/path/to/image"
    -n only create the RAW/VMDK images (not the AMI)
    -r "release (e.g 6.0; default to current)"
```


## References
http://blog.d2-si.fr/2016/02/15/openbsd-on-aws/


#### Quick build

Install required packages
```shell
pkg_add curl ec2-api-tools awscli vmdktool;
```

Prepare your environment.
```shell
export AWS_ACCESS_KEY_ID=000_YOUR_AWS_ACCESS_KEY_HERE;
export AWS_SECRET_ACCESS_KEY=000_AWS_SECRET_KEY_HERE;
export AWS_REGION=eu-central-1;
export MIRROR=http://mirror.switch.ch/ftp/pub/OpenBSD
```

Build and upload your image.
```shell
curl -sS -O https://raw.githubusercontent.com/kolargol/openbsd-aws/master/create-ami.sh;
ksh create-ami.sh -r "6.2" -d "OpenBSD 6.2";
```

Launch your newly created AMI, check public IP and login "ssh root@public_IP". 
You might want to delete S3 volume and EBS volume used during creating process as well as destroying your vagrant instance.
