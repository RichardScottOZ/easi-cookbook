# EASI Cookbook  <img align="right" src="resources/csiro_easi_logo.png">

A collection of notebooks and recipes that demonstrate larger data processing workflows in EASI.

Use the code in this repository as examples and guides to be adapted to your workflows.

## Overview

We regularly see that users can struggle to efficiently go from a development notebook (that works on a small area) to scaling up their workflow to work on a larger set of data or operationally. The main challenges we see are in:

- Efficient use of dask parameters tuned to the workflow
- Resilient and cost-effective workflows

## Common patterns for your package and code

Common patterns that occur for each data processing workflow:

1. Get work
   - Space, time, product and processing parameters
   - Select batching and tiling options
   - Output is a list of work to do (number of batches)
1. Do work
   - Launch processes with each to do a batch
   - Select optional dask configuration

## Common patterns for large workflows

There are three main patterns that can be explored. The best solution will likely depend on your workflow and requirements.

### Jupyter Lab

Launch one dask cluster per process.

### Grid workflow

Job tiling with ODC code

### Argo

Group work into batches each of which is run by a single Argo worker.

- Can control the number of simultaneous Argo workers
- If an Argo worker dies then the batch will be restarted. In this case ensure yor code can skip work that was previously done.
- Each Argo worker can itself launch a dask cluster and a grid workflow, or any complex processing task.
