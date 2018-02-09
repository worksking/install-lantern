记录在centos安装lantern的过程，

## 第一步：先上结果图

![](https://i.imgur.com/DNC79gE.jpg)

## 第二步：安装必备的软件alien
```
# yum install epel-release
# rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
# rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
```
## 第三步：下载ubuntn的deb包。
[download](https://github.com/getlantern/lantern/releases/tag/latest)

## 第四步：转化成rpm包
```
sudo alien -r lantern-installer-64-bit.deb
```
此时会出现：`Get Error:“conflicts with file from package filesystem”`

##第五步：安装rpmrebuild

```
sudo yum install rpmrebuild
sudo rpmrebuild -pe lantern-4.0.1-2.x86_64.rpm
```
## 第六部：替换文件(把里面的内容替换成下面的，大约在中间部位)
```
(Converted from a deb package by alien version 8.95.)
%files
#%dir %attr(0755, root, root) "/"
#%dir %attr(0755, root, root) "/usr"
#%dir %attr(0755, root, root) "/usr/bin"
%attr(0777, root, root) "/usr/bin/lantern"
#%dir %attr(0755, root, root) "/usr/lib"
%dir %attr(0755, root, root) "/usr/lib/lantern"
%attr(0644, root, root) "/usr/lib/lantern/.packaged-lantern.yaml"
%attr(0644, root, root) "/usr/lib/lantern/lantern-binary"
%attr(0755, root, root) "/usr/lib/lantern/lantern.sh"
%attr(0644, root, root) "/usr/lib/lantern/lantern.yaml"
#%dir %attr(0755, root, root) "/usr/share"
#%dir %attr(0755, root, root) "/usr/share/applications"
%attr(0644, root, root) "/usr/share/applications/lantern.desktop"
#%dir %attr(0755, root, root) "/usr/share/doc"
%dir %attr(0755, root, root) "/usr/share/doc/lantern"
%doc %attr(0644, root, root) "/usr/share/doc/lantern/changelog.gz"
%doc %attr(0644, root, root) "/usr/share/doc/lantern/copyright"
#%dir %attr(0755, root, root) "/usr/share/icons"
#%dir %attr(0755, root, root) "/usr/share/icons/hicolor"
#%dir %attr(0755, root, root) "/usr/share/icons/hicolor/128x128"
#%dir %attr(0755, root, root) "/usr/share/icons/hicolor/128x128/apps"
%attr(0644, root, root) "/usr/share/icons/hicolor/128x128/apps/lantern.png"
%changelog
```
## 第七步：安装
```
sudo rpm -i /root/rpmbuild/RPMS/x86_64/lantern-4.0.1-2.x86_64.rpm
```

## 第八步：会出现错误

```
sudo yum install libappindicator-gtk3
```

## 第九步：

```
cp /usr/lib/lantern/lantern.sh  ~
./lantern.sh  
```

第十步：
1.先设置成自动，写入lantern地址栏上的，`http://localhost:39572`  每个人不一样。
2.启动后会自动设置成下图：
![](https://i.imgur.com/EIouJox.jpg)


有啥不懂的可以问。着急分享，就不注重细节了，费一天时间还是蛮开心的。喜欢的点歌star。后续慢慢补充完整。

参考文章：
[为自己写代码](https://c4ys.com/archives/1102)

https://github.com/getlantern/lantern/issues/1720

https://linux.cn/article-6120-1.html
