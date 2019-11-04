# Hi-ClockFlow: Multi-Clock Dataflow Automation and Throughput Optimization in High-Level Synthesis

Tools of high-level synthesis (HLS) are developed to improve the accessibility of FPGAs by allowing designer to describe hardware designs in high-level language, e.g. C/C++. However, the source codes of general applications are not structured as canonical dataflow. Furthermore, clock frequencies are powerful parameters to improve dataflow throughput but currently commercial HLS tools limit themselves to single clock domain. Consequently, in order to benefit from the multiple-clock dataflow design, designers still suffer from manually analyzing the applications, partitioning the source code into modules, optimizing them with appropriate parameters and resource allocation, and finally interconnecting them.  

We analyze the impact of multiple clock domains for HLS designs and present Hi-ClockFlow, an automatic HLS framework. Hi-ClockFlow, which is implemented **[here](https://github.com/zslwyuan/Light-HLS/tree/master/Tests/Hi_ClockFlow)** as one of Light-HLS applications, can analyze the source code based on **[Light-HLS](https://github.com/zslwyuan/Light-HLS)**, our light weight HLS evaluation framework, explore the large design space, and optimize such parameters as clock frequencies and HLS directives in dataflow. By properly partitioning the source code of an application into parts with various clock domains,   Hi-ClockFlow can optimize the dataflow with imbalanced modules and speed up the performance under the specific constraint of resource.


If Hi-ClockFlow helps for your works, please cite our paper in ICCAD 2019 ^_^: 

    Hi-ClockFlow: Multi-Clock Dataflow Automation and Throughput Optimization in High-Level Synthesis. IEEE/ACM 2019 International Conference On Computer Aided Design (ICCAD) 



## Multi-Clock Dataflow DSE formulation

In the design space, the application is described as dataflow, which consists of multiple modules. Each module can has its own setting of HLS directives, i.e. parallelism, and clock frequency. Hi-ClockFlow will find the proper setting for each module to maximize the overall throughput of the application while meeting the resource constraint of the target FPGA device and the number constraint of clock domains.

The problem formulation is shown below:

<img src="https://github.com/zslwyuan/Light-HLS/blob/master/Images/hi-clockflow-formulation.png" width="800"> 

## Pushing-Relaxation Heuristic Algorithm 

Hi-ClockFlow solves this problem based on pushing-relaxation heuristic algorithm.

<img src="https://github.com/zslwyuan/Light-HLS/blob/master/Images/pushrelax_fig.png" width="800"> 
<img src="https://github.com/zslwyuan/Light-HLS/blob/master/Images/pushrelax_code.png" width="400"> 

The detailed codes are provided in **[here](https://github.com/zslwyuan/Light-HLS/blob/master/Tests/Hi_ClockFlow/Hi_ClockFlow.cc)**
Compared to common usage of Light-HLS, in the configuration file of Hi-ClockFlow, as **[an example](https://github.com/zslwyuan/Light-HLS/blob/master/Tests/Hi_ClockFlow/convs_settings/conv_config.txt)**, users need to specify the resource constraints and the initial clock for the modules in dataflow.

The example projects of multi-clock dataflow are provided via Google Drive since we go through the synthesis, placement and routing for easier evaluation.

