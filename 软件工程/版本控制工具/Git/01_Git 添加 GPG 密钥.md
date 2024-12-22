# Git 添加 GPG 密钥

## 1. 概述

&emsp;&emsp;git 作为一个版本工具，在使用前，你是需要用 `git config user.email xxx` 和 `git config user.username xxx` 来进行配置你的邮箱和用户名，但是如果说，今天 我心情不爽，用 `git config user.email 同事A@email; git config user.username 同事A名` ；那么这个时候，我提交了，锅是不是甩给用户 A 了；且 git 其实本身是无法判断的，会把我识别成同事 A；那么为了可靠的校验每一次提交你是你；git 是提供 gpg 密钥来进行验证的；

&emsp;&emsp;以 GitHub 来进行举例，如果没有进行添加 GPG 密钥；那么他的递交是：

![image-20241222160305359](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2024/12/1734854592426fb5.png)

## 2. 创建步奏

1.   验证 gpg 版本

     ```shell
     $ gpg --version
     gpg (GnuPG) 2.4.5-unknown
     libgcrypt 1.9.4-unknown
     Copyright (C) 2024 g10 Code GmbH
     License GNU GPL-3.0-or-later <https://gnu.org/licenses/gpl.html>
     This is free software: you are free to change and redistribute it.
     There is NO WARRANTY, to the extent permitted by law.
     
     Home: /c/Users/azwcl/.gnupg
     Supported algorithms:
     Pubkey: RSA, ELG, DSA, ECDH, ECDSA, EDDSA
     Cipher: IDEA, 3DES, CAST5, BLOWFISH, AES, AES192, AES256, TWOFISH,
             CAMELLIA128, CAMELLIA192, CAMELLIA256
     Hash: SHA1, RIPEMD160, SHA256, SHA384, SHA512, SHA224
     Compression: Uncompressed, ZIP, ZLIB, BZIP2
     ```

2.   生成 GPG 密钥对

     ```shell
     $ gpg --full-generate-key
     生成过程中，需要填写密钥类型、密钥大小、有效期等信息；
     ```

3.   查看密钥信息

     ```shell
     gpg --list-secret-keys --keyid-format LONG
     gpg: checking the trustdb
     gpg: marginals needed: 3  completes needed: 1  trust model: pgp
     gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
     [keyboxd]
     ---------
     sec   ed25519/XXXXXXXXXX1 2024-12-22 [SC]
           XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX2
     uid                 [ultimate] azwcl <azwcl@outlook.com>
     ssb   cv25519/XXXXXXXXXX3 2024-12-22 [E]
     ```

4.   查看密钥内容

     ```shell
     gpg --armor --export XXXXXXXXXX1
     ```

## 3. Github 添加 gpg 密钥

1.   GitHub Settings 打开

2.   SSH and GPG keys 选项 --> New GPG key 去添加一个；最后将上面密钥内容放入即可；

     ![image-20241222161822037](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2024/12/1734855502752743.png)

## 4. 本地 Git 关联此密钥

```shell
# 1. 关联，当然，你也可以使用 --global 参数；如果不使用，就到那个仓库目录去关联即可；
git config user.signingkey XXXXXXXXXX1
# 2. 配置 Git 始终签署提交；也可以使用 --global 参数，指定全局；
git config  commit.gpgSign true
# 3. 大功告成；
```

