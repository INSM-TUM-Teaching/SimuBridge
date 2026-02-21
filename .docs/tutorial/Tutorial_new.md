
# Tutorial
This tutorial document demonstrates the usage of SimuBridge on an example. We use the [Purchasing Example](https://github.com/INSM-TUM-Teaching/SimuBridge/tree/main/example_data/event_logs) event log in the tutorial.

 ## Start the project
When you open the tool you have three possibilities to start: create a new project, import an existing project from a .json file or select a project from already existing ones.  
<p align="center">
   <img src="./screenshots/Screenshot 1_1.png">
</p>

 In this tutorial, we start from scratch: Thus, we create an empty new project by entering new name and clicking the _Create project_ button.

 <p align="center">
   <img src="./screenshots/Screenshot 1_2.png" >

 It is possible either to create an empty simulation scenario and fill all parameters manually or to use an integrated process mining tool to automatically extract a BPMN model and the simulation parameters from an event log. 
 We will demonstrate the second option.
 Currently, the only available process mining tool is [Simod](https://github.com/AutomatedProcessImprovement/Simod).

 ## Process Mining & Simulation Scenario Creation

 To extract the simulation scenario and simulation parameters, we go to the process mining page by clicking  _Process Mining_ on the navigation sidebar or by clicking _Add from Process Mining_ on the _Overview_ Page. The miner requires an event log as an input parameter. The user can upload the event log by clicking on the _Upload new event log_ button. Additionally, the user has to choose a process mining tool from the available options. At the moment, the only integrated process mining tool is _Simod_.

 After settings are specified, we run the process miner by clicking _Start Mining_.

 <p align="center">
   <img src="./screenshots/Screenshot 1_3.png" >
</p>

SiumBridge will then confirm the successful start of the process mining run with a green pop-up at the bottom.  
Later, a similar pop-up indicates when the run terminated successfully. 
 <p align="center">
   <img src="./screenshots/Screenshot 1_4.png">
</p>

The .json and .bpmn file that are produced by Simod for a run are then listed under _Last Miner Run Output_. These files represent BPMN process diagrams and simulation parameters mined from the event log. You can download each of them by clicking on the respective list entry or Download all of them by clicking _Download files_ button. 

<p align="center">
   <img src="./screenshots/Screenshot 1_3_1.png">
</p>

To import a simulation scenario from the Simod output, we select one of the .json output files, which contain simulation parameters in Simod format, and a BPMN XML file that contains the mined process model. After clicking _Convert to Scenario_, we specify the scenario name "Ex1". 


 <p align="center">
   <img src="./screenshots/Screenshot 1_5.png">
</p>

## Scenario Overview

On the _Scenario_ page, we can now see the parameters of the scenario we created. These include general scenario parameters, resource parameters, and process-model-related parameters. To access this page, we click on _Scenario_ in the navigation sidebar. If we want to change the general simulation parameters or make a copy of the scenario with some modifications, we can click on _Edit_. 

 <p align="center">
   <img src="./screenshots/Screenshot 1_6.png">
</p>

Let us duplicate the scenario and make some changes afterward.
After clicking _Duplicate Scenario_  Ex1_copy is immediately created. Nevertheless, the original scenario is still shown. We can display the newly created scenario using a scenario switcher on the left sidebar. 
After selecting Ex1_copy, now at the _Scenario Overview_ page, we can see the parameters for Ex1_copy. 

Let us make some changes: We replace the scenario name Ex_copy with Ex1_1 and change the starting time to 00:00  by clicking the _Edit_ button. To save, we click _Save Changes_.

Let us now explore the other simulation scenario parameters: Resource and process model.

## Resource Parameters

Resource parameters provide an overview of resources involved in the business process and their timetables with their availabilities to work on process activities. To access resource parameters, we click  _Resource Parameters_ on the sidebar navigation panel. 

Each resource can be assigned to one or several roles. Resources are individual employees, machines, etc. that work on concrete process activity instances. Roles are a grouping mechanism to collect resources with similar capabilities and responsibilities.

 <p align="center">
   <img src="./screenshots/Screenshot 1_7.png">
</p>

We can get detailed information about a specific role or resource by clicking on it. 

 <p align="center">
   <img src="./screenshots/Screenshot 1_8.png">
</p>

The resources that belong to a role inherit the default timetable and costs of their role. However, we can customize these parameters for each resource individually. To do this, we click on the resource we want to edit, enter the new values and click _Save Changes_.


We can assign a resource to one or multiple roles, or leave it unassigned. To unassign a resource from a role, we uncheck the respective checkboxes under _Select Roles_. If a resource has no role, it will show up in the unassigned resource section. 

<p align="center">
   <img src="./screenshots/Screenshot 1_9.png">
</p>


We can investigate the timetable of each role by clicking on the _Timetable_ tab on the top bar.
<p align="center">
 <img src="./screenshots/Screenshot 1_10.png" >
</p>

The tools visualizes timetables by highlighting hours of the week where the respective resources are active. We can select the timetable to display by clicking on its name. By default, Simod names timetables like the corresponding roles. 

Timetables are defined by a set of items, i.e., continuous time intervals. 
We can select these items by clicking on the respective highlighted time. The currently selected item is highlighted in a different color and can be edited or deleted in the right side panel. 
New items can be added by clicking on unhighlighted hours, i.e., times not currently part of the timetable.


## Process Model Parameters

To display the BPMN process diagram of the business process, we click on _Model_ on the navigation sidebar. We can zoom in or zoom out the model by clicking on the "plus" or "minus" at the bottom of the screen or pressing Ctrl while scrolling. 
We can select process elements by clicking on the respective BPMN diagram element. 
This selects the element for editing and the tools display the element's parameters in the sidebar. 
Let us add one more role to the first activity. To do this, we expand the _Resources_ section, press _+_, and select the role's name. The changes are saved automatically.

<p align="center">
   <img src="./screenshots/Screenshot 1_11.png">
</p>


## Compare Scenarios
At the _Project Overview_ page, we can see all the scenarios that have been created. We can also duplicate and delete scenarios from this page. If we want to see how different scenarios are, we can use the _Compare Scenarios_ function.

To compare scenarios, we click on the _Compare scenarios_ button, select the scenarios we want to compare using the switches and click _Compare_.

<p align="center">
   <img src="./screenshots/Screenshot 1_13.png" width=300>
</p>

The compare view initially appears like the scenario overview for the currently selected scenario. 
However, parameters that are different in the other scenarios will be highlighted as buttons. 
The parameters that are the same in all scenarios will not be highlighted. 
We can click on a highlighted parameter to see its values in the other scenarios.
For example, the role cost we changed earlier is highlighted under _Resource Parameters - Quantity_

<p align="center">
   <img src="./screenshots/Screenshot 1_14.png">
</p>

## Run Simulation
After specifying a scenario and reviewing all parameters we can simulate it in the simulation view. We go there by clicking  _Simulation_ on the navigation sidebar.
In this view we can specify the scenario to simulate and the simulator to use. Currently, the only integrated simulation tool is [Scylla](https://github.com/bptlab/scylla). We start the simulation by clicking on the respective button.

<p align="center">
   <img src="./screenshots/Screenshot 1_15.png">
</p>

Like for the process mining view, run status is indicated with pop-ups, and console outputs as well as output files are displayed at the bottom under _Simulator Feedback_.

## Quality Informed Function (Frontend visualization) 

The _Quality Informed_ page provides a structured UI for assessing log quality and stability. 

As an input the page requires the user to configure several inputs before the assessment can start. You can upload or choose the event log from already available ones. After choosing activities for the assessment, minimum and maximum activity ranges need to be specified, and working hours need to be defined. 

<p align="center">
   <img src="./screenshots/Screenshot 1_16.png">
</p>


The result produces the tables which show the average score for specific group based on single parameter scores and on click provides detailed information about how the score was calculated. 

<p align="center">
   <img src="./screenshots/Screenshot 1_17 .png">
</p>

In addition each score field includes “jump button" with detailed inspection of parameter scores.

<p align="center">
   <img src="./screenshots/Screenshot 1_18.png">
</p>

## Sensitivity Analysis Layer (Frontend visualization) 
The Sensitivity Analysis layer extends SimuBridge with an analysis focused workflow that helps user understand how strongly different parameters affect key performance indicators. 

To start analysis you need to configure three inputs: Method (Sobol or Morris), KPI and Scenario. Each run stores: name, method, KPI, scenario, timestamp and action buttons for load or delete. 

<p align="center">
   <img src="./screenshots/Screenshot 1_19.png">
</p>

If users choose Sobol, the output includes: a ranked bar chart (importance + uncertainty), a details table with Sobol specific columns, an interaction heatmap visualizing S2 interaction and an interaction table listing the strongest interaction pairs. In the case Morris is chosen, the output includes a ranked bar chart and a detail table listing metrics and uncertainty related columns. 

<p align="center">
   <img src="./screenshots/Screenshot 1_20.png">
</p>

<p align="center">
   <img src="./screenshots/Screenshot 1_21.png">
</p>

## Help Guide 

If you need assistance at any stage of the project, you can click the small round "i" button in the top-right corner. The "How SimuBridge works" guide will open, where you can review all the necessary steps to successfully generate insights using the tool.

<p align="center">
   <img src="./screenshots/Screenshot 1_22.png" width= 300>
</p>

## Export Project 
Finally, we can download project file in json format by clicking _Download Project_ on the sidebar navigation menu. The file contains all created simulation scenarios and simulation parameters.
This allows us to share projects with other people.

If we want to resume working on the project at a later session, we do not need to export and download the project, as project data is persisted locally in the browser.  

