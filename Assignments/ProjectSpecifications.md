# Trip Planner

<!-- Found this project from previous curriculum, I think it can work for this course -->

# Project Outline

The goal for this project is to build an iOS app that allows users to plan trips. Users can create trips and trips are defined by a collection of waypoints. Waypoints are represented by a geographic coordinate and a name. Users should be able to create, delete and modify trips.

The content the user creates in the app should be persisted using Core Data. The data should also be synchronized with a backend system that you should setup using Firebase or any other option of your preference. (Note: Firebase recommended for speed time and simplicity)

<!-- Makes sense to include the backend portion of the project? -->

# Data Model

- Trips have a name and a collection of waypoints.
- Waypoints have a name (the name returned from the Google Places API) and geographic coordinates.

# Feature Outline

- Create Trips by providing a Trip name
- Add Waypoints to trips by searching the Google Places API for a location name
- Display Waypoints on a map
- Remove Waypoints
- Remove Trips
- Persist all Trips and Waypoints using Core Data
- Save user settings using any simple persistence method of your preference. For example: distance metrics, currency selector, dark mode preference... these features don't need to work, you just want to demonstrate the case of saving simple data.

You should however implement at least one API call that successfully works together with your backend (e.g. only syncing new trips but not changes or deletions, or login in users)

# Screen Layout

Here are mockups of the individual screens the app should contain, including their connections to each other:

![image](TripPlanner_ScreenFlow.png)

Feel free to design nicer screens than shown in these mockups! They are primarily concerned with the functionality of each screen, not with the specific design or layout. Also, this is missing the settings screen.

## Screen Details

This section provides details for some of the more complex screens.

### Main Screen (List of Trips)

This screen should support deleting trips by using the iOS swipe-to-delete feature. Additionally you could add an *Edit* that puts the table view into edit mode; this provides the user with another way of deleting elements.

### Trip Detail Screen

The Trip Detail Screen shows the waypoints for a selected Trip within a Table View. If the trip doesn't have any waypoints yet it shows another view which has a button to add waypoints

This screen should support deleting waypoints by using the iOS swipe-to-delete feature. Additionally you could add an *Edit* that puts the table view into edit mode; this provides the user with another way of deleting elements.

### Add Waypoint Screen

This screen allows the user to search for waypoints. It displays the search results in a table view. The user can select an entry. The selected entry will be highlighted on the map. By using the *save* button, it should update the trip.

Stretch challenges

- Synchronize all Trips and Waypoints with your Server - this should include user authentication so that persisted data is user specific.  
- Use Keychain to store the user's password, maybe try the sync with iCloud feature.

## Project evaluation criteria

[Link to rubric](https://docs.google.com/document/d/19VNDmeijyo0FlcguhDO9PB5nDDoQcZpYF26WJODvB_I/edit?usp=sharing)
