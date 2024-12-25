java c
Algorithms and Analysis
COSC 1285/2123
Assignment 1: Implementing and Evaluating
Data Structures for Maze Generation
1 Overview
In this assignment, you will implement a number of well-established data structures for developing a maze generation program and evaluate their performance to determine what would be the best data structure in different situations. This assignment aims to help crystallise the analytical parts of the course and familiarise you with certain data structures, how implementation decisions can have an influence on running times, and how to empirically evaluate different possible design choices (in this case, data structures).
2 Learning Outcomes
This assessment relates to 3 learning outcomes of the course which are:
• CLO 2: Compare, contrast, and apply key data structures: trees, lists, stacks, queues, hash tables and graph representations;
• CLO 4: Theoretically compare and analyse the time complexities of algorithms and data structures; and
• CLO 5: Implement, empirically compare, and apply fundamental algorithms and data structures to real-world problems.
3 Background
A maze is typically a 2D grid of cells and walls, an entrance and an exit. The aim is to find a path from the entrance to the exit. See Figure 1 for an example. There are strategies and algorithms to solve a maze, i.e., find such a solution path given a maze. There are also strategies and algorithms to generate a maze; in this assignment, we will focus on generation of mazes, however, the implementation for maze generation is already provided in the Python skeleton (detailed in Section 4) and you will need to only focus on data structures that represent mazes in our maze generation scenario. We are focused on perfect mazes, where there is always a path from entrance to exit (by the virtue that in a perfect maze, there is always a path from a cell in the maze to any other cell in the maze). In addition, in this assignment, we focus on 2D, square cell mazes, i.e., each cell has 4 sides. There is no standard way to reference the cells, hence we adopted the convention issued in Figure 1, with (0,0) denoting the bottom left cell, and columns increase as we travel to the right of the maze (page), and rows increases as we travel up the maze (page). In order to specify the entrances and exits, we have added one row above, and one row below the maze, and one column to the left, and one column to the right of the maze. This means the row below the maze is referenced as -1, the row above by 5 (if we have 5 rows in the maze), the additional column to the left of the maze by -1, and the column to the right by 5 (if we have 5 columns in the maze). This allows us to still be able to use the original indexing, i.e., (0,0) refers to the bottom left cell of the maze, but still able to reference the location of entrances and exits.
4 Assessment details
The assignment is broken up into a number of tasks, to help you progressively complete the project.

Figure 1: Sample 5 by 5 maze. The entrances are il-lustrated as arrows pointing towards the maze, and ex-its are illustrated as arrows pointing away from the maze. The cells of the maze are in-dexed from 0, and the row and column indices are drawn outside the maze. Note that the bottom left cell is (0,0), and top right cell is (4,4). This follows the convention that matplotlib follows (we use that for visualisation). Note the entrances are spec-ified as (0,-1) and (-1,1) and exits as (5,4) and (3,5).
Task A: Implement Mazes using Different Data Structures (6 marks)
In order to generate mazes, we need a way to represent them. In the assignment and this task, you will implement a Maze abstract data type using graphs. Your task is to complete the implementation of a number of sections in the provided Python skeleton code. The implementation of the maze using 2D arrays is provided as an example in the skeleton.
Data Structure Details
Mazes can be implemented using a number of data structures. We provide the imple-mentation of 2D arrays and you are required to implement two others:
• 2D Array. Each element in the 2D array represents a cell or a wall in a 2D (square, 4 sided, cell) maze.
You are required to implement the maze abstract data type using the following data structures:
• Graph (edge list). Edge list representation of a graph representing a 2D (square cell) maze. An edge list is a simple way to represent a graph. It consists of a list or array of all the edges in the graph. Each edge is represented as a pair of vertices that it connects.
• Graph (incidence matrix). Incidence matrix representation of a graph representing a 2D (square cell) maze. It is a matrix where rows correspond to vertices and

Figure 2: Sample graphs with 4 vertices and 4 edges.
columns correspond to edges. An entry in the matrix indicates whether a vertex is incident to an edge.
Example Consider the two graphs depicted in Figure 2. The edge list representation of these graphs are:
EG1 = {(A, B),(A, D),(B, C),(C, D)}
EG2 = {(A, C),(A, D),(B, C),(B, D)}
And the incidence matrix representations are as follows:

