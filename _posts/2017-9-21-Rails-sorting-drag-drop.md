---
layout: post
title: Sorting Drag and Drop
description: How to execute Sorting with jQuery-ui and rails
tags: rails solution tutorial
---

Source [GoRails](https://gorails.com/episodes/sortable-drag-and-drop) tutorial on Sorting with Drag and Drop.
 
#### Setup 
```
# Gemfile
gem 'acts_as_list'


# application.js
//= require jquery-ui/widget 
//= require jquery-ui/sortable  
```

#### Migration
`rails g migration AddPositionToQuestions position:integer`

#### Update routes
```ruby
Rails.application.routes.draw do 
  resources :questions do
    collection do
      patch :sort 
    end
  end 

  #Rest of code
end
```

#### View of Sortable items
```slim
/app/views/questions/index.html.erb
#questions
  div dom_id=question data-url=sort_questions_path
  / ...
```

#### JS 
```coffeescript
$('#questions').sortable update: (e, ui) ->
  Rails.ajax
    url: $(this).data('url')
    type: 'PATCH'
    data: $(this).sortable('serialize')
```

### Controller
```ruby
def  index 
  @questions = Question.order(:position)
end 

def sort 
  params[:question].each_with_index do |id, index|
    Question.where(id: id).update_all(position: index + 1)
  end 
  head :ok
end 

```
