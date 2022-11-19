// SOQL snippets that I use frequently as a Salesforce admin to retrieve data/metadata for an or. 

// Retrieve Queue Names

`SELECT Name, Id FROM Group WHERE Type = 'Queue'`

// Retrieve Profiles

`SELECT Name, Id, Profile.Name FROM User WHERE Profile.Name = ''`

// Dynamic Dashboards

`SELECT FolderName, Title FROM Dashboard WHERE Type = 'LoggedInUser' OR Type = 'MyTeamUser'`

// Query for Users based on Role

`SELECT Name, Id, Profile.Name FROM User WHERE UserRole.Name = '' and IsActive = TRUE`