For the above two data structures, you must program your own implementation, and not use libraries, e.g., networkx or numpy. Have a look at our implementations using a 2D array for an initial idea about how to possibly go about it. In the provided code, we make use of a limited number of packages. Apart from these cases in the provided skeleton code and built-in data types such as lists, dictionaries and arrays, this can be considered as an invalid implementation and attract 0 marks for that data structure. If in doubt, please ask first!
Code Framework
We provide Python skeleton code (see Table 1) to help you get started and ensure we have consistent interfacing to run correctness testing. Table 1 also lists the files that you really need to modify/implement (in the description column). You need to complete the implementation of edgeListGraph.py and incidenceMatGraph.py. We have provided the code to construct and provide functionality of a maze in the graphMaze file. It is mostly generic, but does assume a certain way of implementing the maze using the two graph data structures. If that does not align with your approach, please feel free to modify
file                                                                                                                                                               description
mazeTester.py
Code that reads a configuration file then exe-cutes the generation using specified data struc-ture. No need to modify this file.
maze/maze.py
Abstract class for mazes. All implementations of a maze should implement the Maze class. No need to modify this file.
maze/util.py
Coordinates class, and other utlity classes and methods. No need to modify this file.
maze/graph.py
Abstract class for graphs. All graph implemen-tations should implement the Graph class. No need to modify this file.
maze/arrayMaze.py
2D array data structure implementation of a maze. No need to modify this file.
maze/graphMaze.py
Graph based data structure implementations of a maze. Modify if need to.
maze/edgeListGraph.py
Code that implements an adjacent list (for maze). Complete the implementation.
maze/incMatGraph.py
Code that implements an adjacent matrix (for maze). Complete the implementation.
maze/maze viz.py
Modified code used to visualise generated mazes using matplotlib. No need to modify this file.
generation/mazeGenerator.py
Abstract class for maze generators. No need to modify this file.
generation/recurBackGenerator.py
Implementation of the recursive backtracking maze generator. No need to modify this file.
README.txt
Please read this first, it mentions how to run the code. No need to modify this file.
Table 1: Table of provided Python skeleton files.
it, but please ensure the same functionality is still maintained and that you are able to generate mazes.
Please note that the first time you run this implementation, the two provided configu-ration files will use the array data structure as the representation of the maze. If you modify and use one of the configuration files intended for graphs, you may encounter errors because the graph implementations are currently incomplete. Don’t be alarmed by these errors as once the graph implementation is finalised, the program should be able to correctly output the graphs.
Note that for Task A, part of the assessment will be based on automated testing, which will feed a number of configuration files into your (completed) implementation of the provided Python skeleton. We will then check if the generated mazes are correct, e.g., whether they are perfect, have correct entrances and exits, didn’t go into infinite loops etc. We would like you to do some testing about this - if you look at the code, there is a method to test if the generated maze is perfect which is not implemented. This implementation won’t be part of your assessment, but it might be useful to consider how to implement it and perform. checks yourself as part of practicing code evaluation. Remember a perfect maze is one where any cell in the maze can reach any other cell, or another way to put it, there exists a path between any pair of cells in the maze. If you implement something to evaluate perfect mazes, please refrain from submitting it as part of your final code submission.
Notes
• If you correctly implement the “Implement me!” parts of the provided skeleton, you do not need to do anythi代 写COSC 1285/2123 Algorithms and Analysis Assignment 1Python
代做程序编程语言ng else to get the correct output formatting. mazeTester.py will handle this.
• We will run your implementation on the university’s core teaching servers, e.g., titan.csit.rmit.edu.au, jupiter.csit.rmit.edu.au, and saturn.csit.rmit.edu.au. If you develop on your own machines, please ensure your code compiles and runs on these machines. Discovering at the last minute that your code does not compile on these machines is something you would want to avoid. If your code does not run on these machines, we unfortunately do not have the resources to debug each one and cannot award marks for testing. Please note this carefully, this is a firm requirement.
• All submissions should be compiled with no warnings on Python 3.6.8 when com-piling the files specified in Table 1 - this is the default Python3 version on the Core teaching servers. Please ensure your code runs on the core teaching servers and with this version of Python. Please note this carefully, this is a firm requirement.
Task B: Evaluate your Data Structures (12 marks)
In this second task, you will evaluate your implemented structures both theoretically and empirically in terms of their time complexities for the different use case scenarios and different operations, e.g., removeWall(). Scenarios arise from different parameter settings for generating a maze.
Write a report on your analysis and evaluation of the different implementations. Consider and recommend in which scenarios each type of implementation would be most appro-priate. The report should be 5 pages or less, in font size 12. See the assessment rubric (Appendix A) for the criteria we are seeking in the report.
Theoretical Analysis
At first, you are to conduct a theoretical analysis of the performance. Given the height h and width w (in terms of number of rows and columns) of the generated maze, report the best case and worse case running time estimate in terms of the exact asymptotic complexity (Θ) of each of your graph implementations when executing updateWall() and neighbours(). You will also need to provide an example scenario and explanation on the best case and worse case running time estimates. This will help you when explaining your empirical analysis results. Put the results in the follow format of a table:
Theoretical Analysis
Operations                                                               Best Case                                                    Worse Case
updateWall()                                    [asymptotic complexity]                                   [asymptotic complexity]
                                                                        [example and explanation]                           [example and explanation]
neighbours()                                    [asymptotic complexity]                                   [asymptotic complexity]
                                                                        [example and explanation]                           [example and explanation]
