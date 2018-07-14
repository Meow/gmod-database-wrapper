Garry's Mod Database Wrapper
==================

A simple, easy-to-use database wrapper for Garry's Mod, supporting SQLite and mysqloo.

Usage
==================

First, include the wrapper into your project. It's done the regular Lua way:
```lua
local Database = include 'path/to/database.lua'
```

Then choose which database module do you want the wrapper to use:
```lua
Database:set_module 'sqlite'
```

Now connect to the database:
```lua
Database.connect('example.com', 'username', 'password', 'database', 3306)
```

Let's create a table:
```lua
create_table('my_table', function(t)
  t:primary_key 'id'
  t:string 'name'
  t:string 'steam_id'
  t:integer 'money'
  t:text { 'personal_description', null = true } -- `null = true` will add `DEFAULT NULL`
end)
```

Alternatively, you can do it the OO-way:
```lua
local query = Database:create('my_table')
  query:primary_key 'id'
  query:string 'name'
  query:string 'steam_id'
  query:integer 'money'
  query:text { 'personal_description', null = true } -- `null = true` will add `DEFAULT NULL`
query:execute()
```

Let's insert something into the database:
```lua
local query = Database:insert('my_table')
  query:insert('name', player:Name())
  query:insert('steam_id', player:SteamID())
  query:insert('money', 0)
  query:insert('personal_description', player:Name())
query:execute()
```

Now let's fetch the data:
```lua
local query = Database:select('my_table')
  query:where('steam_id', player:SteamID())
  query:callback(function(result)
    print('The first entry with matching steam id is '..result[1].name)
    -- do something with the result
  end)
query:execute()
```

To be continued...
==================
