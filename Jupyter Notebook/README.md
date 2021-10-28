# Jupyter Notebook HPC

This is an HPC version of [Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/). The app runs on a single Stampede2 or Frontera compute node (depending on which supercomputer is specified in the Tapis system being used by the app). <br></br>


## Details

Jupyter Notebook HPC is an interactive app. This means that while Jupyter Notebook HPC is running on a compute node, the user can access the Jupyter Notebook interface in a web browser on their local machine.

During job runtime, Tapis produces an output file which contains:
* Output and warnings from the running script
* The URL for the Notebook session
* The password needed to log into the session

The user can view the output file's contents while the job is still running to get the URL and password. After copy-pasting the URL into the browser and providing the login password, the user can interact with Jupyter Notebook as normal until the job is manually stopped or it exceeds the maximum job runtime as specified in the app definition. <br></br>


## Using the Jupyter HPC App

Use the _app_definition.json_ file as a reference for creating the Jupyter HPC app. Simply download the file or copy its contents and [create the app](https://tapis.readthedocs.io/en/latest/technical/apps.html#creating-an-application).

If the user wants to use a specific system to run the app rather than a shared system, they can add an "execSystemId" key-value pair under the "jobAttributes" object. For example:

```
{
    ...,

    "containerImage": "tylerclemens/jupyter-v3:latest",
    "jobAttributes": {
        "execSystemId": <SYSTEM_NAME_HERE>
        "execSystemExecDir": "${JobWorkingDir}/jobs/${JobUUID}",
        
        ...
}
```
<br>


## Stopping a Jupyter Notebook HPC session

If the user wants to stop a Jupyter Notebook HPC session, they can delete the "delete_me_to_end_session" file located in the mounted directory. Deleting this file will interrupt the Jupyter kernel and cause the Tapis job to end.