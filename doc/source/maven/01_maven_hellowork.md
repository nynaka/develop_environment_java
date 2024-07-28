01 Hello Work (Maven)
===

1. Hello Work プロジェクトの作成

    ```bash
    mvn archetype:generate \
        -DgroupId=com.example \
        -DartifactId=hellowork \
        -DarchetypeArtifactId=maven-archetype-quickstart \
        -DinteractiveMode=false
    cd hellowork
    ```

    このコマンドで生成されるコードは下記のようになります。

    ```text
    hellowork
    |-- pom.xml
    |-- src
    | |-- main
    | | |-- java
    | | | |-- com
    | | | | |-- example
    | | | | | |-- App.java
    | |-- test
    | | |-- java
    | | | |-- com
    | | | | |-- example
    | | | | | |-- AppTest.java
    ```

2. pom.xml の修正

    最低限、`maven.compiler.source` と `maven.compiler.target` の指定は必要のようです。

    ```diff
    --- /tmp/pom.xml        2024-07-27 11:32:00.986932971 +0900
    +++ pom.xml     2024-07-27 11:36:46.413485172 +0900
    @@ -7,6 +7,12 @@
       <version>1.0-SNAPSHOT</version>
       <name>hellowork</name>
       <url>http://maven.apache.org</url>
    +  <properties>
    +    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    +    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    +    <maven.compiler.source>21</maven.compiler.source>
    +    <maven.compiler.target>21</maven.compiler.target>
    +  </properties>
       <dependencies>
         <dependency>
           <groupId>junit</groupId>
    ```

3. ソースコードの準備

    デフォルトで生成されている `Hello world!` のままでもよいです。

    ```java
    package com.example;

    /**
     * Hello Work...
     *
     */
    public class App
    {
        public static void main( String[] args )
        {
            System.out.println( "Hello Work..." );
        }
    }
    ```

4. ビルド

    ```bash
    mvn package
    ```

5. 実行

    ```bash
    java -cp  target/hellowork-1.0-SNAPSHOT.jar com.example.App
    ```
