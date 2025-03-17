---
title: Understanding Mocking and Stubbing in .NET and C#
categories: [Technology, Debugging, C#]
tags: [C#, Debugging]
image: https://images.unsplash.com/photo-1483058712412-4245e9b90334?fm=jpg&q=60&w=3000&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTh8fGJ1c2luZXNzJTIwdGVjaG5vbG9neXxlbnwwfHwwfHx8MA%3D%3D
---

When it comes to unit testing in .NET and C#, two essential concepts that developers often encounter are *mocking* and *stubbing*. Both techniques are used to isolate the code being tested, but they serve different purposes. In this blog post, we’ll explore what mocking and stubbing are, when to use them, and provide code examples to illustrate their usage.

## What is Stubbing?
**Stubbing** is a technique used to create a controlled environment for testing by providing predefined responses to method calls. Stubs are typically used when you want to isolate the unit of work from its dependencies, allowing you to focus on the behavior of the code under test.

### Example of Stubbing
Let’s say we have a simple service that retrieves user information from a database. We want to test a method that processes user data without actually hitting the database.

```csharp
public interface IUserRepository
{
    User GetUser ById(int id);
}

public class UserService
{
    private readonly IUserRepository _userRepository;

    public UserService(IUser Repository userRepository)
    {
        _userRepository = userRepository;
    }

    public string GetUser Name(int id)
    {
        var user = _userRepository.GetUser ById(id);
        return user?.Name ?? "Unknown User";
    }
}

// Test using a stub
public class UserServiceTests
{
    [Fact]
    public void GetUser Name_ReturnsCorrectName()
    {
        // Arrange
        var stubUser Repository = new StubUser Repository { User = new User { Name = "John Doe" } };
        var userService = new UserService(stubUser Repository);

        // Act
        var result = userService.GetUser Name(1);

        // Assert
        Assert.Equal("John Doe", result);
    }
}

public class StubUser Repository : IUserRepository
{
    public User User { get; set; }

    public User GetUser ById(int id)
    {
        return User;
    }
}
```

In this example, StubUser Repository is a simple stub that returns a predefined user. This allows us to test the GetUser Name method without needing a real database.

## What is Mocking?
**Mocking** is a more advanced technique that not only allows you to define return values for method calls but also verifies that certain interactions with the mock object occurred as expected. Mocks are useful when you want to ensure that specific methods are called with the correct parameters.

### Example of Mocking
Using a mocking framework like *Moq*, we can create a mock of the IUser Repository and verify interactions.

```csharp
using Moq;

public class UserServiceTests
{
    [Fact]
    public void GetUser Name_CallsGetUser ById()
    {
        // Arrange
        var mockUser Repository = new Mock<IUser Repository>();
        mockUser Repository.Setup(repo => repo.GetUser ById(It.IsAny<int>()))
                          .Returns(new User { Name = "Jane Doe" });
        var userService = new UserService(mockUser Repository.Object);

        // Act
        var result = userService.GetUser Name(1);

        // Assert
        Assert.Equal("Jane Doe", result);
        mockUser Repository.Verify(repo => repo.GetUser ById(1), Times.Once);
    }
}
```

In this example, we use Moq to create a mock of IUser Repository. We set up the mock to return a specific user when GetUser ById is called. After calling GetUser Name, we verify that GetUser ById was called exactly once with the expected parameter.

## When to Use Stubbing vs. Mocking
Use Stubbing when you need to provide simple responses to method calls without caring about how many times or in what order those methods are called.
Use Mocking when you need to verify interactions with the dependencies, such as ensuring that certain methods are called with specific parameters.

# Conclusion
Mocking and stubbing are powerful techniques in unit testing that help you isolate your code and ensure it behaves as expected. By understanding the differences between the two and knowing when to use each, you can write more effective and maintainable tests in your .NET applications. *Happy testing!*

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