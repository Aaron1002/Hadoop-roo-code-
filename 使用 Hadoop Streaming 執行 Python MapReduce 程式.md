# 使用 Hadoop Streaming 執行 Python MapReduce 程式

1.  **準備輸入資料：**

    將您的輸入文本檔案上傳到 HDFS。例如，如果您的輸入檔案名為 `input.txt`，則可以使用以下命令將其上傳到 HDFS：

    ```bash
    hdfs dfs -mkdir /input
    hdfs dfs -put input.txt /input
    ```

2.  **執行 Hadoop Streaming 程式：**

    使用以下命令執行 Hadoop Streaming 程式：

    ```bash
    hadoop jar $HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.3.6.jar \
    -input /input \
    -output /output \
    -mapper mapper.py \
    -reducer reducer.py
    ```

    請注意，`/input` 是 HDFS 上的輸入目錄，`/output` 是 HDFS 上的輸出目錄。如果 `/output` 目錄已存在，則需要先將其刪除。

3.  **查看輸出結果：**

    MapReduce 程式執行完成後，您可以使用以下命令查看輸出結果：

    ```bash
    hdfs dfs -cat /output/part-00000
    ```

    此命令將顯示每個單詞及其出現次數。