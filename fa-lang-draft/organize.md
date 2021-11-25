# fa语言草案之项目组织方式

## 项目组织方式

fa项目文件夹组织如下（尖括号代表临时文件或文件夹）：

```log
MyProject
    ┣<build>
        ┗MyProject.exe
    ┣<build_temp>
    ┣<refs>
        ┣<引用的其他fa语言项目本地地址索引>
        ┗<程序用到的本地静态/动态库>
    ┣<refs_3rd>
        ┗<引用的其他fa语言项目源码克隆>
    ┣src
        ┗main.fa
    ┗MyProject.faproj
```
