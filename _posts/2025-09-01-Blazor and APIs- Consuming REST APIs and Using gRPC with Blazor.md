---
title: Blazor and APIs - Consuming REST APIs and Using gRPC with Blazor
categories: [Technology, Blazor, C#]
tags: [C#, API]
author: Shawn Ng'iela
image: /Images/blazorAPI.png
---

Blazor is a powerful framework for building interactive web applications using C# and .NET. One of the common scenarios in modern web development is integrating your frontend with backend services via APIs. In this blog post, we'll explore how to consume REST APIs in Blazor applications and introduce how to use gRPC with Blazor for efficient communication.

## Consuming REST APIs in Blazor

REST (Representational State Transfer) APIs are widely used to expose backend services over HTTP. Blazor, whether Server or WebAssembly, can easily consume REST APIs using the built-in `HttpClient` class.

### Setting Up HttpClient in Blazor

- **Blazor WebAssembly:** `HttpClient` is preconfigured to use the browser's fetch API.
- **Blazor Server:** You need to register `HttpClient` in the dependency injection container.

Example registration in `Program.cs` (Blazor Server):

```csharp
builder.Services.AddHttpClient();
```
This gives you access to an HttpClient instance configured for your app.

## Making HTTP Requests
You can inject HttpClient into your components or services and use it to make HTTP calls.

To retrieve data from an API, you can use methods like GetAsync or the more convenient GetFromJsonAsync<T>() which automatically deserializes JSON responses into C# objects.

Example:

```csharp
@inject HttpClient Http
@code {
    private WeatherForecast[] forecasts;
    protected override async Task OnInitializedAsync()
    {
        forecasts = await Http.GetFromJsonAsync<WeatherForecast[]>("https://api.example.com/weather");
    }
}
```
When the JSON response matches this structure, GetFromJsonAsync<WeatherForecast[]>() will automatically map the data to your objects.

## Handling JSON Data
Blazor uses System.Text.Json by default for JSON serialization and deserialization. You can easily map JSON responses to C# classes.

```csharp
public class WeatherForecast
{
    public DateTime Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
```
When the JSON response matches this structure, GetFromJsonAsync<WeatherForecast[]>() will automatically map the data to your objects.

## Posting Data to REST APIs
Blazor also supports sending data to APIs, such as creating or updating resources. You can use PostAsJsonAsync<T>() to serialize your C# object to JSON and send it in the request body.

Example:

```csharp
var newItem = new Item { Name = "Sample", Quantity = 5 };
var response = await Http.PostAsJsonAsync("https://api.example.com/items", newItem);
```
Similarly, you can use PutAsJsonAsync for PUT requests or DeleteAsync for DELETE requests.

## Additional Tips
* Error Handling: Always check the response status and handle exceptions to make your app robust.
* Headers and Authentication: You can customize headers (e.g., add authorization tokens) by configuring the HttpClient or using HttpRequestMessage.
* Cancellation: Use CancellationToken to cancel long-running requests if needed.
* Timeouts: Configure timeouts on HttpClient to avoid hanging requests.

## Using gRPC with Blazor
gRPC is a modern, high-performance RPC framework that uses HTTP/2 and Protocol Buffers for efficient communication. It is especially useful when you need strongly typed contracts, low latency, and streaming capabilities.

## Why Use gRPC with Blazor?
* Efficient Binary Serialization: Protocol Buffers serialize data compactly and quickly.
* Strongly Typed Contracts: Service definitions are shared between client and server, reducing errors.
* Streaming Support: Enables real-time data streams between client and server.
* Performance: Often faster than REST due to binary protocol and HTTP/2.

## gRPC Support in Blazor
* Blazor Server: Can use the full .NET gRPC client to call gRPC services directly.
* Blazor WebAssembly: Uses gRPC-Web, a variant that works over HTTP/1.1 and is compatible with browsers.

## Setting Up gRPC in Blazor Server
1. Add the gRPC client NuGet package: 

```bash
dotnet add package Grpc.Net.Client
```

2. Inject and use the gRPC client in your component or service: 

```csharp
@inject Greeter.GreeterClient GreeterClient
@code {
    private string greeting;
    protected override async Task OnInitializedAsync()
    {
        var reply = await GreeterClient.SayHelloAsync(new HelloRequest { Name = "Blazor" });
        greeting = reply.Message;
    }
}
```
Here, Greeter.GreeterClient is the client generated from your .proto file.

## Using gRPC-Web in Blazor WebAssembly
Since browsers don’t support HTTP/2 trailers required by standard gRPC, gRPC-Web adapts gRPC to work over HTTP/1.1.

1. Add the Grpc.Net.Client.Web package to your client project.

```bash
dotnet add package Grpc.Net.Client.Web
```

2. Configure the gRPC-Web channel in your client:

```csharp
var httpHandler = new GrpcWebHandler(GrpcWebMode.GrpcWebText, new HttpClientHandler());
var channel = GrpcChannel.ForAddress("https://localhost:5001", new GrpcChannelOptions { HttpHandler = httpHandler });
var client = new Greeter.GreeterClient(channel);
```

3. Call gRPC methods as usual. 

### Important Considerations
* Server Support: Your server must support gRPC-Web and be configured with proper CORS policies.
* Feature Limitations: gRPC-Web does not support all gRPC features, such as full-duplex streaming.
* Security: Use HTTPS to secure gRPC-Web traffic.

By understanding these details, you can confidently integrate REST APIs and gRPC services into your Blazor applications, leveraging the best of both worlds depending on your app’s needs.

# Conclusion
Blazor provides excellent support for integrating with backend APIs, whether you prefer the simplicity and ubiquity of REST or the performance and strong typing of gRPC. For most applications, consuming REST APIs with HttpClient is straightforward and effective. However, if your app demands high performance and real-time communication, exploring gRPC with Blazor is a great choice.

## Get in Touch

Have suggestions, feedback, or specific topics you'd like us to cover? Don't hesitate to reach out:

- 📧 Email: [okelo2014@gmail.com](mailto:okelo2014@gmail.com)
- 🐦 Twitter: [@KnightLord_](https://twitter.com/KnightLord_)
- 📸 Instagram: [i_am.shawn_](https://www.instagram.com/i_am.shawn_/)
- 📱 WhatsApp: [+254743198855](https://wa.me/+254743198855)


Thank you for   stopping by, and let the learning adventure begin! 🚀

### Appreciation:

[![Shawn](/Images/buymeacoffee.png)](https://ko-fi.com/i_am_shawn
)

Thank you for being a part of this journey. Keep the flame alive. Here's to more learning and growth together!