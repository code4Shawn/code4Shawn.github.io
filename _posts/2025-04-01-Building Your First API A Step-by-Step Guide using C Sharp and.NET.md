---
title: Building Your First API: A Step-by-Step Guide using C#
categories: [Technology, API's, C#]
tags: [C#, API's]
author: Shawn Ng'iela
image: https://images.unsplash.com/photo-1550751827-4bd374c3f58b?w=600&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTF8fHRlY2hub2xvZ3l8ZW58MHx8MHx8fDA%3D
---

APIs (Application Programming Interfaces) are the backbone of modern software development, enabling applications to communicate with each other.

Creating a RESTful API is a fundamental skill for modern developers. Whether you're building a mobile app, a web application, or integrating systems, APIs are the backbone of communication between services. 

In this guide, we'll walk through building a simple RESTful API using C# and Visual Studio.

## What is a RESTful API?
REST (Representational State Transfer) is an architectural style for designing networked applications. A RESTful API uses HTTP requests to perform CRUD (Create, Read, Update, Delete) operations on resources, which are typically represented in JSON or XML format.

### Prerequisites
* Visual Studio 2022 (Community edition is free)

* .NET 6 or later (included with Visual Studio)

* Basic knowledge of C# and HTTP concepts

### Step 1: Create a New Project
1. Open Visual Studio and click Create a new project.

2. Select ASP.NET Core Web API and click Next.

3. Name your project (e.g., FirstApi) and choose a location.

4. Select .NET 6.0 (or later) as the framework.

5. Click Create.

Visual Studio will generate a basic API template with a <span style="background-color: #808080">***WeatherForecast controller*** </span>.

### Step 2: Understand the Project Structure

The generated project includes:

* <span style="background-color: #808080">**Controllers/** </span> – Contains API endpoints (controllers handle HTTP requests).

* <span style="background-color: #808080"> **Program.cs** </span> – Configures the application (middleware, services, etc.).

* <span style="background-color: #808080"> appsettings.json </span> – **Configuration file** (e.g., connection strings, logging).

### Step 3: Create a Model

A <span style="background-color: #808080"> **model** </span> represents the data structure. Let's create a simple <span style="background-color: #808080"> **Product** </span> model.

1. Right-click the project → **Add** → **New Folder** → Name it <span style="background-color: #808080"> Models </span>.

2. Right-click the <span style="background-color: #808080"> Models </span> folder → **Add** → **Class** → Name it <span style="background-color: #808080"> Product.cs </span>.

3. Define the model:

```csharp
namespace FirstApi.Models;

public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

### Step 4: Create a Controller

Controllers handle HTTP requests (GET, POST, PUT, DELETE).

1. Right-click the <span style="background-color: #808080"> Controllers </span> folder → **Add** → **Controller**.

2. Select **API Controller** - **Empty** → Name it <span style="background-color: #808080"> ProductsController.cs </span>.

3. Replace the code with:

```csharp
using Microsoft.AspNetCore.Mvc;
using FirstApi.Models;

namespace FirstApi.Controllers;

[Route("api/[controller]")]
[ApiController]
public class ProductsController : ControllerBase
{
    private static List<Product> products = new()
    {
        new Product { Id = 1, Name = "Laptop", Price = 999.99M },
        new Product { Id = 2, Name = "Phone", Price = 699.99M }
    };

    // GET: api/products
    [HttpGet]
    public ActionResult<IEnumerable<Product>> GetProducts()
    {
        return Ok(products);
    }

    // GET: api/products/1
    [HttpGet("{id}")]
    public ActionResult<Product> GetProduct(int id)
    {
        var product = products.Find(p => p.Id == id);
        if (product == null)
            return NotFound();
        return Ok(product);
    }

    // POST: api/products
    [HttpPost]
    public ActionResult<Product> AddProduct(Product product)
    {
        products.Add(product);
        return CreatedAtAction(nameof(GetProduct), new { id = product.Id }, product);
    }
}
```

### Step 5: Run and Test the API

1. Press F5 or click the Run button to start the API.

2. Open a browser or Postman and test the endpoints:

    * **GET** <span style="background-color: #808080"> https://localhost:5001/api/products </span> – Retrieve all products.
    
    * **GET** <span style="background-color: #808080"> https://localhost:5001/api/products/1 </span> – Retrieve a single product.
    
    * **POST** <span style="background-color: #808080"> https://localhost:5001/api/products </span> – Add a new product (send JSON body).

Example POST request (JSON):

```json
{
    "id": 3,
    "name": "Tablet",
    "price": 299.99
}
```

### Step 6: Add More Functionality (Optional)

To make the API more robust, consider:
* **Data Validation** (e.g., check for null values).

* **Database Integration** (use **Entity Framework Core**).

* **Error Handling** (global exception middleware).

* **Authentication** (JWT, OAuth).

# Conclusion

You’ve just built a basic RESTful API in C#! This is just the beginning — APIs can be extended with more features, security, and scalability.

#### Next Steps
* Explore Swagger/OpenAPI for API documentation.

* Learn about Dependency Injection in .NET.

* Try integrating a database with Entity Framework Core.


***Happy coding**!* 🚀

## Get in Touch

Have suggestions, feedback, or specific topics you'd like us to cover? Don't hesitate to reach out:

- 📧 Email: [okelo2014@gmail.com](mailto:okelo2014@gmail.com)
- 🐦 Twitter: [@KnightLord_](https://twitter.com/KnightLord_)
- 📸 Instagram: [i_am.shawn_](https://www.instagram.com/i_am.shawn_/)
- 📱 WhatsApp: [+254743198855](https://wa.me/+254743198855)


Thank you for   stopping by, and let the learning adventure begin! 🚀

### Appreciation:

[![Shawn](https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png)](https://buymeacoffee.com/f9w2rkj4rw
)

Thank you for being a part of this journey. Keep the flame alive. Here's to more learning and growth together!







