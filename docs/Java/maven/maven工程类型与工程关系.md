# Maven工程类型

## POM工程

- POM工程是逻辑工程，用在父级工程或聚合工程中，主要是用来作为jar包的版本控制

## JAR工程

- 将会打包成jar包，用作jar包使用。也就是我们常见的java本地工程

## WAR工程

- 将会打包成war包，发布在服务器上面的工程

# Maven工程关系

## 依赖

- 在开发过程中，A工程需要B工程的支持，那么就说A工程依赖B工程，通俗的理解就是导jar包
- B工程可以是自己项目打包后的jar包，也可以是远程仓库中的jar包

- 使用依赖的方法

  - 在maven工程中使用依赖，可以直接在项目的`pom.xml`文件中进行配置即可，不用将jar包导入

  - ```xml
        <!-- 通过dependencies添加依赖，可以添加多个依赖 -->
        <dependencies>
           <!-- dependencies里面可以有多个dependency--> 
            <dependency>
                <!--dependency可以直接在maven远程中央仓库直接获取-->
                <groupId>org.mybatis</groupId>
                <artifactId>mybatis</artifactId>
                <version>3.5.5</version>
            </dependency>
        </dependencies>
    ```

- 依赖的传递性

  - 传递性依赖是Maven2.0的新特性。假设你的项目依赖于一个库，而这个库又依赖于其他库。你不必自己去找出所有这些依赖，你只需要加上你直接依赖的库，Maven会隐式的把这些库间接依赖的库也加入到你的项目中

- 依赖的两个原则

  - 最短路径优先原则
    - “最短路径优先”意味着项目依赖关系树中路径最短的版本会被使用
    - 假设A、B、C之间的依赖关系是A->B->C->D(2.0)  和A->E->(D1.0)，那么D(1.0)会被使用，因为A通过E到D的路径更短。
  - 最先声明原则
    - 依赖路径长度是一样的的时候，第一原则不能解决所有问题，maven定义了依赖调解的第二原则，第一声明优先，在依赖路径长度相等的前提下，在POM中依赖声明的顺序决定了谁会被解析使用。顺序最靠前的那个依赖优胜。

- 如何排除特定的依赖

  - `exclusions`： 用来排除传递性依赖 其中可配置多个exclusion标签

  - 每个exclusion标签里面对应的有groupId, artifactId, version三项基本元素。注意：不用写版本号。

  - ```xml
        <dependencies>
            <!-- 子工程依赖父工程 -->
            <dependency>
                <groupId>com.shanlei</groupId>
                <artifactId>MavenDemo</artifactId>
                <version>1.0-SNAPSHOT</version>
                <!-- 将父工程中的mybatis依赖排除-->
                <exclusions>
                    <exclusion>
                        <groupId>org.mybatis</groupId>
                        <artifactId>mybatis</artifactId>
                    </exclusion>
                </exclusions>
            </dependency>
        </dependencies>
    ```

- 依赖的范围

  - compile

    - 这是默认范围。如果没有指定，就会使用该依赖范围。表示该依赖在==编译和运行时都生效==。

  - provided

    - 已提供依赖范围。使用此依赖范围的Maven依赖。典型的例子是servlet-api，编译和测试项目的时候需要该依赖，但在运行项目的时候，由于容器已经提供，就不需要Maven重复地引入一遍(如：servlet-api)

  - runtime

    - runtime范围表明编译时不需要生效，而==只在运行时生效==。

  - system

    - 系统范围与provided类似，不过你==必须显式指定一个本地系统路径的JAR==。

    - ```xml
          <!-- 通过dependencies添加依赖，可以添加多个依赖    -->
          <dependencies>
              <dependency>
                  <groupId>org.mybatis</groupId>
                  <artifactId>mybatis</artifactId>
                  <version>3.5.5</version>
                  <scope>system</scope>
                  <systemPath>XXXXXXXXX</systemPath>
              </dependency>
          </dependencies>
      ```

  - test

    - ==只在编译测试代码和运行测试的时候需要==

  - import

    - import范围只适用于pom文件中的`<dependencyManagement>`部分。表明指定的POM必须使用`<dependencyManagement>`部分的依赖。
    - 注意：import只能用在dependencyManagement的scope里

