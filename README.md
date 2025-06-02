# Postman + API Testing Demo

This is a simple API Testing demo project using Postman and the JSONPlaceholder fake API. It demonstrates how to use basic GET and POST requests with response validation using Postman’s built-in scripting.

## 🔧 Setup Instructions

1. Download and install [Postman](https://www.postman.com/downloads/)
2. Create a new collection named `Postman Test Demo`
3. Create a new environment:
   - Name: `API Env`
   - Variable: `base_url` = `https://jsonplaceholder.typicode.com`
4. Create and test the following requests.

## 📡 API Endpoints Used

### 1. Get All Posts

- **Method**: `GET`
- **URL**: `{{base_url}}/posts`

#### Test Script

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response is an array", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.be.an('array');
});
```

### 2. Create a Post

- **Method**: `POST`
- **URL**: `{{base_url}}/posts`
- **Body (JSON)**:

```json
{
  "title": "Postman Demo",
  "body": "This is a test post using Postman.",
  "userId": 1
}
```

#### Test Script

```javascript
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Post is created", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("id");
    pm.expect(jsonData.title).to.eql("Postman Demo");
});
```

### 3. Update a Post

- **Method**: `PUT`
- **URL**: `{{base_url}}/posts/1`
- **Body (JSON)**:

```json
{
  "title": "Postman Demo",
  "body": "This is a test post using Postman.",
  "userId": 1
}
```

#### Test Script

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Post was fully updated", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.title).to.eql("This Is an Updated Post Title");
    pm.expect(jsonData.body).to.eql("This replaces the entire body of an existing post.");
});
```

### 4. Patch the Title of the Post only

- **Method**: `PATCH`
- **URL**: `{{base_url}}/posts/1`
- **Body (JSON)**:

```json
{
  "title": "Patched Title Only"
}
```

#### Test Script

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Title was patched", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.title).to.eql("Patched Title Only");
});
```

### 5. Patch the Title of the Post only

- **Method**: `DELETE`
- **URL**: `{{base_url}}/posts/1`
- **Body (JSON)**:

```json
{
  "title": "Patched Title Only"
}
```

#### Test Script

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

## ✅ Features Covered

- Using Postman collections
- Setting environments and variables
- Sending requests (GET, POST, PUT, PATCH, DEL)
- Writing validation tests

## 📌 Notes

- Postman Test Demo is a fake API for prototyping.
- POST, PUT, PATCH, DEL requests simulate creation but do not store data.

## 🧑‍💻 Author

Created by [Ruddy Galo]
