# Step 4. Post Processing

![Inference Implementation Architecture](/files/img/postProcessingGeneral.png)  
   
   
## Workflows Github Description
This github explores the fourth step in Building a RAG Enabaled Gen AI application.  Post processing is where we decide what to do with the llm answers. We need to validate teh answers returned are true and correct. We can do this in a number of ways, with a custom python consumer / producer or a series of Flink SQL statements.  In this example I will focus on the product recommendations.  We will use flink SQL to query an operational data store to determine if the store and product actually exist.  There are a few Steps to follow:   

   1. We obtain the llm response from the llm_ansers kafka topic through flink sql
   2. We query the current ODS product and store information where inventory count is greater than zero
   3. We perform an intersect on the results
   4. We provide the final answer in llm_answers_processed topic.
 
This github is a continuation of a previous github that showed how to get data from different data sources based on a reasoning agent.  Be sure to check it out as we are using the data generated there and all the way back in step 1 for vector searches in this github example. [Confluent-Kafka-Vector-Search-Workflows](https://github.com/brittonlaroche/Confluent-Kafka-Vector-Search-Workflows)   
   
Focusing on this retail example lets consider the following answers.

```json
{}
````  
   
In some cases we could query the product vector database.  In some cases we its easier just to hit an operational data store. In this example we will go against the operational data store using the fink SQL federated seach with an intersect against the llm_answers topic on store and product id to eliminate any store and product_id combination not in the ODS.
   
### Implementation Detail
![Workflows Genreral Architecture](/files/img/post_processing.png)  

## 4 Steps to Building a GenAI Application
There are 4 steps to building a GenAI Application and I have included a github for each step.    
The githubs (some still work in progress) are indexed here:   
Step 1. Data Augmenatation: [Confluent-Kafka-Vector-Encoding](https://github.com/brittonlaroche/Confluent-Kafka-Vector-Encoding)   
Step 2. Inference: [Confluent-Kafka-Vector-Search-Prompt-Inference](https://github.com/brittonlaroche/Confluent-Kafka-Vector-Search-Prompt-Inference)   
Step 3. Workflows: [Confluent-Kafka-Vector-Search-Workflows](https://github.com/brittonlaroche/Confluent-Kafka-Vector-Search-Workflows)   
Step 4. Post Processing: [Confluent-Kafka-Vector-Search-Post-Processing](https://github.com/brittonlaroche/Confluent-Kafka-Vector-Search-Post-Processing)   
   
