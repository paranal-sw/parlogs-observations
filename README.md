# Parlogs-Observations Tutorials

## Dataset Summary

Parlogs-Observations is a comprehensive dataset that includes the Very Large Telescope (VLT) logs for Template Execution of PIONIER, GRAVITY, and MATISSE instruments when they used Auxiliary Telescopes (ATs). It also encompasses all VLTI subsystems and ATs logs. This dataset aggregates logs based on instruments, time ranges, and subsystems, and contains template executions from 2019 in the VLTI infrastructure at Paranal. The dataset is formatted in single Parket files, which can be conveniently loaded, for example, with Pandas in Python.

This repository provides tutorials for the parlogs-observations dataset, available at:

* https://huggingface.co/datasets/Paranal/parlogs-observations
* Zenodo

## Install

We recommend to install a virtual environment to encapsulate the required libraries, but they are rather standard. 

```bash
python3 -m pip install --upgrade pip wheel
python3 -m venv env
source env/bin/activate

# Install requirements
pip3 install -r requirements.txt
```

## Supported Tasks and Leaderboards

The `parlogs-observations` dataset is a resource for researchers and practitioners in astronomy, data analysis, and machine learning. It enables a wide range of tasks focused on enhancing the understanding and operation of the Very Large Telescope Interferometer (VLTI) infrastructure. The following tasks are supported by the dataset:

- **Anomaly Detection**: Users can identify unusual patterns or abnormal behavior in the log data that could indicate errors or bugs. This is crucial in providing operaional maintenance to the VLTI.

- **System Diagnosis**: The dataset allows for diagnosing system failures or performance issues. By analyzing error logs, trace logs, or event logs, researchers can pinpoint and address the root causes of various operational issues.

- **Performance Monitoring**: With this dataset, monitoring the performance of the VLTI systems becomes feasible. Users can track and analyze systems to understand resource usage, detect latency issues, or identify bottlenecks in the infrastructure.

- **Predictive Maintenance**: Leveraging the dataset for predictive maintenance helps in foreseeing system failures or issues before they occur. This is achieved by analyzing trends and patterns in the log data to implement timely interventions.

## Observations at Paranal

At Paranal, the Very Large Telescope (VLT) is one of the world's most advanced optical telescopes, consisting of four Unit Telescopes and four movable Auxiliary Telescopes. Astronomical observations are configured into Observation Blocks (OBs), containing a sequence of Templates with parameters and scripts tailored to various scientific goals. Each template's execution follows a predictable behavior, allowing for detailed and systematic studies. The templates remain unchanged during a scientific period of six months, therefore the templates referred in parlogs-observations datasets can be considered as immutable source code.


## Data Structure and Naming Conventions

The dataset is organized into Parket files follow a structured naming convention for easy identification and access based on the instrument, time range, and subsystems. This format ensures efficient data retrieval and manipulation, especially for large-scale data analysis:

```
{INSTRUMENT}-{TIME_RANGE}-{CONTENT}.parket
```


Where:
- `INSTRUMENT` can be PIONIER, GRAVITY, or MATISSE.
- `TIME_RANGE` is one of 1d, 1w, 1m, 6m.
- `CONTENT` can be meta, traces, traces-SUBSYSTEMS, or traces-TELESCOPES.

Example files:
- PIONIER-1w-meta.parket
- GRAVITY-1m-traces-SUBSYSTEMS.parket

The "meta" file includes information about the template execution, while "traces" files contain event logs.

The exisiting files are shown in the table below:


| GRAVITY                   | PIONIER                   | MATISSE                   |
|---------------------------|---------------------------|---------------------------|
| GRAVITY-1d-meta.parket    | PIONIER-1d-meta.parket    | MATISSE-1d-meta.parket    |
| GRAVITY-1d-traces-SUBSYSTEMS.parket | PIONIER-1d-traces-SUBSYSTEMS.parket | MATISSE-1d-traces-SUBSYSTEMS.parket |
| GRAVITY-1d-traces-TELESCOPES.parket | PIONIER-1d-traces-TELESCOPES.parket | MATISSE-1d-traces-TELESCOPES.parket |
| GRAVITY-1d-traces.parket  | PIONIER-1d-traces.parket  | MATISSE-1d-traces.parket  |
| GRAVITY-1m-meta.parket    | PIONIER-1m-meta.parket    | MATISSE-1m-meta.parket    |
| GRAVITY-1m-traces-SUBSYSTEMS.parket | PIONIER-1m-traces-SUBSYSTEMS.parket | MATISSE-1m-traces-SUBSYSTEMS.parket |
| GRAVITY-1m-traces-TELESCOPES.parket | PIONIER-1m-traces-TELESCOPES.parket | MATISSE-1m-traces-TELESCOPES.parket |
| GRAVITY-1m-traces.parket  | PIONIER-1m-traces.parket  | MATISSE-1m-traces.parket  |
| GRAVITY-1w-meta.parket    | PIONIER-1w-meta.parket    | MATISSE-1w-meta.parket    |
| GRAVITY-1w-traces-SUBSYSTEMS.parket | PIONIER-1w-traces-SUBSYSTEMS.parket | MATISSE-1w-traces-SUBSYSTEMS.parket |
| GRAVITY-1w-traces-TELESCOPES.parket | PIONIER-1w-traces-TELESCOPES.parket | MATISSE-1w-traces-TELESCOPES.parket |
| GRAVITY-1w-traces.parket  | PIONIER-1w-traces.parket  | MATISSE-1w-traces.parket  |
| GRAVITY-6m-meta.parket    | PIONIER-6m-meta.parket    | MATISSE-6m-meta.parket    |
| GRAVITY-6m-traces-SUBSYSTEMS.parket | PIONIER-6m-traces-SUBSYSTEMS.parket | MATISSE-6m-traces-SUBSYSTEMS.parket |
| GRAVITY-6m-traces-TELESCOPES.parket | PIONIER-6m-traces-TELESCOPES.parket | MATISSE-6m-traces-TELESCOPES.parket |
| GRAVITY-6m-traces.parket  | PIONIER-6m-traces.parket  | MATISSE-6m-traces.parket  |

