
# Create roll up models (WIP)

In this workshop we will look at the process of creating a roll up model. You typically think of rollups as hierarchies and trees. 

There are two basic rules associated with a rollup: 

* rollups consist of nodes
* every rollup has a root node. the root does not have a parent
* every node has a parent (unless it is the root node)
* all leaf nodes (the last node in any branch) are stores

There are two tasks involved in creating a rollup:

* create the rollup model
* add stores to the rollup model


Rollups, once deployed on the platform, are accessible to any application and through the platform API. This includes applications such as HotSchedules Reveal and HotSchedules Count.


## Use Case

You will create a simple rollup model and add stores to your model. In this example we will use the platform API to post the models we require. A CLI tool is available that support CSV import, but that is not covered in this workshop.


##Prerequisites

**To create the model you need** 

* Access to HotSchedules IoT Tools 
* Write access to the Rollup and StoreRollup types
* A text editor that can handle JSON files


## Understanding the data model 

There are two data types that you need to populate to create a roll up. The first describes the roll up structure (what each node is, what the path is and what the parent of the node is)



````
{
        "name": "uswest",
        "display_name": "West Coast",
        "description": "US West Coast Stores",
        "path": "::usnodes:",
        "parent": "usnodes"
    } 
````



## Populate the data model 







## Rollup structure

````
{
    "nodes": [{
        "name": "usnodes",
        "display_name": "United States",
        "description": "US stores",
        "path": "::",
        "parent": ""
    },{
        "name": "useast",
        "display_name": "East Coast",
        "description": "US East Coast Stores",
        "path": "::usnodes:",
        "parent": "usnodes"
    }, {
        "name": "uswest",
        "display_name": "West Coast",
        "description": "US West Coast Stores",
        "path": "::usnodes:",
        "parent": "usnodes"
    }, {
        "name": "uscentral",
        "display_name": "Central US",
        "description": "Central US stores",
        "path": "::usnodes:",
        "parent": "usnodes"
    }],
    "description": "Primary graph model",
    "name": "corporate",
    "display_name": "Sales Rollup"
}
````














For errors or feedback with any of these labs please contact support@hotschedules.com






