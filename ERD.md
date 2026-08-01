Enum order_status {
  opening
  ordered
  received
  completed
}

Enum payment_status {
  unpaid
  paid
}

Enum menu_status {
  opening
  done
  outdated
}

Table users as U {
  username varchar [pk]
  hashed_password varchar [not null]
  full_name varchar [not null]
  phone_number varchar
  avatar_url varchar
  password_changed_at timestamptz [not null, default: '0001-01-01']
  created_at timestamptz [not null, default: `now()`]
}

Table sessions as S {
  id uuid [pk]
  username varchar [not null]
  refresh_token varchar [not null]
  is_blocked boolean [not null, default: false]
  expires_at timestamptz [not null]
  created_at timestamptz [not null, default: `now()`]

  indexes {
    username
  }
}

Table stores as ST {
  id int [pk, increment]
  name varchar [not null]
  address varchar
  description varchar
  type varchar
  phone varchar
  platform varchar [not null]
  shipping_fee numeric [default: 0]
  created_at timestamptz [not null, default: `now()`]

indexes {
  (name, id)
}
}

Table products as P {
  id int [pk, increment]
  store_id int [not null]
  name varchar [not null]
  price numeric [not null]
  available boolean [default: 'true']
  type varchar
  description varchar

  indexes {
    type
  }
}

Table menus as M {
  id int [pk, increment]
  title varchar [not null]
  
  created_by varchar [not null]
  status menu_status [default: 'opening']
  deadline timestamptz [not null]
  note varchar
  created_at timestamptz [not null, default: `now()`]

  indexes {
    id
  }
}

Table menu_stores {
  menu_id int [not null]
  store_id int [not null]

  indexes {
    (menu_id, store_id) [pk]
  }
}

Table participants as PA {
  id int [pk, increment]
  menu_id int [not null]
  username varchar [not null]
  payment_status payment_status [default: 'unpaid']
  joined_at timestamptz [not null, default: `now()`]

  indexes {
    (menu_id, username) [unique]
  }
}

Table orders as O {
  id int [pk, increment]
  menu_id int [not null]
  total_participants int [default: 0]
  total_orders int [default: 0]
  total_amount numeric [default: 0]
  status order_status [default: 'opening']
  created_at timestamptz [not null, default: `now()`]
}

Table order_items as OI {
  id int [pk, increment]
  order_id int [not null]
  participant_id int [not null]
  total_price numeric [default: 0]
  created_at timestamptz [not null, default: `now()`]

  indexes {
    order_id
    participant_id
  }
}

Table order_item_details as OID {
  id int [pk, increment]
  order_item_id int [not null]
  product_id int [not null]
  quantity int [not null, default: 1]
  size varchar
  topping varchar
  note varchar
  price numeric [not null]

  indexes {
    order_item_id
    product_id
  }
}

Ref: sessions.username > users.username [delete: cascade]

Ref: products.store_id > stores.id 

Ref: menus.created_by > users.username

Ref: menu_stores.menu_id > menus.id 
Ref: menu_stores.store_id > stores.id

Ref: participants.menu_id > menus.id 
Ref: participants.username > users.username

Ref: orders.menu_id > menus.id

Ref: order_items.order_id > orders.id [delete: cascade]
Ref: order_items.participant_id > participants.id

Ref: order_item_details.order_item_id > order_items.id [delete: cascade]
Ref: order_item_details.product_id > products.id