## Combining Files

Files from same instrument and within the same time range belong to the same trace_id. For instance, in the files:
- PIONIER-1w-meta.parket
- PIONIER-1w-traces.parket

The trace_id=10 in PIONIER-1w-traces.parket file corresponds to the id=10 in the meta file PIONIER-1w-meta.parket.

## Data Instances

A typical entry in the dataset might look like this:

```python
# File: PIONIER-1m-traces.parket
# Row: 12268
{
"@timestamp": 1554253173950,
"system": "PIONIER",
"hostname": "wpnr",
"loghost": "wpnr",
"logtype": "LOG",
"envname": "wpnr",
"procname": "pnoControl",
"procid": 208,
"module": "boss",
"keywname": "",
"keywvalue": "",
"keywmask": "",
"logtext": "Executing START command ...",
"trace_id": 49
}
```

## Data Fields

The dataset contains structured logs from software operations related to astronomical instruments. Each entry in the log provides detailed information regarding specific actions or events recorded by the system. Below is the description of each field in the log entries:

| Field       | Description                                                                                       |
|-------------|---------------------------------------------------------------------------------------------------|
| @timestamp  | The timestamp of the log entry in milliseconds.                                                   |
| system      | The name of the system (e.g., PIONIER) from which the log entry originates.                       |
| hostname    | The hostname of the machine where the log entry was generated.                                    |
| loghost     | The host of the logging system that generated the entry.                                          |
| logtype     | Type of the log entry (e.g., LOG, FEVT, ERR), indicating its nature such as general log, event, or error. |
| envname     | The environment name where the log was generated, providing context for the log entry.            |
| procname    | The name of the process that generated the log entry.                                             |
| procid      | The process ID associated with the log entry.                                                     |
| module      | The module from which the log entry originated, indicating the specific part of the system.      |
| keywname    | Name of any keyword associated with the log entry, if applicable. It is always paired with keywvalue |
| keywvalue   | Value of the keyword mentioned in `keywname`, if applicable.                                      |
| keywmask    | Mask or additional context for the keyword, if applicable.                                        |
| logtext     | The actual text of the log entry, providing detailed information about the event or action.      |
| trace_id    | A unique identifier associated with each log entry, corresponds to id in metadata table.  |


## Dataset Metadata

Each Parket file contains metadata regarding its contents, which includes details about the instrument used, time range, and types of logs stored. This is the format of a sample template execution in the metadata:

```python
# File: PIONIER-1m-meta.parket
# Row: 49
{
"START": "2019-04-03 00:59:33.005000",
"END": "2019-04-03 01:01:25.719000",
"TIMEOUT": false,
"system": "PIONIER",
"procname": "bob_ins",
"TPL_ID": "PIONIER_obs_calibrator",
"ERROR": false,
"Aborted": false,
"SECONDS": 112.0,
"TEL": "AT"
}
```

Where the fields are:

| Field     | Comment                                                  |
| --------- | -------------------------------------------------------- |
| START     | The start timestamp of the template execution in milliseconds |
| END       | The end timestamp of the template execution in milliseconds   |
| TIMEOUT   | Indicates if the execution exceeded a predefined time limit   |
| system    | The name of the system used (e.g., PIONIER)                    |
| procname  | The process name associated with the template execution       |
| TPL_ID    | The filename of the corresponding template file              |
| ERROR     | Indicates if there was an error during execution              |
| Aborted   | Indicates if the template execution was aborted (manually or because an error) |
| SECONDS   | The duration of the template execution in seconds             |
| TEL       | The class of telescope used in the observation, in this dataset it is only AT |


This structured format ensures a comprehensive understanding of each template's execution, providing insights into the operational dynamics of astronomical observations at Paranal.


## Citation
TBD

## Licensing
TBD