Empirical Analysis
Typically, you may use real usage data to evaluate your data structures. However, for this assignment, you will write configuration file generators to enable testing over different scenarios of interest. There are many possibilities, hence to help you we suggest you consider the following factors.
• The dimensions of the maze.
• Data structure implementations.
Data Generation When generating different maze dimensions, you may want to write some configuration file generators (or generator directly within a copy of mazeTester.py). Due to the randomness of the data, you may wish to generate several datasets with the same parameters settings and take the average across a number of runs.
Note, you may be generating and evaluating a significant number of datasets, hence we advise you to get started on this part relatively early.
Task C: Video Interview (2 marks)
After the report and code is submitted, you will be asked to record your responses to a number of questions in Canvas. These questions will ask you about aspects of your implementation or report. You will have a set time to consider the questions, make a recording then upload that recording. More details will be explained closer to the due date.
5 Report Structure
As a guide, the report could contain the following sections:
• Theoretical Analysis of Data Structures: In this section, perform. a theoretical anal-ysis of the running time and complexities associated with different data structure implementations. Refer to Section 4 for more detail.
• Data and Experimental Setup Explanation: Describe your data and experimental setup. Briefly explain the parameter configurations used in your experiments, e.g., the range of maze dimensions. Provide insight into why you selected such range. You can use a paragraph or even a high-level pseudo code or figure. Also describe which approach(es) you decide to use for measuring the timing results.
• Evaluation of Data Structures: Analyze, compare, and discuss the results obtained from evaluating the data structures using the generated data. Explain why you observed these results. Consider using the known theoretical time complexities of each data structure’s operations to support your analysis.
• Summary: Conclude by summarising your analysis and providing recommendations. For a given range of maze dimensions, suggest which data structure is most suitable, e.g., “for this range of maze dimensions, I recommend to use this data structure because...”. Refer back to your previous analysis for context.
Please make sure to include your name and student ID as well as the statement on the first page of this document in your report.
6 Submission
The final submission will consist of three parts:
1. Your Python source code of your implementations. This must include all files, in-cluding the provided skeleton as well as any extra files you have created. Your source code should be placed into the same structure as the supplied skeleton code, and the root directory/folder should be named as Assign1-. Specifically, if your student number is s12345, when unzip Assign1-s12345.zip is executed then all the source code files should be in directory Assign1-s12345. We use automated testing and compilation, and the testing script. will expect this structure, so if is different, the script. may not be able to compile your code. So please make sure not to change the structure.
2. Your written report for part B in PDF format, called “assign1.pdf”. Place this pdf within the Python source file directory/folder.
3. Your data generation code. Create a sub-directory/sub-folder called “dataGen” within the Python source file directory/folder. Place your data generation code within that folder.
The final folder (consisting the source code, report and dataGen subfolder) should be zipped up and named as Assign1-.zip. E.g., if your student numbers is s12345, then your submission file should be called Assign1-s12345.zip, and when we unzip that zip file, then all the submission files should be in the folder Assign1-s12345.
Note: submission of the report and code will be done via Canvas. We will provide details regarding Task C closer to the submission deadline.
7 Assessment
The project will be marked out of 20.
The assessment in this project will be broken down into three parts. The following criteria will be considered when allocating marks.
Implementation (6/20):
While the emphasis of this project is not on programming, we would like you to maintain decent coding design, readability and commenting, hence commenting and coding style. will make up a portion of your marks. For a detailed breakdown of the implementation marks, please refer to the rubric available via Canvas.
Report (12/20):
The marking sheet in Appendix A outlines the criteria that will be used to guide the marking of your evaluation report1. Use the criteria and the suggested report structure (Section 4) to inform. you of how to write the report.
Video Interview (2/20):
This is a pass/fail assessment, and you’ll be assessed based on your ability to answer some questions about the code and report.
Late Submission Penalty:   Late submissions will incur a 10% penalty on the total marks of the corresponding assessment task per day or part of day late, i.e, 2 marks per day. Submissions that are late by 5 days or more are not accepted and will be awarded zero, unless special consideration has been granted. Granted Special Considerations with new due date set after the results have been released (typically 2 weeks after the dead-line) will automatically result in an equivalent assessment in the form. of a practical test, assessing the same knowledge and skills of the assignment (location and time to be ar-ranged by the coordinator). Please ensure your submission is correct (all files are there, compiles etc), re-submissions after the due date and time will be considered as late sub-missions. To avoid submitting late, make sure to complete and submit your assignments a bit ahead of the deadline, as the core teaching servers and Canvas can sometimes be slow. We strongly advice you submit at least one hour before the deadline. Late submissions due to slow processing of Canvas or slow Internet will not be looked upon favourly, even if it is a few minutes late. Slow processing of Canvas or slow Internet will require documentation and evidence submission attempts was made at least one hour before the deadline.





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
