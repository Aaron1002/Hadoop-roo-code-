# Hadoop 與 Spark 整合指南

本指南將說明如何在 Hadoop 叢集上部署 Apache Spark 3.5.0，並舉例說明如何使用 Spark 讀取 HDFS 資料。

1.  **下載 Spark：**

    從 Apache Spark 官方網站下載 Spark 3.5.0：

    ```bash
    wget https://archive.apache.org/dist/spark/spark-3.5.0/spark-3.5.0-bin-hadoop3.tgz
    tar -xzf spark-3.5.0-bin-hadoop3.tgz
    sudo mv spark-3.5.0-bin-hadoop3 /usr/local/spark
    ```

2.  **配置 Spark 環境變數：**

    編輯 `~/.bashrc` 文件：

    ```bash
    nano ~/.bashrc
    ```

    在文件末尾添加以下內容：

    ```bash
    export SPARK_HOME=/usr/local/spark
    export PATH=$PATH:$SPARK_HOME/bin
    export PATH=$PATH:$SPARK_HOME/sbin
    ```

    儲存並關閉文件。然後執行以下命令使變更生效：

    ```bash
    source ~/.bashrc
    ```

3.  **配置 Spark：**

    Spark 的配置文件位於 `$SPARK_HOME/conf/` 目錄下。

    *   **spark-env.sh**

        複製 `spark-env.sh.template` 文件並編輯：

        ```bash
        cp $SPARK_HOME/conf/spark-env.sh.template $SPARK_HOME/conf/spark-env.sh
        nano $SPARK_HOME/conf/spark-env.sh
        ```

        添加以下內容：

        ```bash
        export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
        export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
        export YARN_CONF_DIR=/usr/local/hadoop/etc/hadoop
        ```

4.  **啟動 Spark：**

    ```bash
    start-all.sh
    ```

5.  **驗證 Spark：**

    瀏覽器訪問 `http://localhost:4040` 查看 Spark 介面。

6.  **使用 Spark 讀取 HDFS 資料：**

    以下是一個使用 Spark 讀取 HDFS 資料的範例：

    ```python
    from pyspark.sql import SparkSession

    # 建立 SparkSession
    spark = SparkSession.builder.appName("HDFSExample").getOrCreate()

    # 從 HDFS 讀取文本文件
    df = spark.read.text("hdfs://localhost:9000/input/input.txt")

    # 顯示 DataFrame
    df.show()

    # 停止 SparkSession
    spark.stop()
    ```

    將以上程式碼儲存為 `hdfs_example.py`，然後使用以下命令執行：

    ```bash
    spark-submit hdfs_example.py