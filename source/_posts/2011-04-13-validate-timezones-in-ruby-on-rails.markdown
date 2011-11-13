---
layout: post
title: "Validate timezones in ruby on rails"
date: 2011-04-13 18:41
comments: true
categories: Ruby on Rails
author: Sonny Mai
---

Rails makes it too simple to allow users to specify their timezone. All you have to do is add the following to your form:

``` ruby _form.html.erb
# ..
<%= f.time_zone_select :time_zone, ActiveSupport::TimeZone.us_zones %>
# ..
```

``` ruby user.rb
# ..
field :time_zone, :type => String
# ..
```

Now you can see a very nice select element with all the timezones the world has to offer. In the above example, the US
timezones will show before the rest of the world. But what do you do to validate the timezones? You just have to drop
the below in to your model.

``` ruby user.rb
# ..
validates_inclusion_of :time_zone, :in => ActiveSupport::TimeZone.zones_map { |m| m.name }, :message => "is not a valid Time Zone"
# ..
```

Simple!!