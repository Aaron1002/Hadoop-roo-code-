# Hadoop HDFS 指令指南

本指南將提供常用的 HDFS 指令，說明如何上傳、下載、刪除、讀取 HDFS 上的文件。

1.  **連接到 HDFS：**

    在執行任何 HDFS 指令之前，請確保 Hadoop 叢集已啟動。

2.  **常用 HDFS 指令：**

    *   **列出目錄內容：**

        ```bash
        hdfs dfs -ls <path>
        ```

        例如：

        ```bash
        hdfs dfs -ls /
        ```

    *   **建立目錄：**

        ```bash
        hdfs dfs -mkdir <path>
        ```

        例如：

        ```bash
        hdfs dfs -mkdir /test
        ```

    *   **上傳文件：**

        ```bash
        hdfs dfs -put <local_path> <hdfs_path>
        ```

        例如：

        ```bash
        hdfs dfs -put input.txt /test
        ```

    *   **下載文件：**

        ```bash
        hdfs dfs -get <hdfs_path> <local_path>
        ```

        例如：

        ```bash
        hdfs dfs -get /test/input.txt input.txt
        ```

    *   **刪除文件或目錄：**

        ```bash
        hdfs dfs -rm -r <path>
        ```

        例如：

        ```bash
        hdfs dfs -rm -r /test
        ```

    *   **讀取文件內容：**

        ```bash
        hdfs dfs -cat <path>
        ```

        例如：

        ```bash
        hdfs dfs -cat /test/input.txt
        ```

    *   **複製文件：**

        ```bash
        hdfs dfs -cp <source_path> <destination_path>
        ```

        例如：

        ```bash
        hdfs dfs -cp /test/input.txt /test/input_copy.txt
        ```

    *   **移動文件：**

        ```bash
        hdfs dfs -mv <source_path> <destination_path>
        ```

        例如：

        ```bash
        hdfs dfs -mv /test/input.txt /test/input_moved.txt
        ```

    *   **查看文件大小：**

        ```bash
        hdfs dfs -du -h <path>
        ```

        例如：

        ```bash
        hdfs dfs -du -h /test/input.txt