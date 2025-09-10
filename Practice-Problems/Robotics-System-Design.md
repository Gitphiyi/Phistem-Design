# Robotics Data Aggregation System
You have a fleet of humanoid robots deployed in the field. These devices generate large amounts of operational data. The data needs to be collected, transmitted back to a central service and aggregated so that downstream teams can use it for analytics and model training.

Design a system that enables robots to:
- Capture and locally store data during operation
- Upload data to the company when network connectivity is available
- Handle large, heterogeneous data types (structured logs, video streams, sensor time-series)
- Ensure data is aggregated, stored, and made queryable for ML training pipelines

### Scope Clarification
- Where are these robots deployed? What types of environments? Where in the world?
- Does the information need to be dessiminated amoung multiple locations where researchers are or is there only one place that needs to hold the information?
- How often can the robots send updated information back to the central service?
- Are the downstream teams writing anything back up to the robots? If so, how often are these robots updated?
- How can the data be split? Does it come back mostly as videos or is there also logs and etc?
- What is the necessary availability?
- How many robots are giving information?
Main Goal: Reliably collect telemetry, logs, and video from humanoid fleet and send to cloud so researchers can access for training
<br>
Functional Requirements:
- Store-and-Forward on robot
- Secure Upload
- Ordering per Device
- Hot Path Metrics/Alerts
- Searchable catalog for videos
- Lakehouse for ML
<br>
NonFunctional Requirements:
- Scalability for thousands of robots
- Reliability
- Security
- Observability

### Estimation
Assume 2000 robots.
- Telemtry: At 20Hz (20 times per second), with about 500B per message this is ~80kbps (kilo bits per second) per robot which is about 160 Mbps for the entire fleet
- Video: assuming 2.5Mbps/robot then it is ~5Gbps for the fleet

### Design API
- Robot should only have 2 HTTP Requests: POST video and POST telemetry. It should also have a GET Update for robot updates.
- Server: POST video to researchers. POST telemetry to researchers. POST update to robot. GET video and GET telemtry from robot.
- Researchers: GET video, GET telemetry, POST robot updates

### High Level Design
Edge robots: Capture data, buffer to store data before sending off (Ring buffer, LinkedList, Bounded Blocking Queue), HTTP to send data to Reverse Proxy Server
Reverse Proxy Server: Should have a load balancer to send to various databases. Consider also creating multiple Proxy servers that correspond to a distinct set of sharded databases
Database: A RBDMS database that is sharded based on device_id and proxy server that was used. Use key-value storage for video. There should be 2 databases one meant for video and the other meant for telemetry. Can consider using NoSQL database as the data isn't very structured, but SQL is very good as the researchers will probably be aggregating data a lot depending on timestamp and machine.
Data Logging: Consider logging Telemetry data in Prometheus as it is built for timestamped data. Then can use Grafana to help visualize the data

### Deep Dive
Database:
- Database is read dominated, so it should have a replication architecture. Databases can get up to 24TB RAM and Petabytes of storage. NICs are at 100-400 Gbps which is well over the video rate that the robot will send. Can send cache between DB and researchers as models will probably end up accessing the same videos multiple times. This can be a Redis key value storage where mostly everything is based on robot at a certain time.
Load Balancer: