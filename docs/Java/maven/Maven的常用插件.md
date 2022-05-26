# Maven的常用插件

## 编译器插件

- 通过编译器插件，我们可以配置使用的JDK的版本：

- 配置编译器插件：`pom.xml`配置片段

- ```xml
  <!-- 配置maven的编译插件 --> 
  <build>
      <plugins>
      <!--JDK编译插件 -->
            <plugin>
          <!--插件坐标 -->
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.2</version>
           <!-- -->
          <configuration>
            <!-- 源代码使用JDK版本-->
            <source>1.7</source>
             <!-- 源代码编译为class文件的版本，要保持跟上面版本一致-->
            <target>1.7</target>
            <encoding>UTF-8</encoding>
          </configuration>
        </plugin>
      </plugins>
    </build>
  ```

## 资源拷贝插件

- Maven在打包时默认只将`src/main/resources`里的配置文件拷贝到项目中并做打包处理，而非resource目录下的配置文件在打包时不会添加到项目中。

- 想把非resources下面的文件也打包到classes下面需要配置`pom.xml`

- `pom.xml`配置片段：

- ```xml
  <build>
          <resources>
                          <resource>
                                  <directory>src/main/java</directory>
                                  <includes>
                                          <include>**/*.xml</include>
                                  </includes>
                          </resource>
                          <resource>
                                  <directory>src/main/resources</directory>
                                  <includes>
                                          <include>**/*.xml</include>
                                          <include>**/*.properties</include>
                                  </includes>
                          </resource>
                  </resources>
          </build>
  ```

  ## tomcat插件

  - 之前如果是创建一个war项目，必然是需要部署在服务器上，那么主要有以下两种方式进行

    - 直接部署咋远程服务器上

    - 将IDEA和外部tomcat产生联系，然后将项目部署到外部tomcat上

    - `pom.xml`文件配置

    - ```xml
      <build>
          <plugins>
            <!-- 配置Tomcat插件 -->
            <plugin>
              <groupId>org.apache.tomcat.maven</groupId>
              <artifactId>tomcat7-maven-plugin</artifactId>
              <version>2.2</version>
              <configuration>
           <!-- 配置Tomcat监听端口 -->
                <port>8080</port>
           <!-- 配置项目的访问路径(Application Context) -->
                <path>/</path>
              </configuration>
            </plugin>
          </plugins>
        </build>
      ```

    - 使用Tomcat插件发布部署并执行war工程的时候，需要使用启动命令，启动命令为： ==tomcat7:run==。命令中的tomcat7是插件命名，由插件提供商决定。run为插件中的具体功能。