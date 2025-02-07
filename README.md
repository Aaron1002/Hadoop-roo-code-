# Hadoop 指南

本指南包含以下內容：

1.  **Hadoop安裝與配置指南.md：** 說明如何在 Ubuntu 上安裝和配置 Hadoop 3.3.6 單節點偽分散式叢集。
2.  **WordCount.java：** 一個 Java MapReduce 程式，用於計算輸入文本中每個單詞的出現次數。
3.  **編譯和執行 Hadoop MapReduce 程式.md：** 說明如何編譯和執行 `WordCount.java` 程式。
4.  **mapper.py：** 一個 Python MapReduce 程式，用於計算單詞出現次數（Mapper）。
5.  **reducer.py：** 一個 Python MapReduce 程式，用於計算單詞出現次數（Reducer）。
6.  **使用 Hadoop Streaming 執行 Python MapReduce 程式.md：** 說明如何使用 Hadoop Streaming 執行 `mapper.py` 和 `reducer.py` 程式。
7.  **Hadoop HDFS 指令指南.md：** 提供常用的 HDFS 指令，說明如何上傳、下載、刪除、讀取 HDFS 上的文件。
8.  **Hadoop 與 Spark 整合指南.md：** 說明如何在 Hadoop 叢集上部署 Apache Spark 3.5.0，並舉例說明如何使用 Spark 讀取 HDFS 資料。
9.  **Hadoop 與 AI/機器學習應用案例.md：** 說明如何使用 Spark MLlib 和 MNIST 手寫數字資料集進行分類，並說明如何使用 Hadoop 處理大規模數據。

## 如何使用本指南

1.  **安裝和配置 Hadoop：**

    *   按照 `Hadoop安裝與配置指南.md` 中的步驟，在您的 Ubuntu 系統上安裝和配置 Hadoop 3.3.6 單節點偽分散式叢集。
    *   驗證 Hadoop 安裝是否成功，確保 HDFS 和 YARN 介面可以正常訪問。

2.  **執行單詞計數 MapReduce 程式：**

    *   將 `WordCount.java` 檔案儲存到您的本地目錄。
    *   按照 `編譯和執行 Hadoop MapReduce 程式.md` 中的步驟，編譯 `WordCount.java` 檔案並建立 JAR 檔案。
    *   準備輸入資料 `input.txt`，例如：

        ```
        hello world
        hello hadoop
        hadoop spark
        ```

    *   將 `input.txt` 上傳到 HDFS：

        ```bash
        hdfs dfs -mkdir /input
        hdfs dfs -put input.txt /input
        ```

    *   執行 MapReduce 程式：

        ```bash
        hadoop jar WordCount.jar WordCount /input /output
        ```

    *   查看輸出結果：

        ```bash
        hdfs dfs -cat /output/part-r-00000
        ```

3.  **使用 Hadoop Streaming 執行 Python MapReduce 程式：**

    *   將 `mapper.py` 和 `reducer.py` 檔案儲存到您的本地目錄。
    *   準備輸入資料 `input.txt`，例如：

        ```
        hello world
        hello hadoop
        hadoop spark
        ```

    *   將 `input.txt` 上傳到 HDFS：

        ```bash
        hdfs dfs -mkdir /input
        hdfs dfs -put input.txt /input
        ```

    *   執行 Hadoop Streaming 程式：

        ```bash
        hadoop jar $HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.3.6.jar \
        -input /input \
        -output /output \
        -mapper mapper.py \
        -reducer reducer.py
        ```

    *   查看輸出結果：

        ```bash
        hdfs dfs -cat /output/part-00000
        ```

4.  **使用 HDFS 指令：**

    *   參考 `Hadoop HDFS 指令指南.md`，學習如何使用常用的 HDFS 指令。

5.  **整合 Hadoop 與 Spark：**

    *   按照 `Hadoop 與 Spark 整合指南.md` 中的步驟，下載和配置 Spark 3.5.0。
    *   編寫 Spark 程式，從 HDFS 讀取資料並進行處理。

6.  **使用 Spark MLlib 進行機器學習：**

    *   按照 `Hadoop 與 AI/機器學習應用案例.md` 中的步驟，下載 MNIST 資料集並轉換為 CSV 格式。
    *   將轉換後的 CSV 檔案上傳到 HDFS。
    *   執行 Spark MLlib 程式，進行 MNIST 手寫數字分類。