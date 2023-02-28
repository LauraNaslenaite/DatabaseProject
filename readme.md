## Connection details
https://zeno.computing.dundee.ac.uk/2021-ac32006/team4/index.php \
  **Customer’s view:** \
    Username: felicia@claybrooks.co.uk\
    Password : felicia\
  **Staff’s view :**\
  Username: e1\
  Password: 123\
  **Manager’s view:**\
  Username: m1\
  Password: 123


## User guide
### a) Customer’s view and a homepage

![alt text](https://github.com/LauraNaslenaite/DatabaseProject/blob/main/2023-02-28_22h32_29.png)

The homepage allows any user to briefly get acquainted with the
company and its activities by clicking on “About” (1 in Fig.1) in the top
left corner or get the location of the main company’s branch by
selecting “Contact” (2 in Fig.1). Alternatively it can be done by clicking
on either of the images.

![alt text](https://github.com/LauraNaslenaite/DatabaseProject/blob/main/2023-02-28_22h32_34.png)

By scrolling down, as a default the most popular items sold are
displayed first (Fig.2.). Yet, a user is able to choose to see items of
specific category only (books, book accessories, gifts or stationery)
with a drop down list “Choose category” (3 in Fig.2). In addition, there
is an option to sort all items or of a particular category by their price in
either ascending or descending order (“Sort by”)(4 in Fig.2). It also
allows a user to have the books displayed based on their rating. To provide more functionality, a “Search by genres, ISBN, title” input field
(5 in Fig.3.) can be used to find books based on the genres or a
specific word in the title of a book or just simply by ISBN. \
\
By clicking on any of the items, a user can add it to his shopping cart,
but it requires him to be logged in. (6 in Fig.2.)\
\
A user can log in by clicking on the ‘’LOGIN‘’ button (7 in Fig.1.) at the
very top of the main page in the right corner. This leads him to another
page (Fig.3.) where a valid username and password must be entered
to access his customer’s account. After the individual has successfully
logged in, he can add items to the cart, check the profile details
including transactions made, and change a phone number. (Fig.4)
![alt text](https://github.com/LauraNaslenaite/DatabaseProject/blob/main/2023-02-28_22h32_42.png)

### b) Staff view

To access the staff’s view, a user needs to log in via the home page and then
enter a username which must start with “e” as it indicates a staff member.
After it was successfully done, there are several tables with particular
functionalities applicable for a staff displayed :\
\
**Staff**- Shows limited staff information. Requires the use of 2 database
tables (staff and address). Provides the functionality of searching and sorting
of staff information based on the given inputs: staffID, name, lastname and
sorting by all columns either descending or ascending.\
\
**Customers** - Shows limited customer information. Requires the use of
1 database table (customer table). Provides functionality of searching and
sorting of customer information based on given inputs: customerID, name,
email and sorting by all available columns either descending or ascending.\
\
**Item** - The table lists the content from 3 database tables(items, supplier
and author) and provides only one functionality to sort items by various fields
(quantity of the particular item in stock, book rating, price, category, supplier
and items ID ) in different orders (descending and ascending).\
\
**Transaction** - the table displays transactions made at different
branches with a sorting option based on ID.

### c) Managers view

All managers' usernames start with “m” which grants access to the manager's
account. After a successful login, there are several tables with particular
functionalities applicable for a manager displayed :\
\
**Staff** - The Table lists the content from 2 database tables (staff, and
address) and provides functionality of adding, deleting, searching and sorting
using various categories; Adding and deleting of staff details is a manager
only functionality. Address information is accessed via relationships via the
addressID’s of both tables.\
\
**Items** - The table lists the content from 3 database tables(items,
supplier and author) and provides functionalities such as to add(1 in Fig.5),
delete(3 in Fig.5), edit (2 in Fig.5) and sort by various categories in different
order. To improve the integrity of the database and its data, when an item is to
be inserted or edited, only mandatory input fields are required (for instance
when adding a product of a gift category, book related inputs are disabled).
Regarding the editing, a manager is able to change every field displayed in
the table except from items ID and its category.

![alt text](https://github.com/LauraNaslenaite/DatabaseProject/blob/main/2023-02-28_22h32_52.png)

**Suppliers** - lists the suppliers that provide items for sale, as well as
their contact information - phone number and address reference.\
\
**Sell/Buy Difference** - Lists each item from its given supplier, as well as
the purchase cost and the sale price of the item, as well as how many of the
items are currently the Bababook has in stock. Finally, the difference between
buying and selling price is calculated and the table is sorted from the highest
gain in sell/buy prices to the lowest.\
\
**Customer** - Lists all customer information. Only requires the use of
one database table (customer table). Allows for searching and sorting of
customer information. Adding and deleting customer information is at the
discretion of the customer and not the manager hence why these functions
were not implemented.\
\
**Transactions** - the table displays transactions made at different
branches with a sorting option based on ID.

## Technical Annex
### Administration
The access to different user views is insured by a username
meaning that if a username entered is an e-mail containing “@” ,
then a customer’s view is displayed, if a username starts with
“m” or “e” , either managers or employees' view respectively is
opened.\
\
Regarding indexing, every table contains a PRIMARY KEY and
most of them FOREIGN KEY which are all numeric. To ensure
the uniqueness of primary keys, an AUTO_INCREMENT is
applied, for instance when a new item is added to a table, a user
does not need to explicitly enter its ID.

## Advanced queries (min 4):
1) SELECT * FROM ITEM NATURAL JOIN SUPPLIER_ITEM WHERE itemID=$id;\

2) SELECT * FROM AUTHOR WHERE authorID= (SELECT authorID FROM
BOOK_AUTHOR WHERE itemID = $id);\

3) SELECT ITEM.itemID, ITEM.name as itemName, ITEM.category, ITEM.rating,
ITEM.description, ITEM.isbn, ITEM.genres,ITEM.publisher, ITEM.publicationYear,
ITEM.price, SUPPLIER_ITEM.supplierID, SUPPLIER_ITEM.supplied_quantity,
SUPPLIER..name as supplierName FROM ITEM JOIN SUPPLIER_ITEM ON
ITEM.itemID = SUPPLIER_ITEM.itemID JOIN SUPPLIER ON
SUPPLIER_ITEM.supplierID = SUPPLIER.supplierID order by item."
.$_POST['sortField'] ." ".$_POST['sortOption'];\

4) SELECT i.name as itemName, s.name as supplierName, si.cost_per_item as
buyCost, i.price as salePrice, si.supplied_quantity as stock, (price - cost_per_item)
as sellBuyDifferencePerItem
FROM item i, supplier s, supplier_item si
WHERE si.itemID = i.itemID AND si.supplierID = s.supplierID
ORDER BY sellBuyDifferencePerItem DESC;\

5) SELECT staff.staffID, staff.name, staff.lastname, staff.role, staff.phonenum,
staff.branchID, address.street, address.city, address.postcode FROM STAFF,
ADDRESS WHERE staff.addressID = address.addressID (with added searching and
sorting conditions)
