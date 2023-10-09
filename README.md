# ICDS_FAQ

Why Incrasing number of cores or memory doesn't make my code run fast?

The relationship between memory per core and the running speed of a task in MATLAB, or any other computational task, can be influenced by several factors. It's important to understand that simply increasing memory per core doesn't necessarily lead to faster execution times, and the optimal memory setting can vary depending on the specific nature of the task and the hardware configuration. Here are some key points to consider:

1. Parallelization and Task Distribution: MATLAB tasks that are parallelized across multiple cores can benefit from having enough memory per core to accommodate the data and computations for each core. However, there's a balance to strike. If you allocate too much memory per core, it can lead to inefficient use of resources, as some cores may not fully utilize the available memory.

2. Memory Bandwidth: Memory bandwidth plays a crucial role in task execution speed. If the memory per core is too low, it can lead to frequent data transfers between main memory and CPU caches, which can slow down the execution. Conversely, if you allocate an excessive amount of memory per core, it may not fully utilize the available memory bandwidth.

3. Task-Specific Resource Requirements: The resource requirements of MATLAB tasks can vary widely. Some tasks may be more CPU-intensive, while others may require significant memory for large datasets or intermediate results. Optimizing memory per core depends on the specific needs of your task.

4. Resource Contention: When multiple users are sharing a cluster or server, resource contention can occur. Allocating excessive memory per core may lead to resource contention and slower execution times due to competition for resources.

5. Optimal Memory Setting: Finding the optimal memory setting often involves experimentation. You can start with a reasonable memory per core value and monitor the resource usage and task execution time. Adjust the memory setting up or down based on the observed performance. Tools like MATLAB's profiling and resource monitoring can help in this process.

6. Task Decomposition: Consider how your task is divided among cores. If the task is evenly divided, a balanced allocation of memory per core may be optimal. However, if some cores perform more intensive computations than others, you may need to allocate more memory to those specific cores.

7. Hardware Configuration: The underlying hardware, including CPU architecture, memory speed, and interconnects, can impact the relationship between memory and task performance. Different hardware may require different memory configurations for optimal performance.

In summary, the optimal memory per core setting depends on a combination of factors, including the specific task, hardware, parallelization strategy, and resource availability. Experimentation and monitoring are often necessary to fine-tune memory settings for optimal performance. It's important to strike a balance between providing enough memory to avoid bottlenecks and not allocating excessive memory that leads to inefficient resource utilization.

-------------------------------------------------------------------------------------

-------------------------------------------------------------------------------------
How to create new conda environment and use it?

We have a few suggestions to improve your workflow:

a) When running jobs, it's best not to use the submit node. Instead, request a dedicated compute node using the following command, adjusting the resources to match your requirements:

```
$ salloc -A open --nodes=1 --ntasks-per-node=1 --mem-per-cpu=64GB --time=02:00:00
```

b) We recommend creating a dedicated Anaconda environment for your work. You can include commonly used packages and easily install more in the future. Here's how to set it up (You may want to change the version of python):

```
$ module load anaconda3
$ conda create -n my_env python=3.8 numpy pandas matplotlib scikit-learn
$ source activate my_env
$ python3 Test.py
```

To install additional packages in the future, simply use:

```
$ conda install package_name
```

This approach allows you to manage and extend your Anaconda environment efficiently. 
