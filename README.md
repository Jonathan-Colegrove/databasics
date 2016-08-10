## Databasics

Fork this repository into your own github profile.

Before closing the homework assignment issue:

- Update this README as follows:
  - [ ] For each question (just after or below the question itself) include the SQL you wrote to generate the answer
  - [ ] For each question (just after or below the question itself) include the *answer* to the question asked.

- Also:
  - [ ] Commit the updated `store.sqlite3` database file
  - [ ] Include a link to your forked repo in the comments when closing the issue.


NOTE: To run sqlite with this database: `sqlite3 store.sqlite3`

NOTE: You may want to keep a backup of the `store.sqlite3` file in case you damage the file. *OR* you can use the command `git checkout store.sqlite3` to undo any changes to the database file since the fork or your last commit.

## Explorer Mode

- [ ] How many users are there?
    select count(id) from users;
      50

- [ ] What are the 5 most expensive items?
  select * from items order by price desc limit 5;

      id          title                category                    description                         price     
----------  -------------------  --------------------------  ----------------------------------  ----------
25          Small Cotton Gloves  Automotive, Shoes & Beauty  Multi-layered modular service-desk  9984      
83          Small Wooden Comput  Health                      Re-engineered fault-tolerant adapt  9859      
100         Awesome Granite Pan  Toys & Books                Upgradable 24/7 access              9790      
40          Sleek Wooden Hat     Music & Baby                Quality-focused heuristic info-med  9390      
60          Ergonomic Steel Car  Books & Outdoors            Enterprise-wide secondary firmware  9341    

- [ ] What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
    It does change, as it doesn't find a category = book / Book / "book" / "Book"

    select * from items where category like "%book%" order by price limit 1;
    id          title                    category    description                          price     
    ----------  -----------------------  ----------  -----------------------------------  ----------
    76          Ergonomic Granite Chair  Books       De-engineered bi-directional portal  1496


- [ ] Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
  select first_name, last_name
  from users, addresses
  where addresses.id = users.id
    and addresses.street = "6439 Zetta Hills"
    and addresses.city = "Willmouth"
    and addresses.state = "WY";

    first_name  last_name
   ----------  ----------
   Kyra        Kilback  

  Yes:  405 Zulauf Park  North Pascale OK  51657
  select * from addresses, users where users.first_name = "Kyra" and users.last_name = "Kilback" and addresses.street != "6439 Zetta Hills" and addresses.city != "Willmouth" and addresses.state != "WY" and addresses.user_id = users.id;

- [ ] Correct Virginie Mitchell's address to "New York, NY, 10108".
done.
    select * from users where first_name = "Virginie" and last_name = "Mitchell";  ---> ID = 39
    update addresses set city = "New York", state = "NY", zip = 10108 where id = 39;

- [ ] How much would it cost to buy one of each tool?
    select total(price) from items where category like "%Tool%";
    46477.0

- [ ] How many total items did we sell?
    select sum(quantity) from orders;
    2125

- [ ] How much was spent on books?
    select sum(price) from items, orders where category like "%Book%";
    22333857


- [ ] Simulate buying an item by inserting a User for yourself and an Order for that User.
    insert into users values(NULL, "Jonathan", "Colegrove", "472@mailinator.com")
    insert into addresses values (NULL, 51, "1000 Firefox Drive", "Pellston", "MI", 49769);
    insert into orders values (NULL, 51, 21, 1, "2016-01-03");

## Adventure Mode

- [ ] What item was ordered most often?
    select item_id, quantity from orders order by quantity desc limit 1;
      item_id     quantity  
      ----------  ----------
      66          10

- [ ] Grossed the most money?
- [ ] What user spent the most?
- [ ] What were the top 3 highest grossing categories?