## 继承

- 如果A工程继承B工程，则代表A工程默认依赖B工程依赖的所有资源，且可以应用B工程中定义的所有资源信息。

- 被继承的工程（B工程）只能是POM工程。

- 放在`<dependencyManagement>`中的内容主要目的是进行版本管理。里面的内容在子项目中依赖时坐标只需要填写`<group id>`和`<artifact id>`即可。（注意：如果子项目不希望使用父项目的版本，可以明确配置version）

  - ```xml
    <!--  父工程  -->
        <properties>
            <mybatis-version>3.5.5</mybatis-version>
        </properties>
        <dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>org.mybatis</groupId>
                    <artifactId>mybatis</artifactId>
                    <version>${mybatis-version}</version>
                </dependency>
            </dependencies>
        </dependencyManagement>
    ```

  - ```xml
    <!--  子工程  -->
        <!-- 指定MavenDemo工程为本工程的父工程 -->
        <parent>
            <groupId>com.shanlei</groupId>
            <artifactId>MavenDemo</artifactId>
            <version>1.0-SNAPSHOT</version>
            <relativePath>../MavenDemo/pom.xml</relativePath>
        </parent>
    
        <dependencies>
            <!-- 子工程依赖父工程 -->
            <dependency>
                <groupId>com.shanlei</groupId>
                <artifactId>MavenDemo</artifactId>
            </dependency>
        </dependencies>
    ```

## 聚合

- 当我们开发的工程拥有2个以上模块的时候，每个模块都是一个独立的功能集合。每个平台都可以独立编译，测试，运行。这个时候我们就需要一个聚合工程。

- 在创建聚合工程的过程中，总的工程必须是一个POM工程（Maven Project）（聚合项目必须是一个pom类型的项目，jar项目war项目是没有办法做聚合工程的），各子模块可以是任意类型模块（Maven Module）

- 聚合的前提是继承，聚合包含了继承的特性

- 聚合时多个项目的本质还是一个项目。这些项目被一个大的父项目包含。且这时父项目类型为pom类型。同时在父项目的pom.xml中出现<modules>表示包含的所有子模块

  - POM项目的`pom.xml`文件配置

  - ```xml
        <modules>
            <module>Childpro</module>
        </modules>
        <!--  定义POM工程  -->
        <packaging>pom</packaging>
        <!--  定义版本号  -->
        <porperties>
            <mybatis.version>3.5.5</mybatis.version>
            <spring.version>5.3.5</spring.version>
        </porperties>
    
        <dependencyManagement>
            <dependencies>
                <!-- 依赖mybatis -->
                <dependency>
                    <groupId>org.mybatis</groupId>
                    <artifactId>mybatis</artifactId>
                    <version>${mybatis-version}</version>
                </dependency>
    
                <!-- 依赖spring -->
                <dependency>
                    <groupId>org.springframework</groupId>
                    <artifactId>spring-core</artifactId>
                    <version>${spring.version}</version>
                </dependency>
            </dependencies>
        </dependencyManagement>
    ```

  - 模块`pom.xml`文件配置

  - ```xml
    <parent>
            <artifactId>MavenDemo</artifactId>
            <groupId>com.shanlei</groupId>
            <version>1.0-SNAPSHOT</version>
        </parent>
        <modelVersion>4.0.0</modelVersion>
    
        <artifactId>Childpro</artifactId>
        <dependencies>
            <!-- 依赖mybatis -->
            <dependency>
                <groupId>org.mybatis</groupId>
                <artifactId>mybatis</artifactId>
            </dependency>
    
            <!-- 依赖spring -->
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
            </dependency>
        </dependencies>
    ```

