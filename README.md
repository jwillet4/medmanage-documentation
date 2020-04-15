# MedManager

The MedManager tool is a tool for our clinical pharmacists to organize the medication research process. MedManage acts as a hub for each person to perform their tasks in an individually customized environment and track the medications to provide more safeguards and structure than previous efforts.

*For any questions, please contact Logan Willett at Logan.Willett@fdbhealth.com or message him through Teams*

## Table of Contents

- [Running the Application Locally](#running-the-application-locally)
- [Authentication](#authentication)
- [Pages](#pages)
  * [Home](#home)
      - [Sorting](#sorting)
      - [Filtering](#filtering)
      - [Element resizing](#element-resizing)
      - [Editing](#editing)
      - [Status progression](#status-progression)
      - [Ambiguous fields](#ambiguous-fields)
  * [Medicine List](#medicine-list)
      - [Sorting](#sorting-1)
      - [Filtering](#filtering-1)
      - [Editing](#editing-1)
      - [Status Progression](#status-progression)
      - [Pagination](#pagination)
      - [Viewing medicine history](#viewing-medicine-history)
  * [New Medicines](#new-medicines)
      - [Sorting](#sorting-2)
      - [Filtering](#filtering-2)
      - [Adding new medicines](#adding-new-medicines)
      - [Editing](#editing-2)
      - [Status progression](#status-progression-1)
  * [Medicine Map](#medicine-map)
      - [Navigating](#navigating)
      - [Cloning](#cloning)
  * [MedReview](#medreview)
  * [RxNav](#rxnav)
  * [Meducation Classic](#meducation-classic)
  * [MAT](#mat)
  * [Medicine Ordering](#medicine-ordering)
  * [Tools](#tools)
  * [Settings](#settings)
- [Editing Window](#editing-window)
- [Status Progression Window](#status-progression-window)
- [Medicine Autofilling](#medicine-autofilling)
- [Cloning](#cloning-1)
  * [What is cloning?](#what-is-cloning-)
  * [How does cloning work?](#how-does-cloning-work-)
- [Status Pathing](#status-pathing)
  * [What is status pathing?](#what-is-status-pathing-)
  * [Flow](#flow)
  * [Routing tables](#routing-tables)

## Running the Application Locally

To start the server, navigate to `MedManagerApp/src/services` and open `MedManager.sln` with Visual Studio. Once in the sln, find `IIS Express` in the top middle of the screen, hit the down arrow to its right, and change the deployment option to `MedManager2`. Click this option to start the server.

To start the Angular project, navigate to `MedManagerApp/src/client` and run the following commands:

    $ npm install
    $ ng serve

*Note: A pipeline is set up to automatically build and deploy the develop and master branches. When running `$ ng serve` certain errors will not cause the build to fail because it is running the development build. To ensure that the build doesn't fail in the pipeline, run the following command before merging into master or develop:*

    $ ng build MedManager2 --configuration=prod

## Authentication

MedManager uses Okta for authentication and user roles. To create a new account, contact Manuel Ramirez at MRamirez@fdbhealth.com and ask about adding a MedManager user. He will assign you an appropriate role, either being a standard user or an admin. An admin in the context of this tool, has the ability to progress the status of any medicine (not just the ones assigned to them) as well as access to all of the tools available, bypassing navbar customization.

## Pages

### Home

The home page is meant to act as the main page for any user to do the majority of their work in progressing medications. If the status pathing system is unfamiliar to you, read [Status Pathing](#status-pathing). This page accomplishes two main goals: visualizing the makeup of medications within the pathing system (how many medicines exist in each status and how many are assigned to the user) as well as presenting a workstation for the user to work with and view only the medicines assigned to them. 

##### Sorting

Sorting is done by clicking on the field names at the top of the grid. This will sort in descending, ascending, and default orders.
![enter image description here](https://s5.gifyu.com/images/sorting.gif)
##### Filtering

Filtering can be done one of two ways: The first is to select or type out a value within the filtering row just under the field titles. The second is to select elements withing the Kendo chart which will automatically populate the status filter with the appropriate status.
![enter image description here](https://s5.gifyu.com/images/filtering-home.gif)

##### Element resizing

The elements on the homepage can be resized if needed. This is done by dragging the divider found near the center of the page.
![enter image description here](https://s5.gifyu.com/images/resizing-home.gif)

##### Editing

Editing is performed by either double-clicking the row with the medicine you would like to edit or clicking the edit button on that row. This will open the edit window which is covered [here](#editing-window).
![enter image description here](https://s5.gifyu.com/images/edit-home.gif)

##### Status progression

Status progression is performed by selecting one or more medicines of the same status and clicking the `Update Status(es)` button at the top of the grid. Only medicines with the same status can be progressed together (a selected New medicine and Clone medicine will give an error). The status progression window is covered [here](#status-progression-window).

*Note: Medicines can be selected via normal file directory bindings:*
- *Selecting a single medicine is done by clicking a row.*
- *Selecting a range of medicines is done by selecting a row, holding shift, and clicking the row at the end of the range.*
- *Selecting multiple non-sequential medicines is done by holding the control key while clicking rows.*

![enter image description here](https://s5.gifyu.com/images/status-home.gif)

##### Ambiguous fields

There are just a handful of fields in the the home grid worth of explanation: 
- **DIS:** Days In Status. This is a count of how many days a medicine has remained in its current status.
- **DSC:** Days Since Creation. This is a count of how many days a medicine has existed since its initial creation.
- **Assigner:** This field contains the name of the last person who owned this medicine. They are the person who passed it off to you.
- **Priority** This is a number between 1 and 10 indicating the priority level of the medicine. Legacy medicines may not have a value but all medicines added through the MedManager system will be given a value.

### Medicine List

The medicine list is a general use page where any user of the MedManager tool can make changes to individual medications. If the status pathing system is unfamiliar to you, read [Status Pathing](#status-pathing). 

##### Sorting

Sorting is done by clicking on the field names at the top of the grid. This will sort in descending, ascending, and default orders.
![enter image description here](https://s5.gifyu.com/images/sorting-list.gif)

##### Filtering

Filtering is done by selecting or typing out a value within the filtering row just under the field titles. Another filtering option unique to the medicine list is to filter by customer. In the upper left of the grid is a filter that will trim the entries down to only medicines associated with the selected customer. This feature is configured to work alongside normal filtering and sorting.
![enter image description here](https://s5.gifyu.com/images/filter-list.gif)

##### Editing

Editing is performed by either double-clicking the row with the medicine you would like to edit or clicking the edit button on that row. This will open the edit window which is covered [here](#editing-window).
![enter image description here](https://s5.gifyu.com/images/edit-list.gif)

##### Status Progression

Status progression is performed by clicking the status progression button under the `Progress` field. When using the program usually, only medicines you own will be available to progress. If using the program in admin mode, you will have the option of progressing any medicine in the list. The status progression window is covered [here](#status-progression-window).
![enter image description here](https://s5.gifyu.com/images/status-list.gif)
##### Pagination

The grid of medicine can only display a certain number before hitting performance issues. Because of this, the grid uses pagination and only displays 100 medicines on each page. Moving to different pages is done by interacting with the buttons at the bottom left of the grid.
![enter image description here](https://s5.gifyu.com/images/pagination-list.gif)

##### Viewing medicine history

A log of medicine history is stored each time a new medicine is added to the database or is progressed to a new status. This log can be viewed by clicking the history button at the top right of the medicine list grid.
![enter image description here](https://s5.gifyu.com/images/history-list.gif)

### New Medicines

The new medicines page is a hub for those to add and work with medicines with the 'New' status. This page is limited to those who are possible owners of new status medicines. If the status pathing system is unfamiliar to you, read [Status Pathing](#status-pathing).

##### Sorting 

Sorting is done by clicking on the field names at the top of the grid. This will sort in descending, ascending, and default orders.
![enter image description here](https://s5.gifyu.com/images/sort-new.gif)

##### Filtering

Filtering is done by selecting or typing out a value within the filtering row just under the field titles.
![enter image description here](https://s5.gifyu.com/images/filter-new.gif)

##### Adding new medicines
The secondary way to add medicines in MedManager is to manually add them via the add new medicine button. This will open a window for the user to populate all of the fields of a medicine object handled by MedManager. Alternatively, the autofill feature may be used to use existing information to attempt to autofill the fields. More about the autofill functionality [here](#medicine-autofilling). Apart from the autofilling feature, the workings of the window are similar to the editing window, covered [here](#editing-window).
![enter image description here](https://s5.gifyu.com/images/add-new.gif)

##### Editing

Editing is performed by either double-clicking the row with the medicine you would like to edit or clicking the edit button on that row. This will open the edit window which is covered [here](#editing-window).
![enter image description here](https://s5.gifyu.com/images/edit-new.gif)

##### Status progression

Status progression is performed by selecting one or more medicines and clicking the `Progress Status(es)` button at the top of the grid. The status progression window is covered [here](#status-progression-window).

*Note: Medicines can be selected via normal file directory bindings:*
- *Selecting a single medicine is done by clicking a row.*
- *Selecting a range of medicines is done by selecting a row, holding shift, and clicking the row at the end of the range.*
- *Selecting multiple non-sequential medicines is done by holding the control key while clicking rows.*

![enter image description here](https://s5.gifyu.com/images/status-new.gif)

### Medicine Map

The medicine map is a tool that uses metrics generated from Meducation users to show statistics like: How often is this medicine queried by users? And how often do those medicines exist in our database? This allows our pharmacists to find commonly  requested medicines and automatically add them into our system either individually or in a clone batch. If the cloning system is unfamiliar to you, read [Cloning](#cloning-1). 

##### Navigating
The medicine map is split up into layers and has a tree-like structure. The first layer is based on the ingredients of medications. The next layer will specify the dose form name. The last layer contains specific medicines. A medicine with a blue background means that it already exists in the database and is going through the normal status paths. A medicine with a yellow background means that it exists as a Clone medicine and has not reached the Approved or Production statuses yet. To navigate through the tree, click the plus at the left of the rows to expand the grid or the minus at the left to condense the grid.

![enter image description here](https://s5.gifyu.com/images/nav-map.gif)

##### Cloning

Cloning is done by selecting a single med from the third layer of the medicine map. This medicine can be a medicine that already exists in the database (a blue medicine), or one that doesn't (a white medicine). The selected medicine will act as the head medicine for the selected clones. Click the `Batch Clone` button at the top right of the third layer grid to open the clone selection window. Here, the medicines you'd like to clone can be selected.

*Note: Medicines can be selected via normal file directory bindings:*
- *Selecting a single medicine is done by clicking a row.*
- *Selecting a range of medicines is done by selecting a row, holding shift, and clicking the row at the end of the range.*
- *Selecting multiple non-sequential medicines is done by holding the control key while clicking rows.*

![enter image description here](https://s5.gifyu.com/images/clone-map.gif)

### MedReview

The MedReview page contains an iframe to [MedReview](https://medreview.meducation.com/), which is a site the researchers use as a bucket to place all medications awaiting approval. This tool is also used to formally approve the medicines.

### RxNav

The RxNav page contains an iframe to [RxNav](https://mor.nlm.nih.gov/RxNav/), a government created tool that is supposed to act as a reliable source for tracking and receiving medicine information.

### Meducation Classic

The Meducation Classic page contains an iframe to [the original Meducation tool](https://dev.meducation.com). The clinical pharmacists generally use this just to check if verify a PMI is visible in production.

### MAT

The MAT page contains an download link to the MAT tool used by the clinical pharmacists during research. The MAT tool is used to assign phrases to medications. This tool has no direct interaction with the MedManager tool at this time.

### Medicine Ordering

Medicine Ordering is a tool created to replace the old process of manually reordering the ordinals of medicines sharing the same rxName when new medicines with that same rxName are added to the database. This process has you enter an rxName and search for it. These medicines are put into a Kendo Sortable object so you can drag and drop the medicines to reorder them. To save the new order, press the save button.

*Note: There is an experimental feature on this page for auto-sorting the medicines. This currently works in most cases, but will not work for packs and medicines who's requires division to compute.*
- *Example of auto-sort viable medicine: `Acetaminophen Disintegrating Oral Tablet 160 mg`*
- *Example of auto-sort enviable medicine: `Acetaminophen Oral Solution 160 mg/5 mL`*

### Tools

The Tools page contains an iframe to [a set of tools created for the clinical pharmacists](https://apioffice.meducation.com/v1.0/apps/index) used during the research of new medications. 

### Settings

The settings page currently holds only one option, to allow admins to swap into admin mode and progress the status of all medicines, not just the ones assigned to them. Because there is only one option within the settings page and that setting is only available to admins, the settings page itself can only be accessed via the navbar by admins. Going forward, if more settings are needed they should be added to the settings page and the following should be altered:

 1. The navbar component should be altered so the settings page is visible to everyone.
 2. Each element in settings should be viewable to only those with the appropriate permissions.

## Editing Window

The editing window is aptly named for its ability to edit medications. With this window, you can edit all the fields of medications needed for the processes on the MedManager tool. Most of the fields are self-explanitory; there are only a few that need additional explaining about what the field is or how its input device functions:
- **Input Boxes with Down Arrows:** The vast majority of these boxes are called combo boxes. These function the same as drop down boxes except with the added benefit of allowing the user to type in part of what they would like to select to filter the results shown in the drop down list.
- **Customers:** This is a multi-selection box. To use it, begin typing and select the customer from the drop down list that appears. As many customers can be added to each medicine as needed.
- **Due Date:** This calendar selection box will allow you to view a calendar and select a specific date via a GUI. The date can also be typed in and will also be auto-formatted. 
- **Generic:** If the user clicks the down arrow, no medicines will appear. MedManager will wait until three characters have been entered into the combo box and there is a half second delay in keystrokes. At this point, it will ask the server for medicines who's rxLbName contains the search string.
- **Why is the Confirm Button Not Working?:** There are checks in place to ensure information entered into the program is what is expected. If a field contains an illegal character, is unpopulated despite being a manditory fields, ETC, a red error message will appear under the field. Satisfy the requirement is gives you and the Confirm button should enable.

![enter image description here](https://i.ibb.co/SrqHcYH/edit.png)

## Status Progression Window

If the status pathing system is unfamiliar to you, read [Status Pathing](#status-pathing). This window is used to progress a medication along the status pathing system. This works by allowing the user to select the next status for the medication and the user it will be assigned to.

There are two modes for this window: Normal mode and Admin mode. When Admin mode is set from the settings, the user will have the ability to set medicines to any status and select anybody as the owner even if they are not an owner of that particular status.

![enter image description here](https://i.ibb.co/jhd1yNC/status.png)

## Medicine Autofilling

Medicine autofilling is a feature that exists as an API call. The rxCui of a medicine you'd like to autofill can be sent to this endpoint and it will use existing information from rxNav to attempt to find certain fields of the medicine. It is important to note that rxNav is incredibly inconsistent with the naming of certain medicines. The swapping of ingredient names and unpredictable salt-forms makes a programmatic solution, like is implemented, susceptible to failures. An autofilled medicine should always be checked for correctness.

*Note: Cloning uses the autofill feature, so all medicines added via the medicine map should be checked afterwards to ensure they have the correct information.*

## Cloning

### What is cloning?

Cloning is a feature within the MedManager tool that allows multiple medicines to be added at once and only requires one of those medicines to go through the full status pathing system. The types of medication we need to understand while talking about the cloning systems are **head** and **cloned** medicines. **Head** medicines are medicines that are added into the system as a medicine with the **New** status. This means that it will progress through the normal status pathing system (see [Status Pathing](#status-pathing)). This medicine will go through the normal research associated with adding a medicine. **Cloned** medicines do not go through the normal pathing system. They instead go through their own clone path and become reliant on the the approval of  the head medicine it is associated with.

### How does cloning work?

Cloning is done via the medicine map. When in the third layer of the map, the user can perform a [batch clone](#cloning). This will allow the user to select the **head** medicine and subsequently select the **cloned** medicines. This will [autofill](#medicine-autofilling) and add all of the selected medicines. The **head** medicine will be added to the *New* status and the **cloned** medicines to the *Clone* status. Each of the **cloned** medicines will be given a reference to the **head** medicine added in that cloning batch, linking these medicines.
The **cloned** medicines will sit in the clone status awaiting review. This review is meant to ensure that the medicine data generated via the autofill feature is correct and if not, fixing it. Once the medicine has the correct information, it can be progressed to the *Clone (A)* status. *Clone (A)* is meant to be a queue where **cloned** medicines wait for their associated **head** medicine to finish its process.
Meanwhile, the **head** medicine will go through the normal research and processing that medicines have traditionally gone through. Once this medicine is moved into the *Approved* status, all of the **cloned** medicines associated with it in the *Clone (A)* status will also be moved into *Approved* as well as relevant information from the **head** being copied to the **clones**.

*Note: The system is set up to handle issues related to **cloned** medicines and status edge cases. For example:*

- If the **head** is moved to *Approved* or *Production* before one of its **clones** is moved to *Clone (A)*, when the **clone** is moved to *Clone (A)* it will see that its **head** is in *Approved* or *Production* and automatically move itself to *Approved*.

## Status Pathing

### What is status pathing?

Status pathing is the routing of medicines through specified paths. Each medicine has a specific path it is currently assigned. The inspiration for this system was inspired by networking tables in networking and thus, have next hops and owners for each individual status and a default owner and default hop reminiscent of weights.
A hop is a representation of certain tasks that need to be performed in the process of adding a new medication. For example: The *New* status is for medicines that have just been created and await assignment to *Research* and a new owner. An owner is someone who is currently assigned a medication and is responsible for that statuses task and to move it to a new status and owner.
 These statuses can be viewed below, with either a [flowchart](#flow) or [a more comprehensive set of routing tables](#routing-tables).

### Flow

![](https://i.ibb.co/Wvyh77m/status-paths.png)

### Routing tables

|New             |Values                         
|----------------|-------------------------------
|Next Hops	 |`Research`
|Owners          |`Kim`            
|Default Hop     |`Research`
|Default Owner   |`Kim`

|Clone           |Values                         
|----------------|-------------------------------
|Next Hops	 |`Clone (A), Research`            
|Owners          |`Kim`            
|Default Hop     |`Clone (A)`
|Default Owner   |`Kim`

|Research        |Values                         
|----------------|-------------------------------
|Next Hops	 |`Research, New, Author`            
|Owners          |`Kim, Donna, Elaina`            
|Default Hop     |`Author`
|Default Owner   |`Donna`

|Author          |Values                         
|----------------|-------------------------------
|Next Hops	 |`Author, QA`            
|Owners          |`Kim, Donna, Elaina`            
|Default Hop     |`QA`
|Default Owner   |`Donna`

|QA              |Values                         
|----------------|-------------------------------
|Next Hops	 |`Review`            
|Owners          |`Kim`            
|Default Hop     |`Review`
|Default Owner   |`Donna`

|Review          |Values                         
|----------------|-------------------------------
|Next Hops	 |`Review, Rejected, Approved`            
|Owners          |`Chuck, Tom`            
|Default Hop     |`Approved`
|Default Owner   |`Tom`

|Rejected             |Values                         
|----------------|-------------------------------
|Next Hops	 |`Fixed`            
|Owners          |`Tom`            
|Default Hop     |`Fixed`
|Default Owner   |`Tom`

|Fixed           |Values                         
|----------------|-------------------------------
|Next Hops	 |`Review`            
|Owners          |`Dan`            
|Default Hop     |`Review`
|Default Owner   |`Dan`

|Clone (A)       |Values                         
|----------------|-------------------------------
|Next Hops	 |`Research`            
|Owners          |`Kim`            
|Default Hop     |`Research`
|Default Owner   |`Kim`

|Approved        |Values                         
|----------------|-------------------------------
|Next Hops	 |`Production`            
|Owners          |`Dan`            
|Default Hop     |`Production`
|Default Owner   |`Dan`

|Production      |Values                         
|----------------|-------------------------------
|Next Hops	 |`--`            
|Owners          |`Dan`            
|Default Hop     |`--`
|Default Owner   |`Dan`


