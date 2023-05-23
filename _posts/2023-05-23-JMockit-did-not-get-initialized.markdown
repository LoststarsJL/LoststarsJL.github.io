---
layout: post
title: "JMockit didn't get initialized"
date: 2023-05-23 08:23:13 +0800
categories: 
header-img: "img/post-bg.jpg"
header-mask: 0.3
---

## 使用JMockit报错

### 问题描述

引入JMockit依赖后，配合Junit编写测试方法，运行测试方法报错。

```(shell)
JMockit didn't get initialized; please check the -javaagent JVM initialization parameter was used
```

### 解决办法

添加`-javaagent JVM`初始化参数。

这里使用`Maven Surefire`插件进行测试，并通过它添加参数。

在`pom.xml`文件中加入下述依赖

```(xml)
<properties>
    <jmockit.version>1.46</jmockit.version>
</properties>

<dependency>
    <groupId>org.jmockit</groupId>
    <artifactId>jmockit</artifactId>
    <version>${jmockit.version}</version>
    <scope>test</scope>
</dependency>

<build>
    <plugins>
        <plugin>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.21.0</version>
            <configuration>
                <testFailureIgnore>true</testFailureIgnore>
                <argLine>
                    -javaagent:${settings.localRepository}/org/jmockit/jmockit/${jmockit.version}/jmockit-${jmockit.version}.jar
                </argLine>
            </configuration>
        </plugin>
    </plugins>
</build>
```
