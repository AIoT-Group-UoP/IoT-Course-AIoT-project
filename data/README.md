# Data local repository

**In this folder, please, put the data that are related to the gestures 
collection process before you upload it to the database.**

The accelerometer and gyroscope data from the wristband are streamed over a 
Bluetooth connection and will be stored in CSV file format. Specifically, each 
of the CSV files contains the session performed by the user gesture, as well 
as a coding base that is defined based. The CSV files’ names, specifically, 
are determined in such a way that except for the annotation of the session 
with respect to a gesture ID. They also include other fields related to 
metadata from each session, which help in the later processing of the data 
each file includes. Additionally, this filename format provides a way to 
achieve a more accurate analysis of the collected data. Each field is separated 
by ”_” so it can be easily then extracted in the analysis process. The list 
below contains a description of each of the CSV file’s naming fields, in the 
order they follow, when saving a session. Each field corresponds to the 
appropriate metadata that is used later in the statistical analysis of the 
sessions and gestures that were collected, accordingly.

* Gesture ID: It refers to the gesture identifier. It could be the following: 
  * scroll-up-thumb, scroll-down-thumb, swipe-left-thumb, swipe-right-thumb 
  * scroll-up-index, scroll-down-index, swipe-left-index, swipe-right-index 
  * texting-two, texting-single 
* Hand: It denotes the hand where the participant wears the wristband, right 
or left hand. 0 stands for the right hand while 1 is for the left hand. 
* Sampling Frequency: The recording data sampling in Hz. 
* Sensor Type: This field lists the sensor whose recordings are contained in 
the current file, which in our case is the accelerometer and gyroscope, and 
can be  identified as”AccGyr”, “Acc”, or “Gyr” in the filename. 
* Primary Hand: If the hand that the participant wore the wristband is the 
primary hand the value 1 is inserted, or 0 if it is in the non-primary hand 
of the user (secondary hand). 
* Spontaneous: Corresponds to the movement’s impulsivity. The 0 value means 
that the gesture that is performed is not spontaneous, while it defaults to 1 
in case it is. 
* User ID: For each user, the participant ID is an incremental number, e.g., 
01, 02, 03. 
* Unique ID Hash: A unique ID is created to identify the particular 
session/gesture. It could be the MongoDB’s Object ID (_id).

The directory should contain subdirectories each one having the name of the 
corresponding class.

An example of a sessions instance could be:

`scroll-up-thumb_0_50_AccGyr_1_1_01_61964f51d11ec26c3bbde60b.csv`

As a guide, you can study the publication [3], which is available in the 
"References" section of the `README.md` file in the root folder.

Then, the data folder structure can have the following format:

```
.
└── data/
    ├──
    ├── scroll-up-thumb/
    │   ├── scroll-up-thumb_0_50_AccGyr_1_1_01_61964f51d11ec26c3bbde60b.csv
    │   ├── scroll-up-thumb_0_50_AccGyr_1_1_01_7982f51d11ec26c3be60b875.csv
    │   └── ..
    ├── scroll-up-down/
    │   ├── scroll-up-down_0_50_AccGyr_1_1_01_12432f51d11ec26c3b944jd0.csv
    │   ├── scroll-up-down_0_50_AccGyr_1_1_02_47563f51d11ec26c3bb4210k.csv
    │   └── .
    └── class ...
```

Each document in the MongoDB database should have the following schema, if you 
utilize ony the Accelerometer:

```json
{
  "_id": ObjectId("6984b3fa87abe7f4dff571aa"),
  "data": {
    "acc_x": ["array", "of", "values"],
    "acc_y": ["array", "of", "values"],
    "acc_z": ["array", "of", "values"]
  },
  "gesture_id": "The label of the instance",
  "hand": 0,
  "sr": 100,
  "sensor": "AccGyr",
  "primary": 1,
  "spontaneous": 1,
  "user": "01",
  "datetime": "MongoDB datetime object (it can be generated with the datetime.datetime.now() function"
}
```

If you are using gyroscope or both accelerometer and gyroscope, 
the following order and naming of the sensor keys should be defined:

* for gyroscope: `gyr_x`, `gyr_y`, `gyr_z` for the three axes
* for accelerometer **and** gyroscope: `acc_x`, `acc_y`, `acc_z`, `gyr_x`, 
`gyr_y`, `gyr_z` for the six axes
