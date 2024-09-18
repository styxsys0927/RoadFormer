# RoadFormer

This is the GitHub repository for the paper "RoadFormer: Road-Anchored Adversarial Dynamic Graph Transformer for Unlimited-Range Traffic Incident Impact Prediction", which is accepted by IEEE Big Data 2023.

## Dataset
The benchmark dataset can be found in the [Dropbox directory](https://www.dropbox.com/scl/fo/i307pqi72eeq64c1bfx9b/ADcx1eR0_gMSB8Z9vfiugh4?rlkey=sy59iwkinbf4k20h9cjlshycw&dl=0). 

Below is some information about the dataset:

### Incident-LA
| filename              | # cases | # sensors/roads | # timestamps                         | features         | shape               |
| --------------------- | ------- | --------------- | ------------------------------------ | ---------------- | ------------------- |
| graph_data_full.npy   | 5,668   | 1,663           | 18 (12 before the incident, 6 after) | speed, occupancy | (5668, 18, 1663, 2) |
| graph_label_full.npy  | 5,668   | 1,663           |	| eid, 5-min, rid, type_id, dists, <br>dur (s), q_len (m) |	(5668, 7)           |
| adj_sr.csv		        | /       | 1,663		        |                                      | 1 if a sensor is on the road, else 0	| (1663, 32) |
| adj_rr.csv		        | /       | 32		          |                                      | 1 if two roads intersect, else 0	| (32, 32) |
| adj_ss.npy		        | /       | 1,663		        |                                      | 1 if adj_sr @ adj_rr @ adj_sr.T > 0, else 0	| (1663, 1663) |
| sensors_dists.csv     | /       | 1,663	          |                                      | ID, dists, rid | (1663, 3) |

### Incident-SB
| filename              | # cases | # sensors/roads | # timestamps                         | features         | shape               |
| --------------------- | ------- | --------------- | ------------------------------------ | ---------------- | ------------------- |
| graph_data_full.npy   | 1,452   | 1,150           | 18 (12 before the incident, 6 after) | speed, occupancy | (1452, 18, 1150, 2) |
| graph_label_full.npy  | 1,452   | 1,150           |	| eid, 5-min, rid, type_id, dists, <br>dur (s), q_len (m) |	(1452, 7)           |
| adj_sr.csv		        | /       | 1,150		        |                                      | 1 if a sensor is on the road, else 0	| (1150, 28) |
| adj_rr.csv		        | /       | 28		          |                                      | 1 if two roads intersect, else 0	| (28, 28) |
| adj_ss.npy		        | /       | 1,150		        |                                      | 1 if adj_sr @ adj_rr @ adj_sr.T > 0, else 0	| (1150, 1150) |
| sensors_dists.csv     | /       | 1,150	          |                                      | ID, dists, rid | (1150, 3) |

Specifically, among the features in "graph_label_full.npy", "dur (s)" and "q_len (m)" are the temporal and spatial impact to be predicted, while the others are sample-level attributes that might assist impact prediction.

| feature name  | description |
| ------------- | ------------- |
| eid  | Event ID  |
| 5-min  | The first timestamp in this sample is the t-th five minutes from 09-01-2019 00:00:00.<br> E.g., this value is 0 for an incident that happened at 09-01-2019 00:00:01.|
| rid  | Road ID of the incident  |
| type_id  | Incident category ID |
| dists  | Distance of the incident from the start of the road.  |
| dur (s)  | Incident duration in seconds  |
| q_len (m)  | Queue length in meters  |

"sensors_dists.csv" denotes the relative distances from sensors to the beginning of the corresponding roads. 

| feature name  | description |
| ------------- | ------------- |
| ID  | Sensor ID defined by [PeMS](https://pems.dot.ca.gov/). You may find the sensors' metadata by these IDs.  |
| dists  | Distance of the sensor from the start of the road. |
| rid  | Road ID of the sensor.  |

To use the dataset, please cite

```
@inproceedings{sun2023roadformer,
  title={RoadFormer: Road-Anchored Adversarial Dynamic Graph Transformer for Unlimited-Range Traffic Incident Impact Prediction},
  author={Sun, Yanshen and Fu, Kaiqun and Lu, Chang-Tien},
  booktitle={2023 IEEE International Conference on Big Data (BigData)},
  pages={895--904},
  year={2023},
  organization={IEEE}
}
```
