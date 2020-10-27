---
layout: post
title:      "Brewing Up Hot Cups of JavaScript"
date:       2020-08-31 10:08:17 -0400
permalink:  brewing_up_hot_cups_of_javascript
---


Coding puns aside. . .

For my latest poroject, introduced my established and clean cut friend Rails, to my newer, slightly edgier friend JavaScript and made them work together to create a trivia quiz.

Rails would handle the back end, creating the API (Application Programming Interface) where all the questions and answers would be stored. As well as containing the information as to which answers go to what question, and which answers are correct or not.

Javascript woukld then query my database and get the important information, group the questions and their associated answers, and then stylishly display them to the page with the help of everyone's stylish friend, CSS.

But how *exactly* do we do this?

I'm so glad you asked.

First the API itself needs to be created, Rails has a generator method for that:

```
rails g trivia_back_end --api
```

The '--api' at the end will build a Rails app but will withhold certain parts like the views or anything on the front end.

It's at this point that we will enlist the help of one of Rails little gems, known as: gem 'fast_jsonapi'
After adding this to the Gemfile and then running 'bundle install', we can now generate something called a 'serializer'. Serializers helo us to format our JSON (JavaScirpt Object Notation) making things on the front end MUCH easier.

Once we generate our serializers, they will look like this:

```class QuestionSerializer
  include FastJsonapi::ObjectSerializer
  attributes  :title
  has_many :answers
end```

```class AnswerSerializer
  include FastJsonapi::ObjectSerializer
  attributes :response, :question_id, :correct_answer
  belongs_to :question
end```

and the Questions controller's index method looks like:

```def index
                questions = Question.all
                options = {
                    include: [:answers, :correct_answer]
                }
                render json: QuestionSerializer.new(questions, options)
   end```
	 
This will render the questions, their associated answers (taken from the answer's question_id attribute), and will also show which of the four answer options has the 'correct_answer" arrtibute of 'true'. Needless to say it's very helpful.

This will make Fetching the questions very easy to handle.

Using 'fetch()' provides an easy way for Javascript to fetch resources asynchronously from what ever network you tell it to fetch it from, in my case it's my own database. The fetching process essentially works like this:\

1. The URL for my API is plugged in to the argument: ```'fetch('http://localhost:3000/api/v1/questions')```
2. The response it gets will then be converted to JSON: ```then(resp => resp.json())```
3. From there the JSON data is then pluggeed into my createQuestions function: ```.then(json => createQuestions(json))```

Here is where we actually turn the JSON data into Question objects to better access them in the app.

1. To start we will use a forEach() method to iterate over each question. This is better than hard coding a set amount because if in the future more questions were created every question in the database would get fetched.
```json.data.forEach((question)```
2. We need to assign a veriable for these Question objects, so let's use 'questionObj' (Any Giants/Browns fans out there?) ```let questionObj = new Question(question)``` Note that 'question' is used here again because it was established in step 1.
3. ```let answers = json.included.filter((answer) => {
             return answer.relationships.question.data.id === question.id
         })``` Lots of things happening here, but what this is doing is fetching the relationships between the answers and the associated question.
4. We then keep all our shiny new questionObjs in an array, for easy access later. ```allQuestions.push(questionObj)```

This is a lot of steps, with a lot of code, but after this it will be really easy to call questions and easily acces their answers similar to how it would work in a vanilla ruby application.

Using 'fetch()' is a great and easy way to access data from different sites. It follows logical steps from where to look, what information to get, and then converting it to JSON for easy use and manipulation later on. It's a great tool that JavaScript developers should get familiar with.

