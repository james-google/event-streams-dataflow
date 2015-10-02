# Lab: Build an Event Streams Pipeline with Pub/Sub, Dataflow and BigQuery

## Prerequisites

1. A Google Cloud Platform Account - if you don’t have a GCP project, please contact coordinators before the training.
2. [Install Google Cloud SDK](https://cloud.google.com/sdk/)
3. Software: Eclipse and JDK (Java development kit). Installation instructions [here](http://www.eclipse.org/downloads/packages/eclipse-ide-java-developers/marsr). 

## Lab Exercise 1: Hello World with Dataflow

In this first exercise, we'll configure a Hello World sample to ensure your Dataflow environment is up and configured properly. 

1. Read and execute instructions specified in [Cloud Dataflow Getting Started](https://cloud.google.com/dataflow/getting-started). 

2. Follow the following set of instructions for the [Dataflow SDK Eclipse Starter Project](https://cloud.google.com/dataflow/getting-started-eclipse) to use as a baseline Java project.

3. Once you've imported the project (ensure you test on both LOCAL and SERVICE run configurations), you should have the following output in your console:

![submitted job](https://cloud.google.com/dataflow/images/gs-job-status-done.png)<br/><br/>
4. After these steps are completed, create a Google Cloud Storage (GCS) bucket by navigating to [console.developers.google.com](https://console.developers.google.com) > then select **Storage** > **Cloud Storage** > **Browser** > then click **Create Bucket**.<br/><br/>
5. Provide the name of the staging bucket such as "dataflow-demo", etc (this will be used in the following examples) > then click **Create** with the default values.

#### Download Lab Files
The final step is to download the lab files required for building the WordCount and Traffic sensor pipelines. 

1. Either clone the repository to your local workstation via:

    ```
    $ git clone https://github.com/james-google/event-streams-dataflow.git
    ```
or
    
2. Download via this zipped [file](https://github.com/james-google/event-streams-dataflow/archive/master.zip), and extract to the folder of your choice.

## Lab Exercise 2: [optional] WorkCount SDK Example

The following example is based off of the Dataflow SDK example [here](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/tree/master/examples) and will serve to demonstrate the basic functionality of Google Cloud Dataflow, and act as starting points for the development of more complex pipelines.

### Word Count

In this second lab, we'll use the WordCount example included in the [SDK examples](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples), which computes word frequencies.  This example (along with others) are described in detail in the accompanying [walkthrough](https://cloud.google.com/dataflow/examples/wordcount-example).

[`WordCount`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/WordCount.java) introduces Dataflow best practices like [PipelineOptions](https://cloud.google.com/dataflow/pipelines/constructing-your-pipeline#Creating) and custom [PTransforms](https://cloud.google.com/dataflow/model/composite-transforms).

### Building and Running

1. Drag and drop the **WordCount.java** file from the downloaded lab files into the **source/main/java** folder within your starter project in Eclipse.

![WordCount.java](https://cloud.githubusercontent.com/assets/8822452/10249692/a6ffe084-68f4-11e5-85c1-2719bc37f207.png) <br/><br/>
2. Scroll down to **line 196** and explore how this simple pipeline reads from a file on GCS, tokenizes the text lines into individual words, and then performs a frequency count on each of those words.

![](https://cloud.githubusercontent.com/assets/8822452/10249927/fe1c3ec0-68f5-11e5-8737-e70c826db6cf.png)<br/><br/>
3. For a more detailed step-by-step walkthrough, check out the [WordCount Example Pipeline Tutorial](https://cloud.google.com/dataflow/examples/wordcount-example) on the Cloud Dataflow site.<br/><br/>
4. To run this example, **right-click** on **WordCount.java** > select **Run As** > **Run Configurations...**<br/><br/>
5. Select the **SERVICE** option in the left pane > then click **Search** under **Main class**. <br/><br/>
6. Type in **WordCount** and select the appropriate class > then **OK**.<br/><br/>
7. Next, select the **SERVICE** option > then the Arguments tab, and enter the following **Program arguments**:

![](https://cloud.githubusercontent.com/assets/8822452/10250675/4acbb328-68fa-11e5-80ce-5fc00a343aa0.png)<br/><br/>
8. After you enter the appropriate arguments, click **Run**.<br/><br/>
9. Navigate to [console.developers.google.com](https://console.developers.google.com) > then select **Dataflow** under the **Big Data** section to view the newly launched Dataflow job. <br/><br/>
10. Click on the first Dataflow job (ordered by most recent in decending order), and you can now view the status and progress of your Dataflow WordCount job.

![](https://cloud.githubusercontent.com/assets/8822452/10251339/f680e8f2-68fd-11e5-8fcc-fdbaa29bcf7a.png)<br/><br/>
11. Once your job completes, navigate back to your GCS staging bucket created earlier and view the output files from the completed Dataflow job.
![](https://cloud.githubusercontent.com/assets/8822452/10251339/f680e8f2-68fd-11e5-8fcc-fdbaa29bcf7a.png)<br/><br/>
12. This completes Lab exercise 1!



### Beyond Word Count

After you've finished running your first few word count pipelines, take a look at the [`cookbook`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/cookbook)
directory for some common and useful patterns like joining, filtering, and combining.

The [`complete`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/complete)
directory contains a few realistic end-to-end pipelines.

## Lab Exercise 3: Build out traffic sensor pipeline

In this third lab, we'll construct a traffic IoT sensor sample based on the SDK example [here](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/complete/TrafficMaxLaneFlow.java). This example will go beyond using just a static GCS input file, and instead will leverage Pub/Sub, Dataflow and BigQuery to demonstrate an end-to-end real world scenario. 

1. To begin, drag and drop the **TrafficMaxLaneFlow.java** file from the downloaded lab files into the **source/main/java** folder within your starter project in Eclipse.

2. 


## Lab Exercise 4: [optional] Connecting a UI to event streams
