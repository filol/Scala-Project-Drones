# Project Kafka/Spark

## Instructions

Your project is to imagine drone/mobile IOT devices and create it's big data architecture.
Write your code in Scala.

You will have to think about company or NGO creating/selling/promoting IOT devices.
Example : a company selling autonomous transport bus to town halls.

All your devices will be sending regularly some status report as data (you'll chose the format and the communication means).

You will have to build a big data solution with two sides :

**A) Monitoring (Kafka)**
Almost in real times analyse the status of every devices and alert a user of a critical situation.
Example a bus is full of passengers or out of fuel, thus it's unable to provides a good service to passengers waiting at the next bus stop.

**B) Storing and analytics (Spark)**
Store all the data sent by every device and be able to answer questions like:

- In proportion to the whole number of devices is there more failing devices in the north hemisphere or the south hemisphere?
- Is there more failing devices when the weather is hot or when the weather is called?
- Among the failing devices which percentage fails because of low battery or empty fuel tank?

## Our Implementation

For this project we decided to work on a fleet of drones. We could be a company that takes care of filming vines so that, with the video data, the winegrower can make a quick analysis of the state of its vines.
Our goal is to collect information on our drones in real time and to process this information to predict super behaviors, breakdowns, drone losses, ...

## Important part

Attention, this project uses submodule git, after having clone the project you must launch these commands:

- `git submodule init`
- `git submodule update`

## Kafka part

#### Requirements

For this part, we need to have installed:

- kafka : version 2.12-2.1.0
- sbt (to compile scala project code)

#### 1. Launch zookeeper instance:

Go to your kafka folder (“kafka_2.12-2.1.0”) and enter the following command:

`bin/zookeeper-server-start.sh ./config/zookeeper.properties`

#### 2. Launch kafka (in another terminal):

Go to your kafka folder (“kafka_2.12-2.1.0”) and enter the following command:

`bin/kafka-server-start.sh ./config/server.properties`

#### 3. Create topic dronesinfos with a replication factor to 1 and a least 2 partitions (in another terminal).

Go to your kafka folder (“kafka_2.12-2.1.0”) and enter the following command:

`bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 2 --topic dronesinfos`

#### 4. Go to Kafka folder

`cd Kafka`

#### 5. Launch the Main file :

`sbt run`

2 options (2 main) at launch time are proposed:

- **Producer**: this program will send regular updates of 3 drones to the local kafka instance. The purpose of this program is to simulate the data sent by many drones at the same time
- **Consumer**: this program will fetch at regular intervals (each 3 seconds) updates of the 3 drones from the local kafka instance and write down (or update) 3 files: `drone_0.json`, `drone_1.json`, `drone_2.json` to the project root folder.

So In general we should launch both (producer then consumer) in 2 different terminals

Spark should use those 3 files to make statistics and calculations

## Spark part

## Authors

- Grégoire Monet
- Baptiste Perreaux
- François Dexemple
