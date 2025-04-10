# Data local repository

In this folder, please, put the data that are related to the gestures 
collection process before you upload it to the database.

The directory should contain subdirectories each one having the name of the 
corresponding class.

For instance:

```
.
└── data/
    ├── class_A/
    │   ├── data_A_01.csv
    │   ├── data_A_02.csv
    │   └── ..
    ├── class_B/
    │   ├── data_B_01.csv
    │   ├── data_B_02.csv
    │   └── .
    └── class ...
```

Each document in the MongoDB database should have the following schema:

```json
{
  "data": {
    "acc_x": ["array", "of", "values"],
    "acc_y": ["array", "of", "values"],
    "acc_z": ["array", "of", "values"],
  },
  "label": "The label of the instance",
  "datetime": "MongoDB datetime object (it can be generated with the datetime.datetime.now() function"
}
```

Accordingly, if you are using gyroscope or both accelerometer and gyroscope, 
the following order and naming of the sensor keys should be defined:

* for gyroscope: `gyr_x`, `gyr_y`, `gyr_z` for the three axes
* for accelerometer **and** gyroscope: `acc_x`, `acc_y`, `acc_z`, `gyr_x`, 
`gyr_y`, `gyr_z` for the six axes