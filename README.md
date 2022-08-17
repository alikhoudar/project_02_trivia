# Trivia App - Udacitriva

This project is a Trivia App for Udacity employees and students. The project Homepage can display questions - both all questions and by category.

Each listed question shows the question, the category and the difficulty score. And ability for showing/hiding the answer.

Employees and Students also:

- Delete questions.

- Add questions and require that they include questions and anwer text.

- Search for questions based on a text query string.

- Play the quiz game, randomizing either all questions or within a specific category.

All backend code follows [PEP8 style guidelines](https://www.python.org/dev/peps/pep-0008/).

---

#### Project homepage

![](C:\Users\ALI\AppData\Roaming\marktext\images\2022-08-17-15-11-30-image.png)

# Getting Started

### Pre-requisites and Local Development

#### Backend

Developers using this project should already have Python3, pip, virtualenv and node installed on their local machines.

**1. Clone the project on your local environment**

```
git clone https://github.com/alikhoudar/project_02_trivia.git

cd "Your Local Folder where the project was downloaded"
```

**2. Initialize and activate a virtualenv using:**

on Mac or Linux:

```
cd "To your /backend folder"
python -m virtualenv env
source env/bin/activate
```

on Windows:

```
cd "To your /backend folder"
python -m virtualenv env
.\env\Scripts\activate.bat
```

**3. Install the dependencies:**

```
pip install -r requirements.txt
```

**4. Run the development server:**

on Mac or Linux:

```
FLASK_APP=flaskr
FLASK_ENV=development # enables debug mode
flask run
```

on Windows:

```
set FLASK_APP=flaskr
set FLASK_ENV=development # enables debug mode
flask run
```

**5. Verify on the Browser**  
Navigate to project homepage http://127.0.0.1:5000/ or http://localhost:5000

#### Frontend

From the frontend folder, run the following commands to start the client:

```
npm install // only once to install dependencies
npm start 
```

By default, the frontend will run on localhost:3000.

### Tests

In order to run tests navigate to the backend folder,  and run the following commands:

```
dropdb bookshelf_test
createdb bookshelf_test
psql bookshelf_test < books.psql
python test_flaskr.py
```

on Windows:

The first time you run the tests, omit the dropdb command.

All tests are kept in that file and should be maintained as updates are made to app functionality.

#### API Reference

### Getting Started

- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:5000/`, which is set as a proxy in the frontend configuration.
- Authentication: This version of the application does not require authentication or API keys.

### Error Handling

Errors are returned as JSON objects in the following format:

```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```

The API will return four error types when requests fail:

- 400: Bad Request
- 404: Resource Not Found
- 422: Not Processable
- 405: Method Not Allowed

### Endpoints

#### GET /categories

- General:
  
  - Returns a list of category objects, success value, and total number of categories

- Sample: `curl http://127.0.0.1:5000/categories`

```{
  {
  "categories": [
    {
      "id": 1,
      "type": "Science"
    },
    {
      "id": 2,
      "type": "Art"
    },
    {
      "id": 3,
      "type": "Geography"
    },
    {
      "id": 4,
      "type": "History"
    },
    {
      "id": 5,
      "type": "Entertainment"
    },
    {
      "id": 6,
      "type": "Sports"
    }
  ],
  "success": true,
  "total_categories": 6
}
```

#### GET /questions

- General:
  
  - Returns a list of question objects, list of category objects, current_category, success value, and total number of questions
  - Results are paginated in groups of 10. Include a request argument to choose page number, starting from 1.

- `curl http://127.0.0.1:5000/questions?page=1`
  
  ```
  {
    "categories": [
      {
        "id": 1,
        "type": "Science"
      },
      {
        "id": 2,
        "type": "Art"
      },
      {
        "id": 3,
        "type": "Geography"
      },
      {
        "id": 4,
        "type": "History"
      },
      {
        "id": 5,
        "type": "Entertainment"
      },
      {
        "id": 6,
        "type": "Sports"
      }
    ],
    "current_category": "Entertainment",
    "questions": [
      {
        "answer": "Apollo 13",
        "category": 5,
        "difficulty": 4,
        "id": 2,
        "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
      },
      {
        "answer": "Tom Cruise",
        "category": 5,
        "difficulty": 4,
        "id": 4,
        "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
      },
      {
        "answer": "Maya Angelou",
        "category": 4,
        "difficulty": 2,
        "id": 5,
        "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
      },
      {
        "answer": "Edward Scissorhands",
        "category": 5,
        "difficulty": 3,
        "id": 6,
        "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
      },
      {
        "answer": "Muhammad Ali",
        "category": 4,
        "difficulty": 1,
        "id": 9,
        "question": "What boxer's original name is Cassius Clay?"
      },
      {
        "answer": "Uruguay",
        "category": 6,
        "difficulty": 4,
        "id": 11,
        "question": "Which country won the first ever soccer World Cup in 1930?"
      },
      {
        "answer": "Lake Victoria",
        "category": 3,
        "difficulty": 2,
        "id": 13,
        "question": "What is the largest lake in Africa?"
      },
      {
        "answer": "The Palace of Versailles",
        "category": 3,
        "difficulty": 3,
        "id": 14,
        "question": "In which royal palace would you find the Hall of Mirrors?"
      },
      {
        "answer": "Agra",
        "category": 3,
        "difficulty": 2,
        "id": 15,
        "question": "The Taj Mahal is located in which Indian city?"
      },
      {
        "answer": "Escher",
        "category": 2,
        "difficulty": 1,
        "id": 16,
        "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
      }
    ],
    "success": true,
    "total_questions": 20
  }
  ```
  
  #### DELETE /questions/{question_id}

- General:
  
  - Deletes the question of the given ID if it exists. Returns the id of the deleted question, success value, total questions, and question list

- `curl -X DELETE http://127.0.0.1:5000/questions/27`
  
  ```
  {
    "deleted": 27,
    "questions": [
      {
        "answer": "Apollo 13",
        "category": 5,
        "difficulty": 4,
        "id": 2,
        "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
      },
      {
        "answer": "Tom Cruise",
        "category": 5,
        "difficulty": 4,
        "id": 4,
        "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
      },
      {
        "answer": "Maya Angelou",
        "category": 4,
        "difficulty": 2,
        "id": 5,
        "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
      },
      {
        "answer": "Edward Scissorhands",
        "category": 5,
        "difficulty": 3,
        "id": 6,
        "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
      },
      {
        "answer": "Muhammad Ali",
        "category": 4,
        "difficulty": 1,
        "id": 9,
        "question": "What boxer's original name is Cassius Clay?"
      },
      {
        "answer": "Uruguay",
        "category": 6,
        "difficulty": 4,
        "id": 11,
        "question": "Which country won the first ever soccer World Cup in 1930?"
      },
      {
        "answer": "Lake Victoria",
        "category": 3,
        "difficulty": 2,
        "id": 13,
        "question": "What is the largest lake in Africa?"
      },
      {
        "answer": "The Palace of Versailles",
        "category": 3,
        "difficulty": 3,
        "id": 14,
        "question": "In which royal palace would you find the Hall of Mirrors?"
      },
      {
        "answer": "Agra",
        "category": 3,
        "difficulty": 2,
        "id": 15,
        "question": "The Taj Mahal is located in which Indian city?"
      },
      {
        "answer": "Escher",
        "category": 2,
        "difficulty": 1,
        "id": 16,
        "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
      }
    ],
    "success": true,
    "total_questions": 19
  }
  ```
  
  #### POST /questions

- General:
  
  - Creates a new question using the submitted question, answer, category and difficulty. Returns the id of the created question, success value, total questions, and questions list based on current page number to update the frontend

- `curl http://127.0.0.1:5000/questions/ -X POST -H "Content-Type: application/json" -d '{"question":"simple question", "answer": "simple answer", "category": "1", "difficulty": "1"}'`
  
  ```
  {
    "created": 29,
    "questions": [
      {
        "answer": "Apollo 13",
        "category": 5,
        "difficulty": 4,
        "id": 2,
        "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
      },
      {
        "answer": "Tom Cruise",
        "category": 5,
        "difficulty": 4,
        "id": 4,
        "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
      },
      {
        "answer": "Maya Angelou",
        "category": 4,
        "difficulty": 2,
        "id": 5,
        "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
      },
      {
        "answer": "Edward Scissorhands",
        "category": 5,
        "difficulty": 3,
        "id": 6,
        "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
      },
      {
        "answer": "Muhammad Ali",
        "category": 4,
        "difficulty": 1,
        "id": 9,
        "question": "What boxer's original name is Cassius Clay?"
      },
      {
        "answer": "Uruguay",
        "category": 6,
        "difficulty": 4,
        "id": 11,
        "question": "Which country won the first ever soccer World Cup in 1930?"
      },
      {
        "answer": "Lake Victoria",
        "category": 3,
        "difficulty": 2,
        "id": 13,
        "question": "What is the largest lake in Africa?"
      },
      {
        "answer": "The Palace of Versailles",
        "category": 3,
        "difficulty": 3,
        "id": 14,
        "question": "In which royal palace would you find the Hall of Mirrors?"
      },
      {
        "answer": "Agra",
        "category": 3,
        "difficulty": 2,
        "id": 15,
        "question": "The Taj Mahal is located in which Indian city?"
      },
      {
        "answer": "Escher",
        "category": 2,
        "difficulty": 1,
        "id": 16,
        "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
      }
    ],
    "success": true,
    "total_questions": 20
  }
  ```

#### POST /questions/search

- General:
  
  - Search questions by given search term  and return a list of questions for whom the search term, success value, current category, total question that match the search term and update the content of the frontend

- `curl http://127.0.0.1:5000/questions/search -X POST -H "Content-Type: application/json" -d '{"search":"title"}'`
  
  ```
  {
    "current_category": "History",
    "questions": [
      {
        "answer": "Maya Angelou",
        "category": 4,
        "difficulty": 2,
        "id": 5,
        "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
      },
      {
        "answer": "Edward Scissorhands",
        "category": 5,
        "difficulty": 3,
        "id": 6,
        "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
      }
    ],
    "success": true,
    "total_questions": 2
  }
  ```

#### GET /categories/{category_id}/questions

- General:
  
  - Returns a list of question objects, current_category, success value, and total number of questions based on given category id
  - Results are paginated in groups of 10. Include a request argument to choose page number, starting from 1.

- `curl http://127.0.0.1:5000/categories/1/questions`
  
  ```
  {
    "current_category": "Science",
    "questions": [
      {
        "answer": "The Liver",
        "category": 1,
        "difficulty": 4,
        "id": 20,
        "question": "What is the heaviest organ in the human body?"
      },
      {
        "answer": "Alexander Fleming",
        "category": 1,
        "difficulty": 3,
        "id": 21,
        "question": "Who discovered penicillin?"
      },
      {
        "answer": "Blood",
        "category": 1,
        "difficulty": 4,
        "id": 22,
        "question": "Hematology is a branch of medicine involving the study of what?"
      },
      {
        "answer": "",
        "category": 1,
        "difficulty": 1,
        "id": 28,
        "question": ""
      },
      {
        "answer": "simple answer",
        "category": 1,
        "difficulty": 1,
        "id": 29,
        "question": "simple question"
      }
    ],
    "success": true,
    "total_questions": 5
  }
  ```

#### POST /quizzes

- General:
  
  - Returns a list of questions to play the quiz, previous question if exists, quiz category based on given category id and previous question list.

- `curl http://127.0.0.1:5000/quizzes -X POST -H "Content-Type: application/json" -d '{"previous_questions":[], "quiz_category": "{"id": "1", "type": "Science"}"}'`
  
  ```
  {
    "previous_questions": [
      20
    ],
    "question": {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    "success": true
  }
  ```

#### Deployment N/A
