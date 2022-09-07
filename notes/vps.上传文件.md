---
id: tte0d9izaciu4s5q9f7lqr8
title: 上传文件
desc: ''
updated: 1662565912902
created: 1662565912902
isDir: false
---
您可以通过<a id="cmdname-6su-ebi-anc"></a>cp命令将您的本地文件或文件夹上传至OSS。

## 注意事项

- 本文各命令行示例均基于Linux 64位系统，其他系统请将命令开头的<a id="cmdname-2gq-gv1-w6q"></a>./ossutil64替换成对应的Binary名称。详情请参见[命令行工具ossutil快速入门](https://help.aliyun.com/document_detail/195960.htm#task-2012304 "本文旨在引导您通过命令行工具ossutil快速创建目标存储空间（Bucket），然后将本地文件上传至Bucket。上传完成后，将文件（Object）下载至本地或者通过生成签名URL的方式将文件分享给第三方，供其下载或预览。")。
- 使用<a id="cmdname-tig-8fx-jle"></a>cp命令上传文件时，默认使用分片上传和断点续传。如果您因意外中断了文件上传的过程，且未继续完成该文件的上传，则已上传的部分会以碎片（Part）的形式存储在OSS的存储空间（Bucket）中。如果您不再需要这些Part，建议您通过以下方式删除，以免产生额外的存储费用。
    - 手动删除Part，请参见[删除碎片](https://help.aliyun.com/document_detail/120053.htm#li-n3o-5sr-xg9)。
    - 通过生命周期规则自动删除Part，请参见[设置生命周期规则](https://help.aliyun.com/document_detail/31904.htm#concept-bmx-p2f-vdb "您可以通过生命周期规则来批量转换存储空间（Bucket）内对象（Object）的存储类型，也可以批量删除指定的Object和碎片（Part）。")。

## 命令格式

```
./ossutil64 cp file_url cloud_url
[-r, --recursive]
[-f --force]
[-u --update]
[--maxupspeed <value>]
[--enable-symlink-dir]
[--disable-all-symlink]
[--disable-ignore-error]
[--only-current-dir]
[--bigfile-threshold <value>]
[--part-size <value>]
[--checkpoint-dir <value>]
[--encoding-type <value>]
[--include <value>]
[--exclude <value>]
[--meta <value>]
[--acl <value>]
[--snapshot-path <value>]
[--disable-crc64]
[--disable-dir-object]
[--payer <value>]
[--tagging <value>]
[-j, --job <value>]
[--parallel <value>]
```

参数及选项说明如下：

  
| 配置项 | 说明  |
| --- | --- |
| <a id="parmname-mf9-4et-uy0"></a>file_url | 本地文件路径。例如Linux系统文件路径`/localfolder/examplefile.txt`，Windows系统文件路径`D:\localfolder\examplefile.txt`。 |
| <a id="parmname-0gu-ty8-qjo"></a>cloud_url | OSS文件路径。格式为`oss://bucketname/objectname`。例如`oss://examplebucket/examplefile.txt`。 |
| <a id="parmname-5vk-uza-p3g"></a>-r, --recursive | 递归操作。当指定该选项时，ossutil会对Bucket下所有符合条件的Object进行操作，否则只对指定的单个Object进行操作。 |
| <a id="parmname-2qq-oju-q9t"></a>-f --force | 强制操作，不进行询问提示。 |
| <a id="parmname-aym-82q-3kd"></a>-u，--update | 只有当目标文件不存在，或源文件的最后修改时间晚于目标文件时，ossutil才会执行上传操作。 |
| <a id="parmname-cvc-gdz-304"></a>--maxupspeed | 最大上传速度，单位为KB/s。默认值为0，表示不限制上传速度。 |
| <a id="parmname-wh3-i5j-s9d"></a>--enable-symlink-dir | 上传链接子目录，默认不上传。 |
| <a id="parmname-x70-h0v-qx1"></a>--disable-all-symlink | 上传时忽略所有的软链接子文件以及软链接子目录。 |
| <a id="parmname-grp-z7b-2d2"></a>--disable-ignore-error | 批量操作时不忽略错误。 |
| <a id="parmname-fpd-vb0-r5a"></a>--only-current-dir | 仅上传当前目录下的文件，忽略子目录及子目录下的文件。 |
| <a id="parmname-n8h-iqn-z17"></a>-bigfile-threshold | 设置断点续传文件的大小阈值，单位为字节。<br><br>默认值：100 MB<br><br>取值范围：0~9223372036854775807 |
| <a id="parmname-rir-qws-ixr"></a>--part-size | 设置分片大小，单位为字节。默认情况下ossutil会根据文件大小自行计算合适的分片大小值。<br><br>取值范围：1~9223372036854775807 |
| <a id="parmname-gzn-oq5-jv2"></a>--checkpoint-dir | 指定断点续传记录信息所在的目录。断点续传操作失败时，ossutil会自动创建名为`.ossutil_checkpoint`的目录，并在该目录下记录checkpoint信息，断点续传成功后会删除该目录。如果指定了该选项，请确保指定的目录可以被删除。 |
| <a id="parmname-4r3-lpb-iqt"></a>--encoding-type | 文件名称的编码方式。取值为<a id="option-e3v-s2m-vfe"></a>url。如果不指定该选项，则表示文件名称未经过编码。 |
| <a id="parmname-e6q-4vt-u8e"></a>--include | 包含符合指定条件的所有文件。 |
| <a id="parmname-wia-x9j-e7v"></a>--exclude | 不包含任何符合指定条件的文件。 |
| <a id="parmname-qk8-zoz-9pa"></a>--meta | 设置文件的元信息，格式为`header:value#header:value`，示例为`Cache-Control:no-cache#Content-Encoding:gzip`。有关元信息的介绍，请参见[set-meta（管理文件元信息）](https://help.aliyun.com/document_detail/120056.htm#concept-303809 "文件元信息是对文件（Object）的属性描述，包括HTTP标准属性（HTTP Header）和用户自定义元数据（User Meta）两种。其中，HTTP Header可用于自定义HTTP请求的策略，用户自定义元数据可用于标识文件的用途或属性等。您可以通过set-meta命令为已上传的文件（Object）设置、修改或者删除文件元信息。")。 |
| <a id="parmname-phg-8xa-lrv"></a>--acl | 文件的读写权限ACL。取值如下：<br><br>- <a id="option-cdw-bqo-h6n"></a>default：继承Bucket的读写权限。<br>- <a id="option-lt2-ir4-zcp"></a>private（默认值）：只有该Bucket的拥有者可以对该Bucket内的文件进行读写操作，其他人无法访问该Bucket内的文件。<br>- <a id="option-uu7-s9t-a1x"></a>public-read：只有Bucket拥有者可以对该Bucket内的文件进行写操作，其他用户（包括匿名访问者）都可以对该Bucket中的文件进行读操作。这有可能造成您数据的外泄以及费用激增，如果被人恶意写入违法信息还可能会侵害您的合法权益。除特殊场景外，不建议您配置此权限。<br>- <a id="option-77t-7q8-r7x"></a>public-read-write：任何人（包括匿名访问者）都可以对该Bucket内文件进行读写操作。这有可能造成您数据的外泄以及费用激增，请谨慎操作。 |
| <a id="parmname-k3y-xok-1ru"></a>--snapshot-path | 指定保存上传文件时的快照信息所在的目录。在下一次上传文件时，ossutil会读取指定目录下的快照信息进行增量上传。 |
| <a id="parmname-ty6-kd4-xeb"></a>--disable-crc64 | 关闭CRC64数据校验。默认情况下，ossutil进行数据传输时都会打开CRC64校验。 |
| <a id="parmname-h19-ekf-8ji"></a>--disable-dir-object | 表示上传文件时不为目录生成Object。 |
| <a id="parmname-u6h-ul7-fbd"></a>--payer | 请求的支付方式。如果希望访问指定路径下的资源产生的流量、请求次数等费用由请求者支付，请将此选项的值设置为<a id="option-1c7-cn0-8dz"></a>requester。 |
| <a id="parmname-mrh-vdm-oy7"></a>--tagging | 上传文件时设置标签信息，格式为`TagkeyA=TagvalueA&TagkeyB=TagvalueB....`。 |
| <a id="parmname-ety-qk2-29n"></a>-j，--jobs | 多文件操作时的并发任务数，默认值为3，取值范围为1~10000。 |
| <a id="parmname-m13-8cr-q39"></a>--parallel | 单文件操作时的并发任务数，取值范围为1~10000。 如果不设置此选项，默认由ossutil根据操作类型和文件大小自行决定。 |

从以上命令格式中的<a id="parmname-pmy-7y5-7xe"></a>-j，--jobs和<a id="parmname-vu2-y3c-7oi"></a>--parallel选项得知，当ossutil自行设置的默认并发数达不到用户的性能要求时，您可以自行调整这两个选项来升降性能。默认情况下，ossutil会根据文件大小来计算parallel个数。当批量上传大文件时，实际的并发数为jobs个数乘以parallel个数。

- 当ECS虚拟机或者服务器在网络、内存、CPU等资源不是特别大的情况下，建议将并发数调整到100以下。如果网络、内存、CPU等资源没有占满，可以适当增加并发数。
- 由于线程间资源切换及抢夺等原因，如果并发数过大，ossutil上传性能可能会下降。此外，并发数过大还可能产生EOF错误。所以请根据实际的机器情况调整<a id="parmname-xxb-ru6-h4g"></a>-j，--jobs和<a id="parmname-u57-u5s-y6w"></a>--parallel选项的数值。如果要进行压测，可在一开始时调低这两项数值，然后逐渐调大直至找到最优值。

## 示例环境

本文以Linux系统为例，将本地文件或文件夹上传至OSS中。您在实际使用中，请根据您的系统和使用环境修改对应参数。本文涉及的通用示例说明如下：

- 本地文件：examplefile.txt（根目录下的文件）
- 本地文件夹：localfolder（根目录下的文件夹）
- 目标Bucket：examplebucket
- 目标Bucket指定目录：desfolder

## 简单上传

ossutil支持将本地文件上传到OSS，示例如下：

- 上传单个文件
    
    上传文件时，如果不指定上传至OSS的文件名，则默认使用原文件名进行保存；如果指定文件名，则按照指定的文件名保存在OSS中。
    
    ```
    ./ossutil64 cp examplefile.txt oss://examplebucket/desfolder/
    ```
    
- 仅上传文件夹内的文件
    
    使用<a id="cmdname-4b6-bjy-5jz"></a>cp命令时增加<a id="parmname-e90-1ri-tgw"></a>-r选项，可以将目标文件夹内的文件上传到OSS指定目录。
    
    ```
    ./ossutil64 cp -r localfolder/ oss://examplebucket/desfolder/
    ```
    
- 上传文件夹及文件夹内的文件
    
    使用<a id="cmdname-oh0-2iy-pb1"></a>cp命令时增加<a id="parmname-1mx-9v8-pvi"></a>-r选项，可以将目标文件夹以及文件夹内的文件上传到OSS指定目录。
    
    ```
    ./ossutil64 cp -r localfolder/ oss://examplebucket/desfolder/localfolder/
    ```
    
- 上传单个文件并指定<a id="parmname-fv9-406-ofd"></a>--meta选项
    
    上传文件的同时可以使用<a id="parmname-j9p-a1k-qys"></a>--meta选项设置文件的meta信息，其内容格式为`header:value#header:value...`。
    
    ```
    ./ossutil64 cp examplefile.txt oss://examplebucket/desfolder/examplefile.txt --meta=Cache-Control:no-cache#Content-Encoding:gzip
    ```
    
- 上传文件夹并跳过已有文件
    
    批量上传失败重传时，可以指定<a id="parmname-ndc-0ix-1gc"></a>--update（可缩写为<a id="parmname-7fj-vl0-erg"></a>-u）选项跳过已经上传成功的文件，实现增量上传。示例如下：
    
    ```
    ./ossutil64 cp -r localfolder/ oss://examplebucket/desfolder/ -u
    ```
    
- 上传文件到开通了请求者付费模式的Bucket
    
    ```
    ./ossutil64 cp localfolder/examplefile.txt oss://examplebucket/ --payer=requester
    ```
    
- 仅上传当前目录下的文件，忽略子目录
    
    ```
    ./ossutil64 cp localfolder/ oss://examplebucket/desfolder/ --only-current-dir -r
    ```
    
- 上传时不为目录生成Object
    
    OSS的目录是用一个0 KB大小，名称以正斜线（/）结尾的Object模拟的。上传时增加<a id="parmname-tjk-ut1-jxt"></a>--disable-dir-object参数，ossutil不会为该目录生成Object，但您仍可以在OSS控制台看到对应的目录结构。当您删除目录内的文件时，该目录也会消失。
    
    ```
    ./ossutil64 cp localfolder/ oss://examplebucket/desfolder/ --disable-dir-object -r
    ```
    
- 上传软链接子目录下的文件
    
    ```
    ./ossutil64 cp localfolder/ oss://examplebucket/desfolder/ --enable-symlink-dir -r
    ```
    
- 上传时忽略所有的软链接子文件以及软链接子目录
    
    ```
    ./ossutil64 cp localfolder/ oss://examplebucket/desfolder/ -r --disable-all-symlink
    ```
    

## 上传时限速

您可以在上传文件时，结合<a id="parmname-m9o-c29-xds"></a>--maxupspeed选项来限制上传的最大速度，单位为KB/s。示例如下：

- 上传文件并设置限速为1 MB/s
    
    ```
    ./ossutil64 cp examplefile.txt oss://examplebucket/desfolder/ --maxupspeed 1024
    ```
    
- 上传文件夹并设置限速为1 MB/s
    
    ```
    ./ossutil cp -r localfolder/ oss://examplebucket/desfolder/ --maxupspeed 1024
    ```
    

## 上传并设置对象标签

您可以在上传文件时，通过<a id="parmname-7y9-tq0-2ft"></a>--tagging选项设置文件对象标签，多个标签以and（&）符号隔开。示例如下：

```
./ossutil cp examplefile.txt oss://examplebucket/desfolder/ --tagging "abc=1&bcd=2&……"
```

关于对象标签的更多说明请参见[object-tagging（对象标签）](https://help.aliyun.com/document_detail/129735.htm#concept-1614441 "OSS支持以标签的方式对存储的对象（Object）进行分类，方便您管理拥有相同标签的Object，例如通过生命周期规则为相同标签的Object指定过期天数或转换其存储类型。object-tagging命令用于添加、修改、获取和删除对象标签。")。

## 上传并指定文件类型

您可以在上传文件时，通过<a id="parmname-hy5-992-v7d"></a>--meta选项设置文件存储类型。存储类型可选值为：

- Standard：标准存储
- IA：低频访问
- Archive：归档存储

如果上传时未指定存储类型，则以存储空间的存储类型为准。更多详情请参见[存储类型介绍](https://help.aliyun.com/document_detail/51374.htm#concept-fcn-3xt-tdb "对象存储OSS提供标准、低频访问、归档、冷归档四种存储类型，全面覆盖从热到冷的各种数据存储场景。")。示例如下：

- 上传单个文件并指定存储类型为低频访问类型
    
    ```
    ./ossutil cp examplefile.txt oss://examplebucket/desfolder/ --meta X-oss-Storage-Class:IA
    ```
    
- 上传文件夹并指定存储类型为标准存储类型
    
    ```
    ./ossutil cp localfolder/ oss://examplebucket/desfolder/ --meta X-oss-Storage-Class:Standard -r
    ```
    

## 上传并指定读写权限ACL

您可以在上传文件时，通过<a id="parmname-4a2-pt6-1f8"></a>--meta选项设置文件的ACL。文件ACL可选值为：

- default：继承Bucket（默认）
- private：私有
- public-read：公共读
- public-read-write：公共读写

示例如下：

- 上传单个文件并指定ACL为私有
    
    ```
    ./ossutil cp examplefile.txt oss://examplebucket/desfolder/ --meta x-oss-object-acl:private
    ```
    
- 上传文件夹并指定ACL为公共读
    
    ```
    ./ossutil cp localfolder/ oss://examplebucket/desfolder/ --meta x-oss-object-acl:public-read  -r
    ```
    

## 上传并指定加密方式

您可以在上传文件时指定文件的服务器端加密方式，将文件加密后保存在Bucket内。 示例如下：

- 上传文件并指定加密方式为OSS完全托管，加密算法为AES256
    
    ```
    ./ossutil cp examplefile.txt oss://examplebucket/desfolder/ --meta=x-oss-server-side-encryption:AES256
    ```
    
- 上传文件并指定加密方式为OSS完全托管，加密算法为SM4
    
    ```
    ./ossutil cp examplefile.txt oss://examplebucket/desfolder/ --meta=x-oss-server-side-encryption:SM4
    ```
    
- 上传文件并指定加密方式为KMS<a id="ph-8c5-y54-1be"></a>，指定加密算法为AES256，不指定CMK ID
    
    ```
    ./ossutil cp examplefile.txt oss://examplebucket/desfolder/ --meta=x-oss-server-side-encryption:KMS
    ```
    
    使用KMS加密时，会产生少量KMS密钥使用费用，详情请参见[KMS计费标准](https://help.aliyun.com/document_detail/52608.htm#section-br1-k3j-kfb)。
    
- 上传文件并指定加密方式为KMS，指定加密算法为SM4，指定CMK ID
    
    ```
    ./ossutil cp examplefile.txt oss://examplebucket/desfolder/ --meta=x-oss-server-side-encryption:KMS#x-oss-server-side-data-encryption:SM4#x-oss-server-side-encryption-key-id:7bd6e2fe-cd0e-483e-acb0-f4b9e1******
    ```
    

有关服务器端加密功能介绍，请参见[服务器端加密](https://help.aliyun.com/document_detail/31871.htm#concept-lqm-fkd-5db "对象存储OSS支持服务器端加密功能。上传文件（Object）时，OSS对收到的文件进行加密，再将得到的加密文件持久化保存；下载文件时，OSS自动将加密文件解密后返回给用户，并在返回的HTTP请求Header中，声明该文件进行了服务器端加密。")。

## 上传并生成快照

批量上传时，如果指定<a id="parmname-kbs-1a6-bfx"></a>--snapshot-path选项，ossutil在指定的目录下生成文件上传的快照，记录成功上传的文件的本地lastModifiedTime，在下次上传时通过比较lastModifiedTime来决定是否跳过相同文件，所以在使用该选项时，请确保两次上传期间没有其他用户更改了OSS上对应的Object。<a id="parmname-rxv-u85-pfn"></a>--snapshot-path选项适用于加速增量上传的场景。示例如下：

```
./ossutil cp -r localfolder/ oss://examplebucket/desfolder/ --snapshot-path=path 
```

**注意**

- ossutil不会主动删除<a id="filepath-9ut-nzs-i1n"></a>snapshot-path文件夹中的快照信息。为避免快照信息过多，请定期删除<a id="filepath-i0w-ng3-226"></a>snapshot-path文件夹内无用的快照。
- 由于读写snapshot信息需要额外开销，当待批量上传的文件数量较少、网络状况较好、或有其他用户操作相同Object时，不建议使用该选项。针对以上情况，您可以使用<a id="parmname-9gl-190-1z2"></a>--update选项来增量上传。
- <a id="parmname-jep-50f-9i1"></a>--update选项和<a id="parmname-gzc-13l-7o8"></a>--snapshot-path选项可以同时使用，ossutil会优先根据snapshot-path信息判断是否跳过此文件，如果不满足跳过条件，再根据<a id="parmname-z66-v0k-v0l"></a>--update判断是否跳过此文件。

## 批量上传符合条件的文件

批量上传时，如果指定<a id="parmname-gxu-qej-tpr"></a>--include和<a id="parmname-acr-io5-h5y"></a>--exclude选项，ossutil会批量上传符合指定条件的文件。

<a id="parmname-o1c-rgf-r7u"></a>--include和<a id="parmname-aa9-hes-ntt"></a>--exclude选项支持格式：

- 通配符星号（*）：匹配所有字符。例如：<a id="filepath-x9c-4xf-qit"></a>*.txt表示匹配所有<a id="filepath-vx6-5vh-pwo"></a>TXT格式的文件。
- 通配符问号（？）：匹配单个字符。例如：<a id="filepath-h4j-hhz-l0o"></a>abc?.jpg表示匹配所有文件名为abc+任意单个字符的JPG格式的文件，如<a id="filepath-ukw-v0g-zcz"></a>abc1.jpg。
- \[sequence\]：匹配序列的任意字符，例如：<a id="filepath-ivz-p1r-vt4"></a>abc\[1-5\].jpg表示匹配文件名为<a id="filepath-0wn-zx2-yx8"></a>abc1.jpg~abc5.jpg的文件。
- \[!sequence\]：匹配序列外的任意字符，例如：<a id="filepath-h7z-yj4-qic"></a>abc\[!0-7\].jpg表示匹配文件名不为<a id="filepath-af3-4xp-6b3"></a>abc0.jpg~abc7.jpg的文件。

一条规则中可以包含多个include（包含）和exclude（排除）条件，且每个文件从左到右逐一运用每个规则，直至最后才能最终确定匹配的结果。例如指定生效的文件夹中包含名为<a id="filepath-wgm-xjr-0hz"></a>test.txt的文件，匹配不同的规则产生的结果如下。

- 规则一：`--include "*test*" --exclude "*.txt"` ，当规则匹配到`--include "*test*"`，匹配的结果为<a id="filepath-xgk-vga-zi5"></a>test.txt符合条件；当规则继续匹配到`--exclude "*.txt"`时，因<a id="filepath-q3h-n5e-otj"></a>test.txt文件名包含.txt，所以被排除。则匹配的最终结果为<a id="filepath-vvu-emp-4cz"></a>test.txt不符合条件。
- 规则二：`--exclude "*.txt" --include "*test*"`，当规则匹配到`--exclude "*.txt"`，匹配的结果为<a id="filepath-gza-dac-fxz"></a>test.txt不符合条件；当规则继续匹配到`--include "*test*"`，因<a id="filepath-d99-3pl-dmk"></a>test.txt文件名包含test，所以符合条件。则匹配的最终结果为<a id="filepath-ac0-p6n-320"></a>test.txt符合条件。
- 规则三：`--include "*test*" --exclude "*.txt" --include "te?t.txt"` ，当规则匹配到`--include "*test*"`，匹配的结果为<a id="filepath-dsi-zuu-s7l"></a>test.txt符合条件；当规则继续匹配到`--exclude "*.txt"`时，因<a id="filepath-t8v-gio-a6h"></a>test.txt文件名包含.txt，所以被排除；当规则最后匹配到`--include "te?t.txt"`时，因<a id="filepath-xuc-zm7-8ss"></a>test.txt符合条件，所以被包含。则匹配的最终结果为<a id="filepath-pgg-crc-c2m"></a>test.txt符合条件。

**注意** 设定条件时不支持目录格式，例如`--include "/usr/test/.jpg"`。

示例如下：

- 上传所有文件格式为<a id="filepath-lpc-e1k-ybk"></a>TXT的文件
    
    ```
    ./ossutil cp localfolder/ oss://examplebucket/desfolder/ --include "*.txt" -r
    ```
    
- 上传所有文件名包含<a id="filepath-hbe-yz3-91x"></a>abc且不是<a id="filepath-31q-csv-81y"></a>JPG和<a id="filepath-w3w-0k3-s9j"></a>TXT格式的文件
    
    ```
    ./ossutil cp localfolder/ oss://examplebucket/desfolder/ --include "*abc*" --exclude "*.jpg" --exclude "*.txt" -r
    ```
    

## 通用选项

当您需要通过命令行工具ossutil管理不同地域的Bucket时，可以通过<a id="parmname-6qu-1ey-qbs"></a>-e选项切换至指定Bucket所属的Endpoint。当您需要通过命令行工具ossutil管理多个阿里云账号下的Bucket时，可以通过<a id="parmname-zoi-qih-t8o"></a>-i选项切换至指定账号的AccessKey ID，并通过<a id="parmname-3e5-qhc-rvg"></a>-k选项切换至指定账号的AccessKey Secret。

例如，您需要将本地文件exampleobject.txt上传至另一个阿里云账号下，华东2（上海）地域的存储空间examplebucket的destfolder目录下，命令如下：

```
./ossutil64 cp exampleobject.txt oss://examplebucket/desfolder/ -e oss-cn-shanghai.aliyuncs.com -i LTAI4Fw2NbDUCV8zYUzA****  -k 67DLVBkH7EamOjy2W5RVAHUY9H****
```

有关此命令的其他通用选项的更多信息，请参见[通用选项](https://help.aliyun.com/document_detail/50455.htm#section-yhn-ko6-gqj)。