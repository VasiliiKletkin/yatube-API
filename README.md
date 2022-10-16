# yatube-API
### Description
API for Yatub is a social network project that implements the following features,
publish entries, comment on entries, as well as subscribe or unsubscribe from authors.

---

### Technologies:
* Python
* Django
* Pytest
* Git
* DRF
* JWT

---

### Installation
Clone the repository on the local machine:

```$ git clone https://github.com/vkletkin/yatube-main```

 Create a virtual environment:
 
 ```$ python -m venv venv```
 
 Install dependencies:

```$ pip install -r requirements.txt```

Creating and applying migrations:

```$ python manage.py makemigrations``` and  ```$ python manage.py migrate```

Starting the django server:

```$ python manage.py runserver```

---

### API examples for all users
For unauthorized users, working with the API is available in read mode,
nothing can be changed or created.
```bash
GET api/v1/posts/ - get a list of all posts.
When specifying the limit and offset parameters, the output should work with pagination
GET api/v1/posts/{id}/ - getting a post by id

GET api/v1/groups/ - getting a list of available communities
GET api/v1/groups/{id}/ - getting information about the community by id

GET api/v1/{post_id}/comments/ - get all comments on a post
GET api/v1/{post_id}/comments/{id}/ - Getting a comment on a post by id
```
### API examples for authorized users
To create a post, use:
```bash
POST /api/v1/posts/
```
in body
```
{
"text": "string",
"image": "string",
group: 0
}
```
Post update:
```bash
PUT /api/v1/posts/{id}/
```
in body
```
{
"text": "string",
"image": "string",
group: 0
}
```

Partial post update:
```bash
PATCH /api/v1/posts/{id}/
```
in body
```
{
"text": "string",
"image": "string",
group: 0
}
```

Partial post update:
```bash
DEL /api/v1/posts/{id}/
```
Getting access to the /api/v1/follow/ endpoint
(subscription) is only available to authorized users.
```bash
GET /api/v1/follow/ - user subscription on whose behalf the request was made
to the user passed in the body of the request. Anonymous requests are prohibited.
```
- Authorized users can create posts,
comment on them and follow other users.
- Users can change (delete) the content of which they are the author.

### You need to add a group to the project through the Django admin panel:
```bash
admin/ - after authorization, go to the Groups section and create groups
```
Access by an authorized user is available with a JWT token (Joser),
which can be obtained by performing a POST request to the address:
```bash
POST /api/v1/jwt/create/
```
Passing user data in body (for example, in postman):
```bash
{
"username": "string",
"password": "string"
}
```
We add the received token to headers (postman), after which all project functions will be available:
```bash
Authorization: Bearer {your_token}
```
Update JWT token:
```bash
POST /api/v1/jwt/refresh/ - refresh JWT token
```
Check JWT token:
```bash
POST /api/v1/jwt/verify/ - JWT token verification
```
Also, pagination (LimitOffsetPagination) is implemented in the API project:
```bash
GET /api/v1/posts/?limit=5&offset=0 - pagination for 5 posts, starting from the first
```
