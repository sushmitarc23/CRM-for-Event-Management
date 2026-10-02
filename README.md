# CRM-for-Event-Management
Create an app- Event Management.
Added Custom Objects- Event, Attendee, Registration with standard objects Report and Dashboard.
Create a junction Relationship- Event(master)< Registration(detail)> Attendee(master).
On Event object- data type(Roll up summary), summarized object- Registration. summary type- COUNT. Field (Total Registered)
Validation Rule: 
    1.Event_Starting_Date- Error Condition Formula is Start_Date__c >= TODAY(). Where Error Message is Starting date must be in Past or Today.
    2.End_Date- Error Condition Formula is End_Date__c <= TODAY(). Where Error Message is End Date Must be in Future.
Record Triggerd Flow(Event Management): 
    Step1. On Registration object- When a record is created- Action and Related Records.
    Step2. Add Action(Send Confirmation Email)- Recipient Address(Triggering Registration_c> Attendee> Email)- Sender Email Address(Running User>Email)- Compose Email Content. Subject(Event Registration Confirmed)- Add Body({!Email_for_Confirmation})- Recipient ID({!$Record.Attendee__r.Id}).
Used Apex and Trigger to prevent duplicates (Name & Email). Also prevent Attendee to Register when the event capacity is on maximum. For bulkified Apex Trigger and governor limits used SOQL.
Maintain Role Hierarchy by doing setup in Profile and Security. Event Manager(CRUD), Event Viewer(R).
Create Report and Dashboard for instant view to avoid read Raw Data.