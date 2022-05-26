# Maven的常用命令

## install

- 本地安装，包含==编译，打包==。并且安装到本地仓库

## clean

- 清除已编译信息
- 并且删除工程中target目录

## compile

- 对项目进行编译，类似与java中的javac命令

## package

- 打包，包含==编译，打包==。两个功能

## install与package的区别

- package命令只是完成了==项目编译、单元测试、打包功能==，但是没有把打包好的可执行jar包（或者war包或者其他形式的包）部署到本地maven仓库与远程maven私服仓库
- install命令完成了==项目编译、单元测试、打包功能，同时把打好的可执行jar包（war包或其它形式的包）布署到本地maven仓库==，但没有布署到远程maven私服仓库