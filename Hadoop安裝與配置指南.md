# Hadoop 安裝與配置指南（Ubuntu）

本指南將說明如何在 Ubuntu 作業系統上安裝和配置 Hadoop 3.3.6 單節點偽分散式叢集。

**1. 安裝 Java**

由於您的環境中尚未安裝 Java，我們首先需要安裝 Java Development Kit (JDK)。Hadoop 需要 Java 8 或更高版本。

```bash
sudo apt update
sudo apt install openjdk-8-jdk
```

驗證 Java 安裝：

```bash
java -version
```

**2. 安裝 SSH**

Hadoop 需要 SSH 才能管理叢集節點。

```bash
sudo apt update
sudo apt install openssh-server
```

產生 SSH 金鑰：

```bash
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
```

驗證 SSH 安裝：

```bash
ssh localhost
```

**3. 下載 Hadoop**

從 Apache Hadoop 官方網站下載 Hadoop 3.3.6：

```bash
wget https://archive.apache.org/dist/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz
tar -xzf hadoop-3.3.6.tar.gz
sudo mv hadoop-3.3.6 /usr/local/hadoop
```

**4. 配置 Hadoop 環境變數**

編輯 `~/.bashrc` 文件：

```bash
nano ~/.bashrc
```

在文件末尾添加以下內容：

```bash
export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```

儲存並關閉文件。然後執行以下命令使變更生效：

```bash
source ~/.bashrc
```

**5. 配置 Hadoop**

Hadoop 的配置文件位於 `$HADOOP_HOME/etc/hadoop/` 目錄下。

*   **hadoop-env.sh**

    編輯 `hadoop-env.sh` 文件：

    ```bash
    nano $HADOOP_HOME/etc/hadoop/hadoop-env.sh
    ```

    設定 `JAVA_HOME` 變數：

    ```bash
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
    ```

*   **core-site.xml**

    編輯 `core-site.xml` 文件：

    ```bash
    nano $HADOOP_HOME/etc/hadoop/core-site.xml
    ```

    添加以下配置：

    ```xml
    <configuration>
        <property>
            <name>fs.defaultFS</name>
            <value>hdfs://localhost:9000</value>
        </property>
    </configuration>
    ```

*   **hdfs-site.xml**

    編輯 `hdfs-site.xml` 文件：

    ```bash
    nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml
    ```

    添加以下配置：

    ```xml
    <configuration>
        <property>
            <name>dfs.replication</name>
            <value>1</value>
        </property>
    </configuration>
    ```

*   **mapred-site.xml**

    複製 `mapred-site.xml.template` 文件並編輯：

    ```bash
    cp $HADOOP_HOME/etc/hadoop/mapred-site.xml.template $HADOOP_HOME/etc/hadoop/mapred-site.xml
    nano $HADOOP_HOME/etc/hadoop/mapred-site.xml
    ```

    添加以下配置：

    ```xml
    <configuration>
        <property>
            <name>mapreduce.framework.name</name>
            <value>yarn</value>
        </property>
    </configuration>
    ```

*   **yarn-site.xml**

    編輯 `yarn-site.xml` 文件：

    ```bash
    nano $HADOOP_HOME/etc/hadoop/yarn-site.xml
    ```

    添加以下配置：

    ```xml
    <configuration>
        <property>
            <name>yarn.nodemanager.aux-services</name>
            <value>mapreduce_shuffle</value>
        </property>
    </configuration>
    ```

**6. 格式化 HDFS**

```bash
hdfs namenode -format
```

**7. 啟動 Hadoop**

```bash
start-dfs.sh
start-yarn.sh
```

**8. 驗證 Hadoop**

瀏覽器訪問 `http://localhost:9870` 查看 HDFS 介面。

瀏覽器訪問 `http://localhost:8088` 查看 YARN 介面。

**9. 停止 Hadoop**

```bash
stop-yarn.sh
stop-dfs.sh