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