# Lab: Build an Event Streams Pipeline with Pub/Sub, Dataflow and BigQuery

## Prerequisites

1. A Google Cloud Platform Account - if you don’t have a GCP project, please contact coordinators before the training.
2. [Install Google Cloud SDK](https://cloud.google.com/sdk/)
3. Software: Eclipse and Java 7 JRE/JDK (Java development kit). Installation instructions [here](http://www.eclipse.org/downloads/packages/eclipse-ide-java-developers/marsr).

#### Download Lab Files
The final step is to download the lab files required for building the WordCount and Traffic sensor pipelines. 

1. Either clone the repository to your local workstation via:

    ```
    $ git clone https://github.com/james-google/event-streams-dataflow.git
    ```
or
    
2. Download via this zipped [file](https://github.com/james-google/event-streams-dataflow/archive/master.zip), and extract to the folder of your choice.

## Lab Exercise 1: Hello World with Dataflow

In this first exercise, we'll configure a Hello World sample to ensure your Dataflow environment is up and configured properly. 

1. Read and execute instructions specified in [Cloud Dataflow Getting Started](https://cloud.google.com/dataflow/getting-started-eclipse). 

2. Once you've imported the project, you should have the following Pipeline arguments within Eclipse: <br/><br/>
<img width="782" alt="lab__build_an_event_streams_pipeline_with_pub_sub__dataflow_and_bigquery_-_google_docs" src="https://cloud.githubusercontent.com/assets/8822452/10541417/e45b4d20-73de-11e5-936e-9fc7b7d0e2e1.png"> 
<br/>
When the execution finishes, among other output, the console should contain the statement Submitted job: **"your_job_id"**.

3. After these steps are completed, create a Google Cloud Storage (GCS) bucket by navigating to [console.developers.google.com](https://console.developers.google.com) > then select **Storage** > **Cloud Storage** > **Browser** > then click **Create Bucket**.
4. Provide the name of the staging bucket such as "dataflow-demo", etc (this will be used in the following examples) > then click **Create** with the default values.<br/><br/>
5. You're now done with the first lab!


## Lab Exercise 2: [optional] WordCount SDK Example

The following example is based off of the Dataflow SDK example [here](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/tree/master/examples) and will serve to demonstrate the basic functionality of Google Cloud Dataflow, and act as starting points for the development of more complex pipelines.

### Word Count

In this second lab, we'll use the WordCount example included in the [SDK examples](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples), which computes word frequencies.  This example (along with others) are described in detail in the accompanying [walkthrough](https://cloud.google.com/dataflow/examples/wordcount-example).

[`WordCount`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/WordCount.java) introduces Dataflow best practices like [PipelineOptions](https://cloud.google.com/dataflow/pipelines/constructing-your-pipeline#Creating) and custom [PTransforms](https://cloud.google.com/dataflow/model/composite-transforms).

### Building and Running

1. Drag and drop the **WordCount.java** file from the downloaded lab files into the **source/main/java** folder within your starter project in Eclipse, on top of **"your.package.name"** package you created with the in Step 1 of Lab 1.
<br/>

![WordCount.java](https://cloud.githubusercontent.com/assets/8822452/10249692/a6ffe084-68f4-11e5-85c1-2719bc37f207.png) 

<br/>
_**NOTE**: You will need to update your package name in each class file from **“com.google.cloud.dataflow.starter”** to the package name you created when setting up the Eclipse Dataflow project in Step 1 of Lab 1._
<br/><br/>
2. Scroll down to **line 196** and explore how this simple pipeline reads from a file on GCS, tokenizes the text lines into individual words, and then performs a frequency count on each of those words.

![](https://cloud.githubusercontent.com/assets/8822452/10249927/fe1c3ec0-68f5-11e5-8737-e70c826db6cf.png)<br/><br/>
3. For a more detailed step-by-step walkthrough, check out the [WordCount Example Pipeline Tutorial](https://cloud.google.com/dataflow/examples/wordcount-example) on the Cloud Dataflow site.<br/><br/>
4. To run this example, **right-click** on **WordCount.java** > select **Run As** > **Run Configurations...**<br/><br/>
5. Next, select the **“Dataflow Pipeline”** option > then press the **“New”** button to create a configuration of the selected type: <br/><br/>
<img width="792" alt="lab__build_an_event_streams_pipeline_with_pub_sub__dataflow_and_bigquery_-_google_docs2 1" src="https://cloud.githubusercontent.com/assets/8822452/10541886/53a2d9ac-73e2-11e5-9ee9-24ca07569a39.png"><br/>
6. Click **“Search…”** button under the **Main** tab.<br/><br/>
7. Type in **"WordCount"** and select the appropriate class > then **OK**.<br/><br/>
8. Click the **“Pipeline Arguments”** tab, select the **“BlockingDataflowPipelineRunner”** option (this will allow us to run the pipeline in GCP), enter your **“Cloud Platform Project ID”** and specify the **“Cloud Storage Staging Location”** via the drop-down > then click **“Apply”**:<br/><br/>
<img width="794" alt="lab__build_an_event_streams_pipeline_with_pub_sub__dataflow_and_bigquery_-_google_docs2 2" src="https://cloud.githubusercontent.com/assets/8822452/10541890/5b4437dc-73e2-11e5-9228-4cde7ac44776.png"><br/>
9. After you enter the appropriate arguments, click **Run**.<br/><br/>
10. Navigate to [console.developers.google.com](https://console.developers.google.com) > then select **Dataflow** under the **Big Data** section to view the newly launched Dataflow job. <br/><br/>
11. Click on the first Dataflow job (ordered by most recent in decending order), and you can now view the status and progress of your Dataflow WordCount job.

![](https://cloud.githubusercontent.com/assets/8822452/10251339/f680e8f2-68fd-11e5-8fcc-fdbaa29bcf7a.png)<br/><br/>
12. Once your job completes, navigate back to your GCS staging bucket created earlier and view the output files from the completed Dataflow job.
![](https://cloud.githubusercontent.com/assets/8822452/10251809/7a6cb382-6901-11e5-981c-c39e264b66f7.png)<br/><br/>

### Beyond Word Count

After you've finished running your first few word count pipelines, take a look at the [`cookbook`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/cookbook)
directory for some common and useful patterns like joining, filtering, and combining.

The [`complete`](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/complete)
directory contains a few realistic end-to-end pipelines.<br/><br/>
13. You've now wrapped up Lab exercise 2...now onto the "real stuff"!

## Lab Exercise 3: Build out traffic sensor pipeline

In this third lab, we'll construct a traffic IoT sensor sample based on the SDK example [here](https://github.com/GoogleCloudPlatform/DataflowJavaSDK/blob/master/examples/src/main/java/com/google/cloud/dataflow/examples/complete/TrafficMaxLaneFlow.java). This example will go beyond using just a static GCS input file, and instead will leverage Pub/Sub, Dataflow and BigQuery to demonstrate an end-to-end real world scenario. 

1. To begin, drag and drop the following files into the source/main/java folder within your starter project in Eclipse, on top of the **"your.package.name"** package:
  * DataflowExampleOptions.java
  * DataflowExampleUtils.java
  * ExampleBigQueryTableOptions.java
  * ExamplePubsubTopicOptions.java
  * PubsubFileInjector.java<br/><br/>
_**NOTE**: You will need to update your package name in each class file from **“com.google.cloud.dataflow.starter”** to the package name you created when setting up the Eclipse Dataflow project in Step 1 of Lab 1._ <br/><br/>
2. We will now create a Pub/Sub topic in which our traffic sensor event injector code will publish traffic events.<br/><br/>
3. Go to your **Developer Console** > select **Big Data** > **Pub/Sub** > then click **New Topic**. Enter the desired name for the topic, then click **Create**.<br/>
<img width="562" alt="pub_sub_topics_-_james_demo_project" src="https://cloud.githubusercontent.com/assets/8822452/10254291/af417610-6910-11e5-9a34-f312b7d1f904.png"><br/>
4. Next, navigate to line 327 in the TrafficMaxLaneFlow.java file where you can see the pipleline creation code leveraged to inject Pub/Sub events via a traffic event stream (events are real traffic [sensor data](http://www.dot.ca.gov/dist11/d11tmc/sdmap/showmap.php) from San Diego freeways).<br/><br/>
5. For this example, the **TrafficMaxLaneFlowOptions** interface is setting the project up to pull known traffic sensor events from a shared GCS bucket, and you can download the CSV files to view the raw data. As you can see, compared to the WordCount lab this pipeline has options for streaming data from Pub/Sub, and on **line 338** we are using a utility class to set up our Pub/Sub topic as well as our desired output BigQuery table. <br/><br/>
6. Repeat steps 4-7 from Lab 2, this time selecting the **TrafficMaxLaneFlow.java** class, and update the run configuration parameters with the following:

```
 --streaming=true
 --bigQueryDataset=<yourdatasetname>
 --pubsubTopic=projects/<ENTER-YOUR-PROJECT-ID>/topics/<ENTER-TOPIC-NAME-STEP-3>
 --numWorkers=3
```
Once you've updated the arguments, and you've selected the appropriate class > then click **Run**.<br/><br/>
7. Similar to the first lab, navigate to **Dataflow** via the Developer Console, and select the **trafficmaxlaneflow-YOUR-INFO-HERE-injector** pipeline. This is the injector pipeline that is pulling each line from the San Diego traffic sensor CSV file from GCS, and is pushing each event directly into Pub/Sub via the topic we created earlier.<br/><br/>
8. Click on the **TextIO.Read** node in the Dataflow UI, and you'll see live statistics of Pub/Sub messages:
<br/><br/>
9. Click on the **Job Log** tab and you can expand each node to see how Dataflow is spinning up GCE instances to process the data pipeline. Toggle to **Detailed** mode and you can drill down even further. <br/><br/>
10. Now go back to your list of dataflow jobs and select your active streaming job. Click on the PubsubIO.Read node in the UI and note the **Elements Added** amount trickling in events from our injector pipeline.<br/><br/>
11. To view the output of your Dataflow pipeline, click on **BigQuery** in the Developer Console. <br/><br/>
12. Select the dataset already created from Dataflow via the name we passed as the 
```--bigQueryDataset=dataflow_demo``` parameter > click the new table created from Dataflow in the left panel > then click the **Query** Table button.<br/><br/>
13. Add a * for your select query statement to see if Dataflow has started to inject the event streams into your BigQuery dataset. Make sure and also select **Show Options** and de-select the **Use Cached** Results option to ensure our data is pulling the latest info for each query. <br/><br/>
14.  Click the **Run Query** button to execute the query. It may take a couple minutes for the first events to start showing up, but you will begin to see your events streaming into your BigQuery table. <br/><br/> 
15. You've now successfully built an end-to-end event stream data pipeline using Pub/Sub, Dataflow and Bigquery!

## Lab Exercise 4: [optional] Connecting a UI to event streams
1. Open up a web browser and navigate to the developer console for your project. Click the **Cloud Launcher** link on the left side of the screen.

2. On the Cloud Launcher screen, search for **LAMP**, and then choose **LAMP Stack (Google Click to Deploy)**.

3. On the **LAMP Stack** screen, click the Launch on Compute Engine button.

4. On the Click to **Deploy LAMP Stack** screen, leave all the settings as they are by default and click the Deploy LAMP Stack button. The deployment will take 2-3 minutes to complete.

5. Once the server has been deployed correctly you will be brought to a page that says **Your LAMP Stack deployment is ready**. On that page you will see the **External IP** for your instance. Click the external IP address which will bring up a prompt to enable HTTP traffic

6. On the pop-up window, check the box to **Allow HTTP traffic** and click the **Apply** button.

7. Connect to your instance by clicking the SSH link.
8. An SSH window will open. In that window, navigate to the /var/www/html folder with the following command: <br/>```cd /var/www/html``` 

9. Authenticate within your GCE VM by entering:
sudo gcloud auth login

10. Follow the instructions to open a browser for authentication > select your Google account and paste the authentication code in the VM shell window.

11. Set your default project by entering:
sudo gcloud config set project <YOUR-PROJECT-ID>

12. Run the following command to download the UI:
 sudo gsutil cp -r gs://gtc_event_stream/laneselector ./  

13. Now you will need to create client credentials for the UI. Start by navigating to the developer console, and under the **APIs & auth** link, click the **Credentials** link.

14. From the Credentials screen, click the **Add credentials** button and select **OAuth 2.0 client ID**. 

15. On the **Create client ID** page, select **Web Application**. When prompted, enter “Lane Selector Client” in the **Name** field. In the **Authorized Javascript** origins field, enter “http://INSTANCE_IP_ADDRESS” where INSTANCE_IP_ADDRESS is the external IP address from Step 5. Finally, click the **Create** button.

16. You will be prompted with information about your newly created OAuth client. Make a note of the client ID as you will need it in subsequent steps.
<img width="645" alt="4 16" src="https://cloud.githubusercontent.com/assets/8822452/10545751/3c7f5f00-73f8-11e5-843f-83b9bce90496.png"><br/><br/>
17. Go back to the SSH window for your instance from step 8. Open up the Nano editor to edit the index.html file in the laneselector folder you downloaded in step 9 with the following command: <br/>
```sudo nano /var/www/html/laneselector/index.html  ```
<img width="776" alt="4 17" src="https://cloud.githubusercontent.com/assets/8822452/10545752/3c8251ec-73f8-11e5-9181-2ac84f22a75e.png"><br/><br/>
18. The nano text editor will open. Scroll down the page until you find the **PROJECT_ID**, **CLIENT_ID**, and **DATASET_TABLE** JavaScript variables. Change the values of these three variables to match your project ID, the client ID you created in step 13, and the dataset and table name created by Cloud Dataflow. Hit Ctrl-x when finished and save the file when prompted. <br/>
<img width="793" alt="4 18" src="https://cloud.githubusercontent.com/assets/8822452/10545753/3c858dd0-73f8-11e5-9c36-0fa442bb251e.png"><br/><br/>
19. In a web browser on your local machine, go to http://INSTANCE_IP_ADDRESS/laneselector/index.html, where INSTANCE_IP_ADDRESS is the external IP address of your instance from step 5. You will be prompted to allow the application access to Google BigQuery. Click the Allow button and you should see the UI.<br/><br/>
<img width="809" alt="3 1" src="https://cloud.githubusercontent.com/assets/8822452/10545205/84e8b53c-73f5-11e5-8213-f54eee12f927.png">


## Clean up
These steps are important as you'll be charged for your active Dataflow jobs, BigQuery datasets and GCE instances leveraged for the UI lab.

1. Navigate to your **Developer Console** > select **Big Data** > **Cloud Dataflow**. Click on any job with an **Active** status > then click **Cancel job**.

2. Now click on **Storage** > **Cloud Storage** > **Browser**. Select the bucket you created for the Dataflow staging location and click **Delete**.

3. Navigate to **Compute** > **Compute Engine** > **VM Instances**. Select the **lamp1-lamp** (or whichever LAMP instance name you designated for your UI lab) and click **Delete**.

4. Go to **Big Data** > **Pub/Sub** > click the topic created via Lab 3, step 3 and click **Delete**.

5. To remove your BigQuery datasets, go to **Big Data** > click on the **BigQuery** link to view the BigQuery UI. Select the drop-down next to the **trafficmaxlaneflow_YOUR-INFO** dataset and select **Delete table**.


