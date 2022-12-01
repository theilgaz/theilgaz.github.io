---
layout: post
title: Building Serverless .NET Minimal API (using Controller) with AWS Lambda
date: 2022-11-04 07:00
comments: true
external-url:
categories: 01&nbsp;Programlama
---
## MinimalLambda

We will create a minimal API using `AWS Lambda` and `.NET 6`. It will be a simple API with a single MapGet method and a single controller which is a simple calculator class with four methods.

#### Creating a new project

We are going to use the `serverless.AspNetCoreMinimalAPI` template. You can create a new project using the following command:

```bash
dotnet new serverless.AspNetCoreMinimalAPI --name MinimalLambda --output MinimalLambda
```

or using the Rider IDE.

![Lambda ASP.NET Core Minimal API](./images/minimal-api-create-project.png)

#### Configuring the project

We need to configure `aws-lambda-tools-defaults.json` file.

This time we will use `function-handler` as `MinimalLambda`. Then we can remove `serverless.template` file.

![Project Configurations](./images/minimal-api-project-configurations.png)

#### Looking at the code

In the `Program.cs` file, we have a `CreateHostBuilder` method. This method will create a new `IHostBuilder` instance.

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();

// Add AWS Lambda support. When application is run in Lambda Kestrel is swapped out as the web server with Amazon.Lambda.AspNetCoreServer. This
// package will act as the webserver translating request and responses between the Lambda event source and ASP.NET Core.
builder.Services.AddAWSLambdaHosting(LambdaEventSource.RestApi);

var app = builder.Build();


app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.MapGet("/", () => "Welcome to running ASP.NET Core Minimal API on AWS Lambda");

app.Run();
```

`LambdaEventSource.RestApi` is the event source that will be used to handle the request. If we change it to `LambdaEventSource.HttpApi`, we will be able to use the new HTTP API.

```csharp
builder.Services.AddAWSLambdaHosting(LambdaEventSource.HttpApi);
```

In the Controllers folder, we have a `CalculatorController.cs` file. This file contains a `Calculator` class with four methods. We can use these methods to perform simple calculations.

#### Deploying the project

Now that we have created the project, we can deploy it to AWS Lambda. Go to the project directory and run the following command:

```bash
dotnet lambda deploy-function
```

With `"function-url-enable": true` in `aws-lambda-tools-defaults.json` file, we can get the function URL after deploying the project.

Now we can use the function URL to access the API.

They can be accessed using the following URLs:

- `https://<function-url>/calculator/add/1/2`
- `https://<function-url>/calculator/subtract/1/2`
- `https://<function-url>/calculator/multiply/1/2`
- `https://<function-url>/calculator/divide/1/2`

With `Postman`, we can send a request to these URLs and get the result.

#### Congratulations!

You have created a minimal API using `AWS Lambda` and `.NET 6`.