# Python Essentials with FastAPI CRUD - Explained with Examples

## 1. **Decorators**

**Definition:**  
A decorator is a function that takes another function and extends its behavior without explicitly modifying it.

**Example:**
```python
def my_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@my_decorator
def greet():
    print("Hello!")

greet() 
```
### sample output
```
Output:

Before function call
Hello!
After function call
```
## 2. Generators

### Definition:
* Generators are functions that return an iterable sequence of items, one at a time, using the yield keyword.

#### Sample Example:
```python
def count_up_to(max):
    count = 1
    while count <= max:
        yield count
         count += 1

for number in count_up_to(3):
    print(number)
``` 
#### Sample Output:
```
1
2
3
```
## 3. Lambda Functions
### Definition:
* A lambda function is a small anonymous function defined using the lambda keyword.
``` python
Syntax: lambda arguments: expression
```
#### sample Example:
``` python
square = lambda x: x * x
print(square(5))  # Output: 25
```
### Use in sorting:
``` python
pairs = [(1, 'one'), (3, 'three'), (2, 'two')]
pairs.sort(key=lambda pair: pair[0])
print(pairs)
```
## 4. Dictionary (dict)
### Definition:
* A dictionary is a collection of key-value pairs.

#### sample Example:
``` python
person = {"name": "Alice", "age": 25}
# Create
person["city"] = "New York"

# Read
print(person["name"])

# Update
person["age"] = 30

# Delete
del person["city"]
```
## 5. List
### Definition:
* A list is an ordered collection of items, which can be modified (mutable).

#### sample Example:
```python
numbers = [10, 20, 30]

# Create/Add
numbers.append(40)

# Read
print(numbers[1])  # Output: 20

# Update
numbers[0] = 15

# Delete
del numbers[2]
```
## 6. CRUD Operations with FastAPI
### Definition:
* CRUD stands for Create, Read, Update, and Delete. FastAPI allows you to build RESTful APIs quickly and efficiently.

### sample Example: Basic CRUD App

```python

from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

items = {}

# Create
@app.post("/items/{item_id}")
def create_item(item_id: int, item: Item):
    items[item_id] = item
    return items[item_id]

# Read
@app.get("/items/{item_id}")
def read_item(item_id: int):
    return items.get(item_id, "Item not found")

# Update
@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item):
    items[item_id] = item
    return items[item_id]

# Delete
@app.delete("/items/{item_id}")
def delete_item(item_id: int):
    return items.pop(item_id, "Item not found")

```
### ✅ Installation Requirements

#### 1. Python Version
Requires: Python 3.10+

Check with:

```bash
python --version
```
#### 2. Install Required Packages
```bash
pip install fastapi uvicorn[standard] pydantic
```
#### 3. Run the FastAPI App
Assuming your main script is main.py, use:

``` bash
uvicorn main:app --reload
```
--reload enables auto-reload during development.



### sample output

🔹 1. Create Item (POST)
``` postman
Request:

POST /items/1
``` 
```json
Body:

json
{
  "name": "Laptop",
  "price": 999.99
}
Response:

json
{
  "name": "Laptop",
  "price": 999.99
}
```
🔹 2. Read Item (GET)
```postman
Request:

GET /items/1
```
```json
Response:

json
{
  "name": "Laptop",
  "price": 999.99
}
```
🔹 3. Update Item (PUT)

``` postman Request:
PUT /items/1
```

```json Body:

json
{
  "name": "Gaming Laptop",
  "price": 1299.99
}
Response:

json
{
  "name": "Gaming Laptop",
  "price": 1299.99
}
```

🔹 4. Delete Item (DELETE)
```postman
Request:

DELETE /items/1
```
```json
Response:

json
{
  "name": "Gaming Laptop",
  "price": 1299.99
}
```

🔹 5. Read Deleted Item (GET)
```postman
Request:

GET /items/1
```
```json
Response:

json

"Item not found"
```
###  Python & FastAPI CRUD Interview Questions

- What is FastAPI and what are its advantages over Flask or Django?
- Explain the role of Pydantic in FastAPI. How does it help with data validation?
- How do you define a POST endpoint in FastAPI to create a new resource (e.g., a user)?
- What is the difference between @app.post() and @app.get() in FastAPI?
- How would you structure a FastAPI project that supports CRUD operations for a database table?
- What is a Pydantic model? How is it different from an ORM model?
- What is dependency injection in FastAPI and why is it useful?
- How do you handle request body and query parameters in FastAPI?
- What is the purpose of the Depends function in FastAPI? Give an example use case.
- How do you connect FastAPI to a relational database using SQLAlchemy?
- How would you implement update (PUT/PATCH) functionality in a FastAPI CRUD API?
- How does FastAPI handle asynchronous requests? What is the benefit of using async def?
- How do you return custom error responses in FastAPI (e.g., 404 or 400)?
- What are background tasks in FastAPI and when would you use them?
- Explain how to secure CRUD endpoints using OAuth2 with JWT in FastAPI.

