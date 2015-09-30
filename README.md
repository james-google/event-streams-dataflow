# Lab: Build an Event Streams Pipeline with Pub/Sub, Dataflow and BigQuery

## Prerequisites

1. [Install Google Cloud SDK](https://cloud.google.com/sdk/)
2. A Google Cloud Platform Account
3. Read and execute instructions specified in [Cloud Dataflow Getting Started](https://cloud.google.com/dataflow/getting-started). 
If you don’t have a GCP project, please contact coordinators before the training.
4. Software: Eclipse and JDK (Java development kit). Installation instructions [here](http://www.eclipse.org/downloads/packages/eclipse-ide-java-developers/marsr). 

## Lab Exercise 1: Hello World with Dataflow

1. Create a new Google Cloud Platform project: https://console.developers.google.com/project

2. Enable the Google Container Engine and Google Compute Engine APIs

3. Install gcloud: https://cloud.google.com/sdk/

4. Configure your project and zone: gcloud config set project YOUR_PROJECT ; gcloud config set compute/zone us-central1-f

5. Clone the lab repository to your workstation (or download zipped lab files [here]()):
    ```shell
    $ git clone https://github.com/evandbrown/jenkins-kube-cd.git
    ```

## Lab Exercise 2: [optional] WorkCount SDK Example

The following example is based off of the Dataflow SDK example [here](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/tree/master/examples) and will serve to demonstrate the basic functionality of Google Cloud Dataflow, and act as starting points for the development of more complex pipelines.

### Word Count

A good starting point for new users is our set of
[word count](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples) examples, which computes word frequencies.  This example (along with others are described in detail in the accompanying [walkthrough](https://cloud.google.com/dataflow/examples/wordcount-example).

1. [`MinimalWordCount`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/MinimalWordCount.java) is the simplest word count pipeline and introduces basic concepts like [Pipelines](https://cloud.google.com/dataflow/model/pipelines),
[PCollections](https://cloud.google.com/dataflow/model/pcollection),
[ParDo](https://cloud.google.com/dataflow/model/par-do),
and [reading and writing data](https://cloud.google.com/dataflow/model/reading-and-writing-data) from external storage.

1. [`WordCount`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/WordCount.java) introduces Dataflow best practices like [PipelineOptions](https://cloud.google.com/dataflow/pipelines/constructing-your-pipeline#Creating) and custom [PTransforms](https://cloud.google.com/dataflow/model/composite-transforms).

1. [`DebuggingWordCount`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/DebuggingWordCount.java)
shows how to view live aggregators in the [Dataflow Monitoring Interface](https://cloud.google.com/dataflow/pipelines/dataflow-monitoring-intf), get the most out of
[Cloud Logging](https://cloud.google.com/dataflow/pipelines/logging) integration, and start writing
[good tests](https://cloud.google.com/dataflow/pipelines/testing-your-pipeline).

1. [`WindowedWordCount`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/WindowedWordCount.java) shows how to run the same pipeline over either unbounded PCollections in streaming mode or bounded PCollections in batch mode.

## Building and Running

The examples in this repository can be built and executed from the root directory by running:

    mvn compile exec:java -pl examples \
    -Dexec.mainClass=<MAIN CLASS> \
    -Dexec.args="<EXAMPLE-SPECIFIC ARGUMENTS>"

For example, you can execute the `WordCount` pipeline on your local machine as follows:

    mvn compile exec:java -pl examples \
    -Dexec.mainClass=com.google.cloud.dataflow.examples.WordCount \
    -Dexec.args="--inputFile=<LOCAL INPUT FILE> --output=<LOCAL OUTPUT FILE>"

Once you have followed the general Cloud Dataflow
[Getting Started](https://cloud.google.com/dataflow/getting-started) instructions, you can execute
the same pipeline on fully managed resources in Google Cloud Platform:

    mvn compile exec:java -pl examples \
    -Dexec.mainClass=com.google.cloud.dataflow.examples.WordCount \
    -Dexec.args="--project=<YOUR CLOUD PLATFORM PROJECT ID> \
    --stagingLocation=<YOUR CLOUD STORAGE LOCATION> \
    --runner=BlockingDataflowPipelineRunner"

Make sure to use your project id, not the project number or the descriptive name.
The Cloud Storage location should be entered in the form of
`gs://bucket/path/to/staging/directory`.

Alternatively, you may choose to bundle all dependencies into a single JAR and
execute it outside of the Maven environment. For example, you can execute the
following commands to create the
bundled JAR of the examples and execute it both locally and in Cloud
Platform:

    mvn package

    java -cp examples/target/google-cloud-dataflow-java-examples-all-bundled-<VERSION>.jar \
    com.google.cloud.dataflow.examples.WordCount \
    --inputFile=<INPUT FILE PATTERN> --output=<OUTPUT FILE>

    java -cp examples/target/google-cloud-dataflow-java-examples-all-bundled-<VERSION>.jar \
    com.google.cloud.dataflow.examples.WordCount \
    --project=<YOUR CLOUD PLATFORM PROJECT ID> \
    --stagingLocation=<YOUR CLOUD STORAGE LOCATION> \
    --runner=BlockingDataflowPipelineRunner

Other examples can be run similarly by replacing the `WordCount` class path with the example classpath, e.g.
`com.google.cloud.dataflow.examples.cookbook.BigQueryTornadoes`,
and adjusting runtime options under the `Dexec.args` parameter, as specified in
the example itself.

Note that when running Maven on Microsoft Windows platform, backslashes (`\`)
under the `Dexec.args` parameter should be escaped with another backslash. For
example, input file pattern of `c:\*.txt` should be entered as `c:\\*.txt`.

## Beyond Word Count

After you've finished running your first few word count pipelines, take a look at the [`cookbook`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/cookbook)
directory for some common and useful patterns like joining, filtering, and combining.

The [`complete`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/complete)
directory contains a few realistic end-to-end pipelines.

## Lab Exercise 3: Build out traffic sensor pipeline

## Lab Exercise 4: [optional] Connecting a UI to event streams
