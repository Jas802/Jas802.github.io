---
layout: post
title:      "Searching in Rails"
date:       2020-07-10 23:54:45 +0000
permalink:  searching_in_rails
---


Turns out this can be alot easier than soul searching.

In application we use, the ability to search for a specific item or quality is one of the biggest things a developer can to to improve funtionality. Juat take a second and imagine what YouTube would be like if there was no search funtion. Good luck finding that specific cat video.

I recently built an application that uses trainers as one of my models. I was asked to build a search funtion so the user can visit the trainer index page and then search for a specific trainer by name. Here is how it all went down

My trainers/index.html.erb file shows all the trainers in the databse in a list. Now once a certain number of trainers were created building a search bar and function makes a lot more sense than just scrolling for what could be eternity.

```
<h3> Find Your Trainer! </h3>
    <%= form_tag(trainers_path, method: :get) do %>
      <%= text_field_tag(:search, params[:search]) %>
      <%= submit_tag ("Search")%>
    <% end %>
    <br>

<% @trainers.each do |trainer| %>
<ul>
    <li><%=link_to trainer.name, trainer_path(trainer) %></li><br>
</ul>    
    <% end %><br>
```

The 'form_tag' code will render a search bar on the page. I set the method to ':get' so when the search is submitted, the form will load the 'trainers_path' URL and submit a 'get' request. This will help to filter things out as opposed to just displaying everything.

For anyone reading this: you might notice that I also added a 'params[:search}' underneath where I set my path and method. That won't do anything (actually it'll just break the application) untill ':search' is added to the trainer params, even workout trainers know that strong params are a MUST! Did you get the workout joke?

Before I went off the rails back there (gotcha!) I mentioned that I needed to ass ':search' to the trainer params.

```
private
    def trainer_params
        params.require(:trainer).permit(
            :name,
            :bio,
            :search
        )
    end
end
```
The ':search' param also needs to be added to the index method of the trainers controller. If the index page is loaded without a search input, params[:search] comes up 'nil'.

Next we create our class method to the trainer class itself:

```
def self.search(search)
       if search 
        where(['name LIKE ?', "%#{search}"])
        else
            Trainer.all
        end
    end
```

The third line of the above method uses the user input from what is typed into the search bar, and returns the trainer obejct with a name similar to the one used for the search request.

All of this is wrapped in an if/else statement. Meaning if a search happens, the method will then look for the corresponding trainer. If it cannot find a trainer similar to the name used to search, it will load all the trainers.

Being able to add searching functionality to an application helps to guide the user experience. It allows for quick acces to information which otherise would lead to endless navigation trying to find what the user is looking for. With just a little bit of help from params. Our application manages to stay on the rails.

Man, I am killing it with these coding jokes!
