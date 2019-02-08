# s3s
`s3s` is a tiny CLI that helps you upload local file to your private s3 bucket, generating a presign URL for this file followed by URL shortening with `bit.ly`.

## Build

```
$ make build
$ cp ./s3s ~/bin/
$ s3s
usage: s3s <bucket> <filename>
```

add `export BITLY_TOKEN='<YOUR_BITLY_TOKEN>'` in your `~/.bash_profile`                                                                                                                         


## Usage

```
AWS_PROFILE=<YOUR_PROFILE_NAME> AWS_DEFAULT_REGION=<TARGET_AWS_REGION> s3s <YOUR_S3_BCKET> FILE  
```


## Example #1: through AWS Global regions
```
$ AWS_DEFAULT_REGION=ap-northeast-1 s3s pahud-tmp-nrt  ../lambda-layer-awscli/func-bundle.zip                                                             
Uploading file to S3...                                                                                                                                                                    
Successfully uploaded ../lambda-layer-awscli/func-bundle.zip to https://pahud-tmp-nrt.s3.ap-northeast-1.amazonaws.com/func-bundle.zip                                                      
2019/02/08 14:28:53 The URL is https://pahud-tmp-nrt.s3.ap-northeast-1.amazonaws.com/func-bundle.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAJJFINOFXR3LTLIFQ%2F20190208%2Fap
-northeast-1%2Fs3%2Faws4_request&X-Amz-Date=20190208T142853Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=6b25d5713ac4c928c6f9a6c519841d6ec270807e1f8b7a30387af54023661540
LongURL: https://pahud-tmp-nrt.s3.ap-northeast-1.amazonaws.com/func-bundle.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAJJFINOFXR3LTLIFQ/20190208/ap-northeast-1/s3/aws4_reque
st&X-Amz-Date=20190208T142853Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=6b25d5713ac4c928c6f9a6c519841d6ec270807e1f8b7a30387af54023661540                              
ShortURL: http://bit.ly/2WRSEkE         
```

## Example #2: through AWS China Beijing or Ningxia region

```
$ AWS_PROFILE=cn AWS_DEFAULT_REGION=cn-northwest-1 s3s pahud-tmp-cn-northwest-1  ../lambda-layer-awscli/func-bundle.zip                                   
Uploading file to S3...                                                                                                                                                                    
Successfully uploaded ../lambda-layer-awscli/func-bundle.zip to https://pahud-tmp-cn-northwest-1.s3.cn-northwest-1.amazonaws.com.cn/func-bundle.zip                                        
2019/02/08 14:27:51 The URL is https://pahud-tmp-cn-northwest-1.s3.cn-northwest-1.amazonaws.com.cn/func-bundle.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAOEVQOGI2VHQNTNHA%2
F20190208%2Fcn-northwest-1%2Fs3%2Faws4_request&X-Amz-Date=20190208T142751Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=08900dc04ba2d19be3f5bf8ee2e30fee771ed6c212df9a3116
e9951b7b2500b1                                                                                                                                                                             
LongURL: https://pahud-tmp-cn-northwest-1.s3.cn-northwest-1.amazonaws.com.cn/func-bundle.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAOEVQOGI2VHQNTNHA/20190208/cn-northwest-1
/s3/aws4_request&X-Amz-Date=20190208T142751Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=08900dc04ba2d19be3f5bf8ee2e30fee771ed6c212df9a3116e9951b7b2500b1                
ShortURL: http://bit.ly/2RP7jtp          
```

You may also set an alias in your `~/.bash_profile` like this

```
alias s3sjp="AWS_PROFILE=default AWS_DEFAULT_REGION=ap-northeast-1 s3s pahud-tmp-ap-northeast-1 $@"                                                                                             
alias s3scn="AWS_PROFILE=cn AWS_DEFAULT_REGION=cn-northwest-1 s3s pahud-tmp-cn-northwest-1 $@"                                                                                             
```

And simply 

```
$ s3sjp FILE
or
$ s3scn FILE
```

to upload your local file to your private S3 bucket and get the `bitly` URL immediately.

e.g.

upload to `Tokyo region(ap-northeast-1)`
```
$ s3sjp ../lambda-layer-awscli/func-bundle.zip                                                                                                            
Uploading file to S3...                                                                                                                                                                    
Successfully uploaded ../lambda-layer-awscli/func-bundle.zip to https://pahud-tmp-ap-northeast-1.s3.ap-northeast-1.amazonaws.com/func-bundle.zip                                           
2019/02/08 14:44:20 The URL is https://pahud-tmp-ap-northeast-1.s3.ap-northeast-1.amazonaws.com/func-bundle.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAJJFINOFXR3LTLIFQ%2F20
190208%2Fap-northeast-1%2Fs3%2Faws4_request&X-Amz-Date=20190208T144420Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=6710694d356f7a473f05b7eabe3103bab7d8dc6474bc862dd1c65
c36d67d1dd5                                                                                                                                                                                
LongURL: https://pahud-tmp-ap-northeast-1.s3.ap-northeast-1.amazonaws.com/func-bundle.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAJJFINOFXR3LTLIFQ/20190208/ap-northeast-1/s3
/aws4_request&X-Amz-Date=20190208T144420Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=6710694d356f7a473f05b7eabe3103bab7d8dc6474bc862dd1c65c36d67d1dd5                   
ShortURL: http://bit.ly/2WNuiZq             
```

upload to `Ningxia region(cn-northwest-1)`

```
$ s3scn ../lambda-layer-awscli/func-bundle.zip                                                                                                            
Uploading file to S3...                                                                                                                                                                    
Successfully uploaded ../lambda-layer-awscli/func-bundle.zip to https://pahud-tmp-cn-northwest-1.s3.cn-northwest-1.amazonaws.com.cn/func-bundle.zip                                        
2019/02/08 14:40:50 The URL is https://pahud-tmp-cn-northwest-1.s3.cn-northwest-1.amazonaws.com.cn/func-bundle.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAOEVQOGI2VHQNTNHA%2
F20190208%2Fcn-northwest-1%2Fs3%2Faws4_request&X-Amz-Date=20190208T144050Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=7aba040654c3a1b27373cc982c4bc17e4e7a2573142ec9bbc6
09f246c99afd9c                                                                                                                                                                             
LongURL: https://pahud-tmp-cn-northwest-1.s3.cn-northwest-1.amazonaws.com.cn/func-bundle.zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAOEVQOGI2VHQNTNHA/20190208/cn-northwest-1
/s3/aws4_request&X-Amz-Date=20190208T144050Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=7aba040654c3a1b27373cc982c4bc17e4e7a2573142ec9bbc609f246c99afd9c                
ShortURL: http://bit.ly/2WQzD2b                                                                                     
```