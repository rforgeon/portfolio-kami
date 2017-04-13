---
layout: page
title: Lick Link
thumbnail-path: images/iphone-silver-lickLink-861px.png
short-description: Influencer sponsorship platform.
short-description-line2: "⚠️ Currently Under Development"
short-description-line3: "👀 View Prototype"
---


<div style="text-align:center;">
  <iframe width="438" height="930" src="//invis.io/WTARTIU9S" frameborder="0" allowfullscreen></iframe>
</div>

<br>
<br>

The Lick Link platform allows influencers to support brands with individualized links and allows brands to sponsor influencers with a percentage of sales.


<br>
<br>




## Problems ➡️ Solutions

<div style="text-align:center; -webkit-mask-image:-webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,1)), to(rgba(0,0,0,0))); "><img src ="http://i.giphy.com/l0MYM98IwMYDIn1fO.gif" /></div>

## Problem (A): Using UUID's

I use ID's when communicating with Google Analytics so I wanted to enhance my security slightly. I say slightly, because they main benefit is reducing the possibility of someone simply guessing with brute force. That being said, I implement further protection with using ID's.

**Traditional ID**

```ruby
ID  Value
--  -----
1   #Apple
2   #Orange
3   #Pear
4   #Mango
.. to GUID keys.
```
**UUID**

```ruby
ID                                    Value
------------------------------------  -----
'C87FC84A-EE47-47EE-842C-29E969AC5131'  #Apple
'2A734AE4-E0EF-4D77-9F84-51A8365AC5A0'  #Orange
'70E2E8DE-500E-4630-B3CB-166131D35C21'  #Pear
'15ED815C-921C-4011-8667-7158982951EA'  #Mango
```


## Solution (A): Using UUID's

The first issue I ran into when starting my UUID implementation was the fact that I already had a database setup with traditional incremental ID's.

When using a PostgreSQL server, the database needs to be primed for UUID's

```
$ rails g migration enable_uuid_extension
```

```
class EnableUuidExtension < ActiveRecord::Migration
  def change
    enable_extension 'uuid-ossp'
  end
end
```

Once this is done, you can then create your model.

```
$ rails g model post
```

Note the migration now includes **:uuid** as the primary key.

```ruby
class CreatePosts < ActiveRecord::Migration
  def change
    create_table :posts, id: :uuid, default: "uuid_generate_v4()", force: true do |t|
      t.string :title
      t.string :body
      t.timestamps
    end
  end
end
```

## Results

At the cost of a small increase in database lookup work, this UUID primary key helped make my platform more secure.

<br>

## More Coming Soon!

See how I worked with React + Redux in my [ride sharing discovery app 👉](http://www.forgeon.info/portfolio/1-myTopStop/)
