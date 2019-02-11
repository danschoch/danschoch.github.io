---
layout: post
title:      "Bringing Peace To The Whole Stack With Olive Branch"
date:       2019-02-11 20:32:18 +0000
permalink:  bringing_peace_to_the_whole_stack_with_olive_branch
---


This is another quick post on a wonderful tool I just discovered while working on a full stack application with a Rails API backend and React frontend. 

The problem -- variations in the conventions used by Ruby and Javascript in the syntax of variables. Rubyists tend to use snake_case syntax for their variables, while Javascript uses camelCase. When communicating between a backend and frontend, this can cause significant headaches for your application and its developers. Ultimately, it seems like the choice is that one or the other needs to go against convention and change their syntax, so as to match variables properly and allow data requests to proceed as they normally would. This is a headache, at best.

But put the ibuprofen down, because Olive Branch is here to save the day! Olive branch is a piece of middleware that can be added to your application to let API users work with camelCased keys, while your Rails backend continues with snake_cased ones.

Simply add `gem "olive_branch"` to your Gemfile and run bundler. Then, add `config.middleware.use OliveBranch::Middleware` to `config/applcation.rb`. Now, whenever a request is made to your API, inlclude the header `X-Key-Inflection` with a value of either `camel`, `snake`, or `dash` and that's it! No more variable problems. Here's an example of what a POST request to a Rails API might look like for submitting a recipe to an index using the fetch API:

```
const url = 'https://example.com/recipies';
const data = {
  name: 'Recipe 1',
  instructionList: {
    1: 'Step 1',
    2: 'Step 2',
    3: 'Step 3'
  },
  ingredientList: ['ingedient 1', 'ingredient 2', 'ingredient 3']
};


fetch(url,  {
        method: "POST",
        headers: { 
          "Content-Type": "application/json",
          "X-Key-Inflection": "camel"
        },
        body: JSON.stringify(data)
    }).then(response => {
      return response.json()
    }).then(responseJSON => {
      return console.log(resonseJSON)
		})
```

That little addition of the extra header, plus an easy initial installation, is all it took for me to not have to worry about variable syntax anymore. This saved me a bit of extra time, and I hope it does for you too!


