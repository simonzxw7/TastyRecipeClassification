# TastyRecipeClassification
Implemented new annotations for Tasty to classify and categorize the genres of recipe. 

## Team:
Echo Zhang (piggyeq). 
Qomaruliati Setiawati (@ruli123).  
Kishan Maladkar Vishwanath (@kmv8694).  

## Data Scource

We collected recipes from [Tasty website](https://tasty.co/). The elements we scraped include recipe title, description, ingredients, and preparation steps. We collected around 2000 recipes. However, due to limited budget, we were only able to annotate 800 of them. Our annotations are divided into five categories: Appetizer/side-dish, Main course, Dessert, Drinks, and others. To explore more, please feel free to play around with our page by searching ingredients or food related key words and filter your search result using the drop down menu. Curious how we used our annotated data for predicting food category? please check out our Machine Learning page. 


## Project Introduction


We collected recipes from [Tasty website](https://tasty.co/). The elements we scraped include recipe title, description, ingredients, and preparation steps. We collected around 2000 recipes. However, due to limited budget, we were only able to annotate 800 of them. Our annotations are divided into five categories: Appetizer/side-dish, Main course, Dessert, Drinks, and Other.

We used Amazon Mechanical Turk annotate the recipes  based on tge categeries and for each recipe, we assign it to three different workers. Then, we extracted the best annotation if two annotators agree on one category. We investigated the inter-annotator agreement and we chose to use Krippendorff’s phi and alpha here because we have five categories(Appetizers/Side dish, Main course, Dessert, Drinks and Other). Based on Krippendorff’s alpha result, the observed disagreement is high (57.375%). The alpha is around 0.42, below the lowest conceivable limit (0.667), and falls into the range of (0.41, 0.6) as being moderate.

## Tasty Scraper

Here is a an example on how to run the scraper to extract content from one document (url)

```python
from src.TastyScraper import TASTYScraper

scraper = TASTYScraper()
output = scraper.getJSON("https://tasty.co/recipe/burrito-cups")

>>> {'title': 'Burrito Cups', 'ingredients': ['2 tablespoons olive oil', '1 onion, finely diced', '1 Â½ cups chicken, finely diced', 'salt, to taste', 'pepper, to taste', '2 cloves garlic, minced', '1 teaspoon chili powder', 'Â½ teaspoon paprika', '1 teaspoon cumin', 'Â½ teaspoon garlic powder', 'Â½ teaspoon cayenne pepper', '1 tomato, diced', '6 flour tortillas', 'Â¼ cup refried beans', 'Â¼ cup cooked rice', 'Â½ cup grated cheddar cheese', 'sour cream', 'guacamole', 'salsa', 'Â¼ cup fresh cilantro, chopped'], 'preparation': ['Heat a large skillet over medium heat. Add the oil and the onion and sautÃ© until translucent, 3-5 minutes. Add the chicken, season with salt and pepper, and cook until golden brown, about 5 minutes. Add the garlic and continue to cook for 2 minutes. Remove from heat and transfer the mixture to a medium bowl.', 'Mix together all the burrito spice mix ingredients, and then add the spice mix to the chicken mixture. Add the diced tomatoes and stir until completely combined.', 'Preheat the oven to 350Â°F (180Â°C). Grease a 12-cup muffin tin.', 'Place the 6 tortillas on top of each other. Cut them into a square shape, and then cut the square into quarters.', 'In the prepared muffin tin, place a tortilla square in each cup and push down. Push another layer of tortilla on top of each in a star formation. Spread some refried beans on the bottom of each tortilla cup, then add the cooked rice, and then the chicken mixture. Top each cup with cheddar cheese. Bake for 15 minutes, until the tortillas are brown and crispy and the cheese is melted.', 'Serve with sour cream, guacamole, salsa, and cilantro on the side.', 'Enjoy!'], 'description': "Here's what you need: olive oil, onion, chicken, salt, pepper, garlic, chili powder, paprika, cumin, garlic powder, cayenne pepper, tomato, flour tortillas, refried beans, cooked rice, grated cheddar cheese, sour cream, guacamole, salsa, fresh cilantro", 'reciepe_yield': '12 cups', 'ratings': {'ratingValue': '98', 'ratingCount': '356', 'bestRating': '100', 'worstRating': '0'}, 'cookingMethod': 'Bake', 'recipeCategory': 'Snacks', 'tool': 'Oven Mitts'}

# Output of the above json is as follows

for key, value in output:
    print(f"{key}: {value}")

>>> title: Burrito Cups
>>> ingredients: ['2 tablespoons olive oil', '1 onion, finely diced', '1 Â½ cups chicken, finely diced', 'salt, to taste', 'pepper, to taste', '2 cloves garlic, minced', '1 teaspoon chili powder', 'Â½ teaspoon paprika', '1 teaspoon cumin', 'Â½ teaspoon garlic powder', 'Â½ teaspoon cayenne pepper', '1 tomato, diced', '6 flour tortillas', 'Â¼ cup refried beans', 'Â¼ cup cooked rice', 'Â½ cup grated cheddar cheese', 'sour cream', 'guacamole', 'salsa', 'Â¼ cup fresh cilantro, chopped']
>>> preparation: ['Heat a large skillet over medium heat. Add the oil and the onion and sautÃ© until translucent, 3-5 minutes. Add the chicken, season with salt and pepper, and cook until golden brown, about 5 minutes. Add the garlic and continue to cook for 2 minutes. Remove from heat and transfer the mixture to a medium bowl.', 'Mix together all the burrito spice mix ingredients, and then add the spice mix to the chicken mixture. Add the diced tomatoes and stir until completely combined.', 'Preheat the oven to 350Â°F (180Â°C). Grease a 12-cup muffin tin.', 'Place the 6 tortillas on top of each other. Cut them into a square shape, and then cut the square into quarters.', 'In the prepared muffin tin, place a tortilla square in each cup and push down. Push another layer of tortilla on top of each in a star formation. Spread some refried beans on the bottom of each tortilla cup, then add the cooked rice, and then the chicken mixture. Top each cup with cheddar cheese. Bake for 15 minutes, until the tortillas are brown and crispy and the cheese is melted.', 'Serve with sour cream, guacamole, salsa, and cilantro on the side.', 'Enjoy!']
>>> description: Here's what you need: olive oil, onion, chicken, salt, pepper, garlic, chili powder, paprika, cumin, garlic powder, cayenne pepper, tomato, flour tortillas, refried beans, cooked rice, grated cheddar cheese, sour cream, guacamole, salsa, fresh cilantro
>>> reciepe_yield: 12 cups
>>> ratings: {'ratingValue': '98', 'ratingCount': '356', 'bestRating': '100', 'worstRating': '0'}
>>> cookingMethod: Bake
>>> recipeCategory: Snacks
>>> tool: Oven Mitts
```

## Algorithm Explained

The basic algorithm we will be implementing here will be this:

* Write a function `compile_URL` which compiles all URLs of recipes from the website into one `todo_url` list.
* Pop one URL off the `todo_url` list.
* Pass the URL into the `TASTYScraper` class using the class method `get_json`.
* Get the info from the URL and store all information into a dictionary.
* Append the dictionary to the final `output_lst`
* Wait for 1 second using time.sleep(1)
* Repeat step 2


### Corpus Explanation


The source of the corpus is https://tasty.co/ which we used to scrape recipes for our project. The collected corpus is stored in the milestone2 folder in the repo.For the scraped data, we choose to store everything in one json file with each recipe data identified by an index. 

	* The total number of documents(recipes) is 2000
	* The total number of word types is 12124
	* The total number of  word tokens is 797916 


Since we are using the ‘related recipe’ on each recipe to ultimately crawl all recipe links, here we may end up in a cycle and not be able to scrape all the links of recipes on the site. However, from our experiment, we can scrape 2000+ recipes each time which should be sufficient for our purpose. We made sure that there are no duplicates of recipes and there is not much noise inside the data, the output JSON file is clean and doesn't need much tweaking.  

For the recipe contents, we noticed that a great number of lists of “ingredients” contains some fraction numbers and integer numbers together to indicate the quantity of dose. For example, “1 ¼ cups organic sugar”. Since this number plays a key role when we start predicting for the category of this food in terms of sides, dessert, or main course. We might need to implement a function that turns those expressions into a number that the computer can understand. 
Recipe contains a number of repeated words, which is expected in this setting. Some cooking actions and food ingredients are highly repeated even in completely different recipes. For example, ingredients “water” can be used for a drink and also can be used for a soup, though drink and soup should be categorized differently. 

### Annotation Plan

The annotation that we will be doing involves looking at the recipe types. We are classifying the categories as appetizers/side-dish, main course, dessert, drinks, and others.  For each annotation, each recipe includes the recipe title, description, ingredients, and preparation. Further details on the annotation labels can be seen in the initial draft of our annotation guidelines. 

The tools we will be using to create our annotations are Amazon Mechanical Turk. Our annotators will be workers from Amazon Mechanical Turk. We have done a pilot study of our annotation tasks on Mechanical Turk using 10 recipes. We made sure that the 10 recipes cover all of our classification categories so that we could see the quality of the annotations and evaluate ways to improve the annotations. In addition to that, we did the pilot study with 3 respondents per assignment so we were able to see how the annotation results vary among different respondents.

The result of our pilot study shows that the annotations were correct for most of the recipes. However, there were one or two recipes such as Slow-Cooker Roasted Tomato Basil Soup and Spaghetti Meatball Bake, where we got completely different results among the three different respondents. This was a good lesson for us to evaluate for our complete annotations next week. One thing that we could do to improve is to set the additional filter on the workers such as limiting to workers with an approval rate of 95% and above. In addition to that, we will add additional information on the annotation guideline particularly for the appetizers/side-dish and main course category to improve the quality of our annotation. 

For our annotations next week, we are planning to do have 3 respondents per assignment. Given the $50 that we have, we have done the  

	* Cost per assignment = 3 respondents x 0.02 = 0.06
	* Total possible annotated data = $50 / 0.06 = 833

Therefore, we propose to annotate 800 to 830 recipes with Amazon Mechanical Turk.

### Annotation Guidelines Draft

#### Description

The annotation task is to identify the correct type that matches the recipe.  Each task contains one document which is one recipe. Each recipe contains the title, description, ingredients, and preparation steps. We classified the types into five groups: appetizer or side dish, main course, dessert, drinks, and others. A detailed explanation of the types is shown below.

#### Labels Explanation

* Appetizer or side dish. This type usually involves simple preparation steps and has few ingredients. The description of the recipe often indicates that this food is good for sharing. This type usually involves simple preparation steps and has few ingredients. Examples of appetizer or side dish recipes from TASTY website include Garlic Parmesan-Stuffed Mushrooms, Classic Heirloom Tomato Bruschetta, and Buffalo Chicken Mozzarella Sticks.

* Main course. Most of the time, the ingredients contain rice, noodle, potatoes, or pasta. In addition to that, the preparation involves more complex steps. The description usually mention breakfast, lunch or dinner. As an example, the description may say "Are you tired of having the same dinner? Try this easy Creamy Lemon Chicken recipe!" Examples of main courses include Creamy Lemon Chicken, Chicken Paprika Chicken & Rice Bake, and Veggie Cauliflower Fried Rice.

* Dessert. The ingredients usually contain sugar, flour, or fruits. Examples of desserts include cakes, pudding, and chocolate mousse.

* Drinks. Examples of drinks include juice, coffee, smoothies, and other drinks. 

* Others. When the recipe can be classified into two or more categories, please use your best judgment. 

### Example from Pilot Study on MTurk

![pilot_study](pilot_study.png)

The link to the code that produced the 10 data samples for the pilot study is [here](https://github.ubc.ca/piggyeq/COLX_523_Project/blob/master/milestone2/pilotDataGen.py)


## Steps to getting our final annotation

The steps that we took from getting our raw corpus to our final annotation are the following:

* Using `dataCleaner.py`,  we extracted the necessary information for the annotations such as the title, description, ingredients, and preparation steps. In addition to that, we also cleared out all the emojis because otherwise, the CSV file will not work with Mechanical Turk.
* We downloaded the annotation results from Amazon Mechanical Turk. The raw annotation result is stored in `mturk_results.csv`
* In the `annotionsExtractor.py`, we extracted the annotation result from `Answer.category.label` column and we cleaned the data so that we could get a single “best” annotation for each recipe.
* The final annotation result is stored in `mturk_cleaned.csv`

## Discussion

Overall, the annotation process on Amazon Mechanical Turk smoothly. We investigated the inter-annotator agreement and we chose to use Krippendorff’s phi and alpha here because we have five categories(Appetizers/Side dish, Main course, Dessert, Drinks and Other). Krippendorff's alpha specifically compares 'observed' disagreement with the 'expected' disagreement. Based on Krippendorff’s alpha result, the observed disagreement is high (57.375%). The alpha is around 0.42, below the lowest conceivable limit (0.667), and falls into the range of (0.41, 0.6) as being moderate. For further information about our inter-annotator agreement study, please refer to `InterAnnotator.ipynb`.







