## The Problem
Consider a hotel booking system. 

When drafting the requirements we need to ask what stakeholders/users would there be? We know there will be relevant users for every stakeholder.

Requirements should be listed as user stories and acceptance criteria.

To do this we need to understand the business rules of the system: Who can do what function, and with what limits.

We also need to consider the boundary of the system, what bits will be handled by other actors etc.

![[system_boundary.png]]

The business rules in natural language could be:
- Guests can request a booking, only receptionist can confirm booking. Guest can cancel booking up to 3 days before stay. If after 3 days before stay a cancellation charge of 1 day’s stay is levied.
- Cleaning rota will be organized so that rooms that are booked for that day and need cleaning are cleaned first. Meal booking requests for special requirements have to be confirmed by the kitchen staff, before being confirmed to the guest. 
- Receptionist can see the name of the guests and their postcode but not other contact details, only the manager can see these, this is to maximize guest privacy. 
- Depending on current pandemic regulations room will be left unoccupied for 24 before being able to be cleaned and occupied again, to prevent virus transmission.

The full list of stakeholders/human users could be:
- Receptionist 
- Hotel owner
- Guest
- Tax inspector
- Accountant
- Marketing team
- Hotel cleaning staff
- Hotel manager

The non-human actors could be:
- Paypal
- Hotel.com
- Expedia
## Listing Requirements
We can start with listing requirements in simple, natural language and then create user-stories for each one.

So the list could be:
1. Search for hotel, room with given criteria, location, price, pool, air conditioning, pet friendly etc. (Guest)
2. Make booking request (Guest)
3. Confirm booking request (Receptionist)
4. Delete booking (Receptionist) 
5. Check guest in (Receptionist) 
6. Check current room occupancy (Cleaner) 
7. Mark room as cleaned (Cleaner) 
8. Generate guest checkout invoice (Receptionist) 
9. Allow secure login (Receptionist, Owner, Cleaning staff) 
10. Make meal booking request (breakfast, lunch dinner) with dietary requirements section (e.g. vegetarian, allergies) (Guest, Receptionist) 
11. Generate end of year account receipts (Accountant, tax inspector) 
12. Control marketing and loyalty scheme (discount for multiple stays) 
13. Generate cleaning rota (Cleaning staff) 
14. Show meal bookings (Waiting staff)

Which could then be translated into user stories such as:
	As a **Guest** I want to search for hotel, room with given criteria, location, price, pool, air conditioning, pet friendly etc. **So that** I can find a suitable accommodation for my trip.
Which could then be the basis for acceptance criteria such as:
	**Given** that there are rooms that are pet friendly, and the criteria is for pet friendly rooms **When** the search button is pressed **Then** display the rooms which are pet friendly

Use cases should also be generated so that they are of the following format
![[use_case_hotel_example.png]]

Any **non-functional requirements** should also be specified and labelled.

For example:
	NFR5: 
	 - The password must be at least 8 characters long and include both upper case and lower-case letters and a numerical digit 
	 - All usernames must be 10 characters
