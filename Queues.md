# Queues
Queues are used for asynchronous workflows which help reduce request time for expensive operations. These do work such as periodic aggregation of data

## Types of Queues
Message queues - Message queues receive, hold, and deliver messages. If an operation is too slow to perform inline, you can use a message queue with the following workflow. This is good because user isn't blocked and the job is processed in the background.
<br>
An application publishes a job to the queue, then notifies the user of job status $\rightarrow$ A worker picks up the job from the queue, processes it, then signals the job is complete.
<br>
Task Queues - Receive tasks and their related data, run them, and deliver results. They can support scheduling and can be used to run computationally intensive jobsi n the background

## What happens when queues grow very long?
This is the job of Back Pressure. Back Pressure can limit the queue by either blocking them through not accepting new messages and sending them a response to send later. Then the server can send a message saying that the queue is back up again.
<br>
The idea of work stealing here can also be implemented. Suppose a server is overwhelmed but another is not. Then that server can steal some of the work from another server and process it. This works because modern NICs support parallel queues
