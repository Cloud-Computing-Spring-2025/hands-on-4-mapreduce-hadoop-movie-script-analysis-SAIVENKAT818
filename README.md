# Hands-on #4: MapReduce : Movie Script Analysis

This repository is designed to test the Java-based MapReduce job to process a dataset of movie script dialogues and extract insights while using Hadoop Counters to track key statistics.

## Objectives

Your task is to analyze the movie script using Hadoop MapReduce and perform the following tasks:

1.⁠ ⁠Find the most frequently spoken words by characters.
2.⁠ ⁠Calculate the total dialogue length per character.
3.⁠ ⁠Extract unique words used by each character.
4.⁠ ⁠Introduce Hadoop Counters to track the following:
   
    Total number of lines processed.
   
    Total words processed.
   
    Total characters processed.

    Total unique words identified.

    Number of characters speaking dialogues.
   
The MapReduce program should process the movie script dataset and output the results in a structured format.

## Setup and Execution

### 1. *Start the Hadoop Cluster*

Run the following command to start the Hadoop cluster:

⁠ bash
docker compose up -d
 ⁠

### 2. *Build the Code*

Build the code using Maven:

⁠ bash
mvn install
 ⁠

### 3. *Move JAR File to Shared Folder*

Move the generated JAR file to a shared folder for easy access:

⁠ bash
mv target/*.jar input/
 ⁠

### 4. *Copy JAR to Docker Container*

Copy the JAR file to the Hadoop ResourceManager container:

⁠ bash
docker cp input/hands-on2-movie-script-analysis-1.0-SNAPSHOT.jar resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
 ⁠

### 5. *Move Dataset to Docker Container*

Copy the dataset to the Hadoop ResourceManager container:

⁠ bash
docker cp input/movie_dialouges.txt resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
 ⁠

### 6. *Connect to Docker Container*

Access the Hadoop ResourceManager container:

⁠ bash
docker exec -it resourcemanager /bin/bash
 ⁠

Navigate to the Hadoop directory:

⁠ bash
cd /opt/hadoop-3.2.1/share/hadoop/mapreduce/
 ⁠

### 7. *Set Up HDFS*

Create a folder in HDFS for the input dataset:

⁠ bash
hadoop fs -mkdir -p /input/dataset
 ⁠

Copy the input dataset to the HDFS folder:

⁠ bash
hadoop fs -put ./movie_dialouges.txt /input/dataset
 ⁠

### 8. *Execute the MapReduce Job*

Run your MapReduce job using the following command:

⁠ bash
hadoop jar /opt/hadoop-3.2.1/share/hadoop/mapreduce/hands-on2-movie-script-analysis-1.0-SNAPSHOT.jar com.example.controller.Controller /input/dataset/movie_dialouges.txt /output
 ⁠

### 9. *View the Output*

To view the output of your MapReduce job, use:

⁠ bash
hadoop fs -cat /output/*
 ⁠

### 10. *Output*

To view the output of your MapReduce job, use:

⁠ bash
hadoop fs -cat /output/<taskno.>/*
 ⁠

### 11. *Copy Output from HDFS to Local OS*

To copy the output from HDFS to your local machine:

1.⁠ ⁠Use the following command to copy from HDFS:
    ⁠ bash
    hdfs dfs -get /output /opt/hadoop-3.2.1/share/hadoop/mapreduce/
     ⁠

2.⁠ ⁠use Docker to copy from the container to your local machine:
   ⁠ bash
   exit 
    ⁠
    ⁠ bash
    docker cp resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/output/ input/output/
     ⁠
3.⁠ ⁠Commit and push to your repo so that we can able to see your output
