---
title: SOQL Snippets
updated: 2022-09-13 20:36:50Z
created: 2022-08-01 15:32:45Z
author: Zen Newman
---

// Retrieve Queue Names

`SELECT Name, Id FROM Group WHERE Type = 'Queue'`

// Retrieve Profiles

`SELECT Name, Id, Profile.Name FROM User WHERE Profile.Name = ''`

// Dynamic Dashboards

`SELECT FolderName, Title FROM Dashboard WHERE Type = 'LoggedInUser' OR Type = 'MyTeamUser'`

// Query for Users based on Role

`SELECT Name, Id, Profile.Name FROM User WHERE UserRole.Name = '' and IsActive = TRUE`
