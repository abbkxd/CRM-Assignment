<h1>Overview</h1>

The User Interaction Management System is a comprehensive software application designed to manage and track user activities, interactions, events, subscriptions, and facility bookings. The system focuses on maintaining accurate records of users, their memberships, and the various ways they interact with events, facilities, and other services. 


<h2>Features</h2>

User Management: Store and manage user details, membership types, and statuses.

Interactions Tracking: Record various user activities, such as event participation, ticket purchases, and facility usage.

Event and Facility Management: Track event details, ticket sales, participant lists, and facility bookings.

Subscription and Mailing List: Manage user subscriptions, including mailing list preferences and renewal details.

Visitor Tracking: Track visitor access to facilities with detailed visit information.


<h3>Progress</h3>

...

<h3>Requirements</h3>

**Install MySQl.Data from Nuget Package Manager in Visual Studio.**

**Code to run in SQl Server.**

```
CREATE DATABASE usercred; USE usercred;

CREATE TABLE users ( Id INT AUTO_INCREMENT PRIMARY KEY,
 Username VARCHAR(50) NOT NULL UNIQUE,
 PasswordHash VARCHAR(64) NOT NULL,
 Email VARCHAR(64) NOT NULL );

CREATE TABLE `useraddr` (
  `Username` varchar(100) DEFAULT NULL,
  `BuildingNo` varchar(10) DEFAULT NULL,
  `Strname` varchar(100) DEFAULT NULL,
  `City` varchar(50) DEFAULT NULL,
  `PCode` varchar(10) DEFAULT NULL);

CREATE TABLE `userinfo` (
  `Username` varchar(100) DEFAULT NULL,
  `FName` varchar(50) DEFAULT NULL,
  `LName` varchar(50) DEFAULT NULL,
  `DOB` date DEFAULT NULL,
  `PhoneNumber` varchar(15) DEFAULT NULL);

CREATE TABLE `payments` (
  `PaymentID` varchar(50) NOT NULL,
  `Username` varchar(100) DEFAULT NULL,
  `CardHolderName` varchar(100) NOT NULL,
  `CardNo` int(20) NOT NULL,
  `CVV` int(11) NOT NULL,
  `ExpiryNo` date NOT NULL,
  `CardType` varchar(50) DEFAULT NULL);

CREATE TABLE `user_interests` (
  `interest_id` int(11) NOT NULL,
  `username` varchar(50) DEFAULT NULL,
  `interest_tag` varchar(50) DEFAULT NULL);

ALTER TABLE `user_interests`
  ADD CONSTRAINT `user_interests_ibfk_1` FOREIGN KEY (`username`) REFERENCES `users` (`Username`) ON DELETE CASCADE;
COMMIT;

CREATE TABLE `usersubscription` (
  `SubID` varchar(255) PRIMARY KEY,
  `Username` varchar(255) NOT NULL,
  `SubscriptionType` varchar(255) NOT NULL,
  `Subdate` datetime NOT NULL);

CREATE TABLE Events (
    EventID VARCHAR(255)  NOT NULL,
    EventName VARCHAR(255) NOT NULL,
    EventDescp TEXT NOT NULL,
    EventDate DATE NOT NULL,
    EventTime TIME  NOT NULL,
    HostName VARCHAR(255) NOT NULL,
    TicketPrice INT NOT NULL
);

CREATE TABLE Members (
    member_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    subscription_type VARCHAR(50) DEFAULT 'Community Member',
    email VARCHAR(100) NOT NULL UNIQUE,
    ph_no VARCHAR(15)
);


CREATE TABLE UserInteractions (
    Interaction_ID VARCHAR(50) PRIMARY KEY,
    Username VARCHAR(50) NOT NULL,
    Interaction_Type VARCHAR(50) NOT NULL,
    Interaction_Date DATE NOT NULL,
    Interaction_Details TEXT,
    Engagement_Level VARCHAR(20),
    FOREIGN KEY (Username) REFERENCES Users(Username)
);

CREATE TABLE Participant (
    Participant_ID VARCHAR(50) PRIMARY KEY,
    EventID VARCHAR(50) NOT NULL,
    Username VARCHAR(50) NOT NULL,
    Attendance_Status VARCHAR(50) NOT NULL,
    FOREIGN KEY (EventID) REFERENCES Events(EventID),
    FOREIGN KEY (Username) REFERENCES Users(Username)
);



```

