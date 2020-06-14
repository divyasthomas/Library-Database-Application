# Library-Database-Application

### Summary:
Designed and created a library database and an application using python and sqlite that allows users to find, borrow, return, donate items to the library and also find events, book rooms for events, register for events, volunteer for programs and ask for help from a librarian. The database also stores information of library personnel and library members.

### Project Specifications:

This database is designed for a university library but it could be used for any library. This library database has the following characteristics:

●	Library has Items. All Items in the library are of three kinds- books, periodicals (journals, magazines etc.), audiovisuals (CD, DVD, cassette, records etc). Items are identified by an item ID. Other information such as title of the item, date of when it was produced, shelf where it is located in the library (shelf_num), whether it is currently available or not, if loaned- then the last borrow date, due date and if returned- then last return date are also stored. Each item also belongs to one of 7 categories namely Books-nonfiction, Books-fiction, Journal, Magazine, Movies, Music, Others.

●	A book can also have an edition and can indicate if it is available online or not. It can be authored by many authors. Each author is identified by an author ID and has an author first and last name. 

●	Periodicals can have an issue number, volume and if it is available online or not. It can also have many publishers. Each publisher is identified by an ID and has a publisher name. 

●	Audiovisuals have a type of medium (DVD, cassette, records, other) and can have multiple artists and producers. Each artist is identified by an ID and has an artist name. Each producer is identified by an ID and has a producer name

●	A Person is identified by an ID and has a first name, last name, phone, email, address, gender (M/F/O), member type (since we are assuming a university library, this will be staff, faculty, undergraduate, graduate student), membership start date, membership end date and a Boolean value indicating whether the person is currently allowed to borrow items. A library personnel is a type of person who additionally has a job start date and end date

●	A person is automatically subject to fines if they do not return items by the due date. Fines are identified by a combination of item ID, person ID and the fine date. Fines also have the amount of fine due and the amount paid so far. A person can have many fines on the same item (borrowed and returned late many times) and many people can have fines on the same item. We have set our due date to be 2 months from the date borrowed and fines will be $2 per late day.

●	A person can also volunteer for the different volunteering activities offered by the library. Each volunteering opportunity is identified by a unique name and also belongs to one of 5 types of volunteering activity categories (Adult literacy tutoring, Adult numeracy tutoring, Home delivery of library materials, Teen volunteers, others). Each activity also has a short description and an estimated hours per week needed.

●	A person can also request help from the library. Each help request is identified by an ID.  A person can choose one of the 5 different types of help request categories to place their help request into, namely Research/finding items, Citation help, Writing, Event/workshop help, Others. Each help request is also accompanied by a brief description written by the user which gives the library more details about the request. The person can also choose to indicate whether the request is urgent or not.

●	A person can also donate items to the library. These might be added to the library in future after librarians review them (i.e they are not automatically added to library items). This is because maybe the item may not be in good condition or maybe too redundant. These new items are identified by an ID which is automatically assigned by the system. Each person can provide a title, short description and condition of the item. The person can also choose one of 7 categories namely Books-nonfiction, Books-fiction, Journal, Magazine, Movies, Music, Others to which the item most belongs. A person can donate many items but each item is donated by a specific person.

●	A person can register for many events happening in the library. Each event is identified by a unique event name, event type ( book related events, art shows, film screenings, workshops, networking, others), event description, event time, event date, recommended audience, a Boolean value indicating if the event has food or not, location and organizers. There is no fee to attend any event. 

●	 Each event is organized by a single organizer or multiple organizers. Each organizer is identified by a unique organizer email and has an organizer name. Each organizer can host multiple events.

●	Each library location (social rooms) is identified by a unique room number and the floor number of this room is also specified. Each event is held in a specific room.

●	A library user can borrow many items and return many items. But each item can only be borrowed and returned by one person at a time. 

### Entity Relationship Model and Proposed relations
An ERM of the database designed to reduce redundancies and anomalies can be found in the repository.

#### Proposed Relations (all in BCNF):
●	Item( item_id, cat_name, title, pub_date,availability, shelf_num, Person_ID<sup>FK-Person</sup> ,borrow_date, due_date,return_date)

●	Person(Person_ID, first_name, last_name, address1, address2, city, state, zipCode, phone, email,gender,member_type, mem_startdate, mem_enddate,allow_borrow)

●	Personnel(Person_ID<sup>FK-Person</sup>, job_startdate, job_enddate)

●	Books( item_id<sup>FK-Item</sup>, edition, online)

●	Periodicals(item_id<sup>FK-Item</sup> , issue, volume,online)

●	Audiovisuals(item_id<sup>FK-Item</sup> , medium )

●	Artist( artist_id, Artist_name)

●	Author( author_id, first_name, last_name)

●	Publisher(publisher_id, Publisher_name)

●	Producer(producer_id, Producer_name)

●	Volunteer_options(vol_name, vol_type, activity_desc ,hours_week)

●	Help(help_id, help_type, help_desc, is_urgent, Person_ID<sup>FK-Person</sup>)

●	Event( event_name, event_type, event_desc, date,  time, audience, has_food, room_number<sup>FK-Location</sup>)

●	Location( floor, room_number)

●	New_items( new_id,   new_title, Person_ID<sup>FK-Person</sup>, desc, cat_name, condition)

●	Organizer( organizer_name, organizer_email)

●	Register(event_name<sup>FK-Events</sup>, Person_ID<sup>FK-Person</sup>)

●	Volunteer(Person_ID<sup>FK-Person</sup>, vol_name<sup>FK-Voluntter_options</sup>)

●	Fines_on ( item_id<sup>FK-Item</sup> , Person_ID<sup>FK-Person</sup>, fine_date, fine_amount, fine_payed)

●	Items_of_author( author_id <sup>FK-Author</sup> , item_id<sup>FK-Item</sup>)

●	Items_of_Publisher( publisher_id <sup>FK-Publisher</sup> , item_id<sup>FK-Item</sup>)

●	Items_of_Producer( producer_id <sup>FK-Producer</sup> , item_id<sup>FK-Item</sup>)

●	Items_of_Artist(artist_id <sup>FK-Artist</sup>, item_id<sup>FK-Item</sup>)

●	Event_by_Organizer(organizer_email<sup>FK-organizer</sup>, event_name<sup>FK-Events</sup>)

### SQL Schemas, Populated Database
The proposed relations were created using SQLite and the database was populated using random data generators. Each table has at least 10 tuples. 

### Database Application
The database application in python which uses this database allows a library user to find, borrow, return, donate items, find and register for events and also seek help from the library. 

