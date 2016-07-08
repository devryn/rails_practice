# Homework Answers

* How many users are there?
  50

  User.count

* What are the 5 most expensive items?
  "Ergonomic Steel Car", price: 9341,
  "Sleek Wooden Hat", price: 9390,
  "Awesome Granite Pants", price: 9790,
  "Small Wooden Computer", price: 9859,
  "Small Cotton Gloves", price: 9984

  item = Item.order(:price).last(5)

* What's the cheapest book?
  <Item id: 76, title: "Ergonomic Granite Chair", category: "Books", description: "De-engineered bi-directional portal", price: 1496>

  Item.where("category LIKE 'Books'").order(:price).first

* Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
  Corrine Little

  User.joins("INNER JOIN addresses ON addresses.user_id = users.id AND addresses.street = '6439 Zetta Hills'").first

  Other address: street: "54369 Wolff Forges",
  city: "Lake Bryon",
  state: "CA"

  Address.joins("INNER JOIN users ON users.id = addresses.user_id AND addresses.user_id = 40").last

* Correct Virginie Mitchell's address to "New York, NY, 10108".

  Address.joins("INNER JOIN users ON users.id = addresses.user_id").where("users.first_name = 'Virginie' AND state = 'NY'").update(city: 'New York', zip: '10108')

* How much would it cost to buy one of each tool?
  46477

  Item.where("category LIKE '%Tools%'").distinct.sum("price")

* How many total items did we sell?
  2125

  Item.joins("INNER JOIN orders ON orders.item_id = items.id").sum("quantity")
        Order.sum("quantity")

* How much was spent on books?
  180356

  Item.joins("INNER JOIN orders on orders.item_id = items.id").where("LOWER(category) LIKE '%book%'").sum("price * quantity")

  * Simulate buying an item by inserting a User for yourself and an Order for that User.
  User.create(first_name: 'Kate', last_name: 'Walters', email: 'kateisawesome@email.com')
  Order.create(user_id: User.where(last_name: 'Walters').pluck(:id).first, item_id: 14, quantity: 10)

* What item was ordered most often? Grossed the most money?
  Gorgeous Granite Car

  Item.joins("INNER JOIN orders ON orders.item_id = items.id").order("orders.quantity").last

  Awesome Granite Pants

  Item.joins("INNER JOIN orders ON orders.item_id = items.id").order("orders.quantity * items.price").last



<!-- * What user spent the most?

  User.joins("INNER JOIN items ON items.id = orders.item_id INNER JOIN orders ON orders.user_id = users.id").order(:price).first

* What were the top 3 highest grossing categories?

  Item.joins("INNER JOIN orders on orders.item_id = items.id").order("items.category").last(3) -->


# rails_practice
