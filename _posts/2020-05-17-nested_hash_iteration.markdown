---
layout: post
title:      "Nested Hash Iteration"
date:       2020-05-17 13:48:36 +0000
permalink:  nested_hash_iteration
---

```
contacts = {

    "Batman" => {
        name: "John Wayne",
        email: "batman@dcuniverse",
        fav_ice_cream_flavor: ["strawberry", "mint"]
     },

  "Ironman" => {
        name: "Tony Stark",
        email: "ironman@marveluniverse",
        fav_ice_cream_flavor: ["caramel","vanilla"]
     }
}  

puts contacts  

# First level. iterating through your key(super_hero) and value(data_hash)

contacts.each do |super_hero, data_hash| 
  "#{super_hero} #{data_hash}" 
end 



# Second level is selecting superhero("Batman") iterating through  your value(data_hash)

contacts.each do |super_hero, data_hash| 
  if super_hero == "Batman" 
    data_hash.each do |attribute, value|  
      puts "#{attribute} #{value}"
    end 
  end 
end 



# Third level. selecting your attribute(:fav_ice_cream_flavor) and iterating through your value(an array of ice cream flavors)


contacts.each do |super_hero, data_hash| 
  if super_hero == "Batman" 
    data_hash.each do |attribute, value|  
      if attribute == :fav_ice_cream_flavor 
        value.each do |flavor| 
          puts "#{flavor}"
        end
      end
    end 
  end 
end
    
#COPY AND PASTE IN YOUR SOURCE CODE EDITOR. 

```
