Qiboconnection
==============

Qiboconnection is the python-based user interface for using qilimanjaro's services. With ``qiboconnection``, users can
provide the descriptions of what they want to get executed, check the status of the jobs created for said
executions, and retrieve the results for performing further analytics.



Using Qiboconnection
--------------------

Here we will provide some minimal examples for kick-starting with qiboconnection. A plethora of examples with more
detailed information can be found here (tbd).

For a first execution of a circuit, a user would need to:


Log into our system:

.. code-block:: python

    from qiboconnection.api import API
    from qiboconnection.connection import ConnectionConfiguration

    config = ConnectionConfiguration(
        username="username",
        api_key="api_key",
    )
    api = API(configuration=configuration)


Define your circuit:

.. code-block:: python

    from qibo.gates import M, X
    from qibo.models.circuit import Circuit

    circuit = Circuit(nqubits=1)
    circuit.add(X(0))
    circuit.add(M(0))

Check your available devices:

.. code-block:: python

    api.list_devices()

Select a device and send your execution, recovering the id of your job:

.. code-block:: python

    api.select_device_id(device_id=1)
    ids = api.execute(circuit=circuit)
    print(ids)

Check your jobs, and their status

.. code-block:: python

    jobs = api.list_jobs()
    jobs.dataframe

Download the full information of a given job, including the results, should it be finnished.

.. code-block:: python

    job = api.get_job(job_id=987)
    job.results

