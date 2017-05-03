---
title: MD5加密 
tags: 密码加密方法
grammar_cjkRuby: true
---


    MD5功能：
    输入任意长度的信息，经过处理，输出为128位的信息（数字指纹）；
    不同的输入得到的不同的结果（唯一性）；
    根据128位的输出结果不可能反推出输入的信息（不可逆）； 
	
	MD5用途：
    1、防止被篡改：
    1）比如发送一个电子文档，发送前，我先得到MD5的输出结果a。然后在对方收到电子文档后，对方也得到一个MD5的输出结果b。如果a与b一样就代表中途未被篡改。2）比如我提供文件下载，为了防止不法分子在安装程序中添加木马，我可以在网站上公布由安装文件得到的MD5输出结果。3）SVN在检测文件是否在CheckOut后被修改过，也是用到了MD5.

    2、防止直接看到明文：
    现在很多网站在数据库存储用户的密码的时候都是存储用户密码的MD5值。这样就算不法分子得到数据库的用户密码的MD5值，也无法知道用户的密码(其实这样是不安全的，后面我会提到)。（比如在UNIX系统中用户的密码就是以MD5（或其它类似的算法）经加密后存储在文件系统中。当用户登录的时候，系统把用户输入的密码计算成MD5值，然后再去和保存在文件系统中的MD5值进行比较，进而确定输入的密码是否正确。通过这样的步骤，系统在并不知道用户密码的明码的情况下就可以确定用户登录系统的合法性。这不但可以避免用户的密码被具有系统管理员权限的用户知道，而且还在一定程度上增加了密码被破解的难度。）

    3、防止抵赖（数字签名）：
    这需要一个第三方认证机构。例如A写了一个文件，认证机构对此文件用MD5算法产生摘要信息并做好记录。若以后A说这文件不是他写的，权威机构只需对此文件重新产生摘要信息，然后跟记录在册的摘要信息进行比对，相同的话，就证明是A写的了。这就是所谓的“数字签名”。

参考:http://blog.csdn.net/forgotaboutgirl/article/details/7258109

``` MD5
public void testDigest(){
        try {
            MessageDigest digest = MessageDigest.getInstance("md5");
            String password= "123456";
            byte[] bytes = digest.digest(password.getBytes());
            StringBuffer sb = new StringBuffer();
            for (byte b : bytes) {
                String hex = Integer.toHexString(b & 0xff);
                if(hex.length()==1) {
                    sb.append(0);
                }
                sb.append(hex);
            }
            Log.v("cherish233",sb.toString());

        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
        }
    }
```
