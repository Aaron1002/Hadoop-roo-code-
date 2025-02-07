# 編譯和執行 Hadoop MapReduce 程式

1.  **確認 Hadoop 環境變數已設定：**

    請確保您已按照 Hadoop 安裝指南設定了 `HADOOP_HOME`、`PATH` 和 `JAVA_HOME` 環境變數。

2.  **編譯 Java 程式：**

    使用以下命令編譯 `WordCount.java` 檔案：

    ```bash
    javac -classpath "$HADOOP_HOME/share/hadoop/common/*:$HADOOP_HOME/share/hadoop/mapreduce/*:$HADOOP_HOME/share/hadoop/hdfs/*:." -d . WordCount.java
    ```

3.  **建立 JAR 檔案：**

    使用以下命令建立 JAR 檔案：

    ```bash
    jar -cvf WordCount.jar WordCount\*.class
    ```

4.  **準備輸入資料：**

    將您的輸入文本檔案上傳到 HDFS。例如，如果您的輸入檔案名為 `input.txt`，則可以使用以下命令將其上傳到 HDFS：

    ```bash
    hdfs dfs -mkdir /input
    hdfs dfs -put input.txt /input
    ```

5.  **執行 MapReduce 程式：**

    使用以下命令執行 MapReduce 程式：

    ```bash
    hadoop jar WordCount.jar WordCount /input /output
    ```

    請注意，`/input` 是 HDFS 上的輸入目錄，`/output` 是 HDFS 上的輸出目錄。如果 `/output` 目錄已存在，則需要先將其刪除。

6.  **查看輸出結果：**

    MapReduce 程式執行完成後，您可以使用以下命令查看輸出結果：

    ```bash
    hdfs dfs -cat /output/part-r-00000
    ```

    此命令將顯示每個單詞及其出現次數。