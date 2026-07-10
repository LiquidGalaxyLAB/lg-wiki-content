---
title: Creating Tab Bar for Liquid Galaxy Apps
contributor: Debanjan Naskar
date: 2025-03-17T17:11:41.685+00:00
---
## Overview
It has been conventionally seen that In Liquid Galaxy Apps, we generally use a Home Screen for all the necessary buttons to run our core App functionalities but for the Connection functionalities we still use a ‘gear-icon’ Settings.

We can substitute this by another design known as the Tab Bar.

This would look something like this:

![Image](https://raw.githubusercontent.com/devxdebanjan/Task4/refs/heads/main/apphome.png) App-HomeTab

![Image](https://raw.githubusercontent.com/devxdebanjan/Task4/refs/heads/main/appsettings.png) App-SettingsTab

To create something like this, you must have the following tree structure for your Flutter pages:

```bash
Home
 ├─── HomePage Tab
 └─── Settings Tab
```

Then in your Home you have to create a TabController object of length 2:

```bash
TabController tabController = TabController(length: 2, vsync: this);
```

Next you have to create two Tabs with the help of TabBar and TabBarView widgets:

In the TabBar widget, you define the whole style of the TabBar.

```bash
Container( 
            child: TabBar(
              indicatorColor: const Color.fromARGB(255, 105, 234, 110),
              indicatorSize: TabBarIndicatorSize.tab,
              indicatorWeight: 5.0,
              labelStyle: TextStyle(
                fontSize: 22.0,
                color: Colors.black,
              ),
              unselectedLabelColor: const Color.fromARGB(255, 121, 121, 121),
              controller: tabController,
              tabs: [
              Tab(text: "Home"),
              Tab(text: "Settings"),
               ], 
            ),
          ),
```

Whereas in the TabBarView widget, you have to link each Tab with a Flutter Class imported from the Homepage and Settings file in your project.

```bash
Expanded(
                child: TabBarView(
                  controller: tabController,
              children: [
                SubHome(),
                Settings(),
              ],
       ), 
),
```

And this is how we built the TabBar in the image shown at the starting of this entry. Following this you can change any aspect of this TabBar and use it for your own use case.
