# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 

REVIEW_COMMENT
```
This README is missing documentation of your endpoints. Below is an example for your endpoint to get all categories. Please use it as a reference for creating your documentation and resubmit your code. 

Endpoints
GET '/categories'
GET ...
POST ...
DELETE ...
 
GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, categories, that contains a object of id: category_string key:value pairs.
{'1' : "Science",
'2' : "Art",
'3' : "Geography",
'4' : "History",
'5' : "Entertainment",
'6' : "Sports"}


GET ‘/questions’
- Fetches a List of Questions Available
- Request Arguments: page , for fetching the data for particular page
- Returns: Returns Object with details about categories, current_category, questions list and total_no_of questions.

Sample response format
 {
     "categories": {
         "1": "Science",
         "2": "Art",
         "3": "Geography",
         "4": "History",
         "5": "Entertainment",
         "6": "Sports"
     },
     "current_category": null,
     "questions": [
         {
             "answer": "Spain",
             "category": null,
             "difficulty": 1,
             "id": 30,
             "question": "Who won 2010 Worldcup?"
         },
         {
             "answer": "Italy",
             "category": 6,
             "difficulty": 1,
             "id": 31,
             "question": "Who won 2006 Worldcup?"
         }
     ],
     "total_questions": 26
 }


GET ‘/categories/<int:id>/questions’
- Fetches a List of Questions for particular category received from id parameter in request
- Request Arguments: page (OPTIONAL) , for fetching the data for particular page
- Returns: Returns Object with details about current_category, questions list and total_no_of questions, status_code,success

-Sample Request Format:

 http://localhost:5000/categories/6/questions?page=1

-Sample Responseformat:
 {
     "current_category": null,
     "questions": [
         {
             "answer": "Brazil",
             "category": 6,
             "difficulty": 3,
             "id": 10,
             "question": "Which is the only team to play in every soccer World Cup tournament?"
         },
         {
             "answer": "Uruguay",
             "category": 6,
             "difficulty": 4,
             "id": 11,
             "question": "Which country won the first ever soccer World Cup in 1930?"
         }],
     "status_code": 200,
     "success": true,
     "total_questions": 10
 }

DELETE ‘/questions/<int:id>’
- Delete Question based on specific Question id
- Request Arguments: id (Required) -Question Id
- Returns: object with status_code and success

Sample Request :
  http://localhost:5000/questions/11

Sample Response :
  {
      "status_code": 200,
      "success": true
  }
 
POST '/questions'
- This endpoint is used for search as well as creating new question
 
Request body:
 
   For Creating New Question
 
   Request Body : {
           "question": "Who won 2006 Worldcup?",
           "answer": "Italy",
           "difficulty": 1,
           "category": "6"
   }
 
   For Seaching the Question
           Request Body :
                   {
                   "searchTerm":"1930"
                   }
  
Returns:
   Search Result Response:
       {
           "current_category": null,
           "questions": [
               {
                   "answer": "Agra",
                   "category": 3,
                   "difficulty": 2,
                   "id": 15,
                   "question": "The Taj Mahal is located in which Indian city?"
               }
           ],
           "total_questions": 1
       }
  
    Creating New Question:
       Response:
       {
           "status_code": 200,
           "success": true,
           "total_questions": 24
       }
  
POST: /quizzes
 
End point created for getting a question for quiz based on category  .
This method will give the question based on the category and it will also exclude the question already answered in current quiz.
 
Request Body:
	Previous_questions :List of Questions,
	Quiz_category : object that have category id
 
Sample RequestBody:
    {
        "previous_questions": [],
        "quiz_category":  {"type": "click", "id": 0}
    }
 
Sample ResponseBody:
	{
        "question": {
            "answer": "Jackson Pollock",
            "category": 2,
            "difficulty": 2,
            "id": 19,
            "question": "Which American artist was a pioneer of Abstract Expressionism, and a leading exponent of action painting?"
        },
        "status": 200,
        "success": true
    }


```


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```