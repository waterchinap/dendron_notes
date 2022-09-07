---
id: 626f8fzt3xg9srkabo62ci0
title: 同步本地文件到oss
desc: ''
updated: 1662565912904
created: 1662565912904
isDir: false
---
# 同步本地文件到OSS

**目前我上传同步的命令是**
`./ossutil64 sync ~/workdir/ridemyway/site/ oss://ridemyway/ --delete -f`

更新时间：2021-09-09 16:55

[我的收藏](https://help.aliyun.com/my_favorites.html)

<a id="cmdname-hv6-9e1-jka"></a>sync命令用于将本地文件同步到OSS。

## 注意事项

- Binary名称
    
    本文各命令行示例均基于Linux 64位系统，其他系统请将命令开头的<a id="cmdname-o0l-d59-ud5"></a>./ossutil64替换成对应的Binary名称。详情请参见[命令行工具ossutil快速入门](https://help.aliyun.com/document_detail/195960.htm#task-2012304 "本文旨在引导您通过命令行工具ossutil快速创建目标存储空间（Bucket），然后将本地文件上传至Bucket。上传完成后，将文件（Object）下载至本地或者通过生成签名URL的方式将文件分享给第三方，供其下载或预览。")。
    
- 文件数量
    
    通过sync命令执行同步任务时，如果没有携带<a id="option-zdb-whh-3jn"></a>--delete选项，则单次同步任务同步的文件个数无限制。如果携带了<a id="option-m6r-5nt-cbv"></a>--delete选项，则单次同步任务最多可同步100万个文件。当同步的文件个数超出100万时，将报错over max sync numbers 1000000.。
    
- sync命令与cp命令的区别
    
    - sync命令强制以递归的方式遍历指定文件夹内所有文件或子文件夹。cp命令需增加<a id="option-x18-iaq-vuw"></a>-r选项才会进行递归操作。
    - 通过sync命令将数据同步到OSS时，ossutil支持通过<a id="option-1o9-kk3-e6l"></a>--delete选项将目的端存在而源端不存在的文件都删除，仅保留本次同步的文件。cp命令不支持<a id="option-yyv-oas-dlq"></a>--delete选项。
    - sync不支持<a id="option-i10-dcs-94a"></a>--version-id选项，无法在已开启版本控制的Bucket内同步历史版本文件。cp命令支持<a id="option-fk0-918-g1d"></a>--version-id选项。
    
    除以上区别外，sync命令与cp命令用法类似。有关cp命令的用法及示例，请参见[cp（上传文件）](https://help.aliyun.com/document_detail/179388.htm#concept-1937458 "您可以通过cp命令将您的本地文件或文件夹上传至OSS。")。
    

## 命令格式

```
./ossutil64 sync file_url cloud_url
[-f --force]
[-u --update]
[--delete]
[--enable-symlink-dir]
[--disable-all-symlink]
[--disable-ignore-error]
[--only-current-dir]
[--output-dir <value>]
[--bigfile-threshold <value>]
[--part-size <value>]
[--checkpoint-dir <value>]
[--encoding-type <value>]
[--snapshot-path <value>]
[--include <value>]
[--exclude <value>]
[--meta <value>]
[--acl <value>]
[--maxupspeed <value>]
[--disable-crc64]
[--payer <value>]
[-j, --job <value>]
[--parallel <value>]
[--retry-times <value>]
[--tagging <value>]
```

参数及选项说明如下：

  
| 配置项 | 说明  |
| --- | --- |
| <a id="parmname-1dt-1pk-itk"></a>file_url | 待同步的本地文件夹路径。例如Linux系统文件路径`/localfolder/`，Windows系统文件路径`D:\localfolder\`。 |
| <a id="parmname-59q-uhm-dbe"></a>cloud_url | OSS文件夹路径。格式为`oss://bucketname/path/`。例如`oss://examplebucket/exampledir/`。如果输入的`cloud_url`没有以正斜线（/）结尾，ossutil会自动在结尾处添加一个正斜线（/）。 |
| <a id="parmname-leq-lzv-y7x"></a>-f --force | 强制操作，不进行询问提示。 |
| <a id="parmname-u2e-25k-puy"></a>-u，--update | 只有当目标文件不存在，或源文件的最后修改时间晚于目标文件时，ossutil才会执行同步操作。 |
| <a id="parmname-esg-42u-s31"></a>--delete | 删除目的端指定路径下的其他文件，仅保留本次同步的文件。<br><br>**警告** 建议您使用<a id="parmname-vp5-xiq-ddj"></a>--delete选项前开启[版本控制](https://help.aliyun.com/document_detail/109695.htm#concept-jdg-4rx-bgb "版本控制是针对存储空间（Bucket）级别的数据保护功能。开启版本控制后，针对数据的覆盖和删除操作将会以历史版本的形式保存下来。您在错误覆盖或者删除对象（Object）后，能够将Bucket中存储的Object恢复至任意时刻的历史版本。")，防止数据误删除。 |
| <a id="parmname-w1s-vrv-szh"></a>--enable-symlink-dir | 同步链接子目录。 |
| <a id="parmname-7uc-ct5-wu0"></a>--disable-all-symlink | 同步目录时，忽略所有的链接子文件以及链接子目录。 |
| <a id="parmname-f97-2e8-jcc"></a>--disable-ignore-error | 批量操作时不忽略错误。 |
| <a id="parmname-lns-20n-57t"></a>--only-current-dir | 仅同步当前目录下的文件，忽略子目录及子目录下的文件。 |
| <a id="parmname-psz-fs2-br1"></a>--output-dir | 指定输出文件所在的目录。输出文件是指批量同步文件出错时产生的report文件，默认保存在当前目录下的<a id="filepath-fi1-jh7-v6k"></a>ossutil_output目录。 |
| <a id="parmname-tlo-pak-ajl"></a>-bigfile-threshold | 设置断点续传文件的大小阈值，单位为字节。<br><br>默认值：100 MB<br><br>取值范围：0~9223372036854775807 |
| <a id="parmname-t8c-cuc-ow6"></a>--part-size | 设置分片大小，单位为字节。默认情况下ossutil会根据文件大小自行计算合适的分片大小值。<br><br>取值范围：1~9223372036854775807 |
| <a id="parmname-rtb-xnc-6yx"></a>--checkpoint-dir | 指定断点续传记录信息所在的目录。断点续传操作失败时，ossutil会自动创建名为`.ossutil_checkpoint`的目录，并在该目录下记录checkpoint信息，断点续传成功后会删除该目录。如果通过该选项指定了目录，请确保指定的目录可以被删除。 |
| <a id="parmname-8jn-hk6-yjq"></a>--encoding-type | 文件名称的编码方式。取值为<a id="option-8dt-ivp-res"></a>url。如果不指定该选项，则表示文件名称未经过编码。 |
| <a id="parmname-f29-0gt-9rb"></a>--snapshot-path | 指定保存同步文件时的快照信息所在的目录。在下一次同步文件时，ossutil会读取指定目录下的快照信息进行增量同步。 |
| <a id="parmname-dbh-3lc-ops"></a>--include | 包含符合指定条件的所有文件。 |
| <a id="parmname-1iz-pib-7l2"></a>--exclude | 不包含任何符合指定条件的文件。 |
| <a id="parmname-zk6-2x0-0a9"></a>--meta | 设置文件的元信息，格式为`header:value#header:value`，示例为`Cache-Control:no-cache#Content-Encoding:gzip`。有关元信息的介绍，请参见[set-meta（管理文件元信息）](https://help.aliyun.com/document_detail/120056.htm#concept-303809 "文件元信息是对文件（Object）的属性描述，包括HTTP标准属性（HTTP Header）和用户自定义元数据（User Meta）两种。其中，HTTP Header可用于自定义HTTP请求的策略，用户自定义元数据可用于标识文件的用途或属性等。您可以通过set-meta命令为已上传的文件（Object）设置、修改或者删除文件元信息。")。 |
| <a id="parmname-ou2-t4v-57e"></a>--acl | 文件的读写权限ACL。取值如下：<br><br>- <a id="option-aoy-ig4-pwz"></a>default：继承Bucket的读写权限。<br>- <a id="option-01e-q16-rlz"></a>private（默认值）：只有该Bucket的拥有者可以对该Bucket内的文件进行读写操作，其他人无法访问该Bucket内的文件。<br>- <a id="option-avx-0a3-tlm"></a>public-read：只有Bucket拥有者可以对该Bucket内的文件进行写操作，其他用户（包括匿名访问者）都可以对该Bucket中的文件进行读操作。这有可能造成您数据的外泄以及费用激增，若被人恶意写入违法信息还可能会侵害您的合法权益。除特殊场景外，不建议您配置此权限。<br>- <a id="option-152-wm8-yzh"></a>public-read-write：任何人（包括匿名访问者）都可以对该Bucket内文件进行读写操作。这有可能造成您数据的外泄以及费用激增，请谨慎操作。 |
| <a id="parmname-pgn-flw-i71"></a>--maxupspeed | 最大上传速度，单位为KB/s。默认值为0，表示不限制上传速度。 |
| <a id="parmname-dv1-6f0-uap"></a>--disable-crc64 | 关闭CRC64数据校验。 |
| <a id="parmname-295-emx-s9j"></a>--payer | 请求的支付方式。如果希望访问指定路径下的资源产生的流量、请求次数等费用由请求者支付，请将此选项的值设置为<a id="option-b83-6js-6i7"></a>requester。 |
| <a id="parmname-twn-j8l-tqc"></a>-j，--job | 多文件操作时的并发任务数，默认值为3，取值范围为1~10000。 |
| <a id="parmname-sh4-jo9-d8q"></a>--parallel | 单文件操作时的并发任务数，取值范围为1~10000。 如果不设置此选项，默认由ossutil根据操作类型和文件大小自行决定。 |
| <a id="parmname-ljb-xtv-6fs"></a>--retry-times | 发生错误后的重试次数。默认值为10，取值范围为1~500。 |
| <a id="parmname-248-40f-oxv"></a>--tagging | 文件的标签信息，格式为`TagkeyA=TagvalueA&TagkeyB=TagvalueB....`。 |

## 使用示例

本地根目录下<a id="filepath-8nn-61l-bxv"></a>localfolder 文件夹内有<a id="filepath-7ii-nm5-apl"></a>d.txt和<a id="filepath-pvy-0yt-abp"></a>e.png文件。OSS中名为examplebucket的Bucket下文件夹<a id="filepath-q1x-cz9-gvg"></a>destfolder内有文件<a id="filepath-zmc-d62-832"></a>a.txt、<a id="filepath-3wj-1tf-7yh"></a>b.txt和子文件夹<a id="filepath-fmq-xw4-ewp"></a>C，文件结构如下：

```
本地根目录                  examplebucket
    └── localfolder         └── destfolder/
            ├── d.txt               ├── a.txt
            ├── e.png               ├── b.txt
                                       └── C/
```

示例场景及命令如下：

- 将本地<a id="filepath-zuy-bhd-0vc"></a>localfolder文件夹同步到OSS
    
    ```
    ./ossutil64 sync localfolder/  oss://examplebucket/destfolder/
    ```
    
    命令执行后，examplebucket的 <a id="filepath-spr-2nv-q7g"></a>destfolder文件夹内新增<a id="filepath-vkf-b0x-ntd"></a>d.txt和<a id="filepath-umh-rrm-va5"></a>e.png文件。
    
    ```
    本地根目录                  examplebucket
        └── localfolder         └── destfolder/
                ├── d.txt               ├── a.txt
                ├── e.png               ├── b.txt
                                           ├── d.txt 
                                           ├── e.png 
                                           └── C/ 
    ```
    
- 同步本地文件夹到OSS，并删除OSS指定路径下已存在而本地端不存在的文件
    
    通过增加<a id="parmname-u2g-zjj-mqt"></a>--delete选项，删除目的端存在而源端不存在的文件，仅保留本次同步的文件。
    
    ```
    ./ossutil64 sync localfolder/  oss://examplebucket/destfolder/ --delete
    ```
    
    命令执行后，本地<a id="filepath-fsa-3uc-q9k"></a>localfolder文件夹被同步到OSS，同时会删除OSS的文件<a id="filepath-as1-yp7-pem"></a>a.txt、<a id="filepath-gir-xds-esa"></a>b.txt以及子文件夹<a id="filepath-8oe-ot9-wdg"></a>C，即OSS的<a id="filepath-e04-avg-d39"></a>destfolder文件夹内仅保留<a id="filepath-84d-ns5-pyv"></a>d.txt和<a id="filepath-yot-wzm-etj"></a>e.png文件。
    
    ```
    本地根目录                  examplebucket
        └── localfolder         └── destfolder/
                ├── d.txt                ├── d.txt
                ├── e.png                ├── e.png 
    ```
    
- 同步本地文件夹到OSS，并省略问询操作
    
    默认情况下，同步本地文件夹到OSS时，如果目的端存在同名文件，ossutil会进行覆写操作的问询。命令如下：
    
    ```
    ./ossutil64 sync localfolder/ oss://examplebucket/destfolder/
    cp: overwrite "oss://examplebucket/destfolder/d.txt"(y or N)?
    ```
    
    如果您确认目的端文件均可被覆写，可增加<a id="parmname-j0j-won-wyv"></a>-f，--force选项强制执行覆写操作。命令如下：
    
    ```
    ./ossutil64 sync localfolder/ oss://examplebucket/destfolder/ -f，--force
    ```
    
    命令执行后，examplebucket的<a id="filepath-ltw-0uh-w3x"></a>destfolder文件夹内新增<a id="filepath-pig-3z4-0fc"></a>d.txt和<a id="filepath-7gu-w2u-k6u"></a>e.png文件。
    
    ```
    本地根目录                  examplebucket
        └── localfolder         └── destfolder/
                ├── d.txt               ├── a.txt
                ├── e.png               ├── b.txt
                                           ├── d.txt 
                                           ├── e.png
                                           └── C/ 
    ```
    
- 以上示例同步成功后，返回结果中将包含同步的文件数量、文件大小以及完成同步操作所用时长，示例如下：
    
    ```
    Succeed: Total num: 2, size: 750,081. OK num: 2(upload 2 files).
    
    average speed 1641000(byte/s)
    ```
    

## 通用选项

当您需要通过命令行工具ossutil管理不同地域的Bucket时，可以通过<a id="parmname-d0n-z8h-w0g"></a>-e选项切换至指定Bucket所属的Endpoint。当您需要通过命令行工具ossutil管理多个阿里云账号下的Bucket时，可以通过<a id="parmname-agz-8zf-pub"></a>-i选项切换至指定账号的AccessKey ID，并通过<a id="parmname-701-9q8-ona"></a>-k选项切换至指定账号的AccessKey Secret。

例如，您需要将本地文件夹srcfolder的文件同步至另一个阿里云账号下，华东2（上海）地域下存储空间examplebucket的文件夹testfolder，命令如下：

```
./ossutil64 sync srcfolder/ oss://examplebucket/testfolder/ -e oss-cn-shanghai.aliyuncs.com -i LTAI4Fw2NbDUCV8zYUzA****  -k 67DLVBkH7EamOjy2W5RVAHUY9H****
```

有关此命令的其他通用选项的更多信息，请参见[通用选项](https://help.aliyun.com/document_detail/50455.htm#section-yhn-ko6-gqj)。