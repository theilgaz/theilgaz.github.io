---
layout: post
title: Simple REST API with AWS Lambda and DynamoDB
date: 2022-11-04 07:00
comments: true
external-url:
categories: 01&nbsp;Programlama
---

Building simple serverless .NET REST API with AWS Lambda and DynamoDB
We are going to create a new project with a simple API and a DynamoDB table. We will use the serverless.AspNetCoreMinimalAPI template.
In this project we need some NuGet packages. We will use AWSSDK.DynamoDBv2 and Amazon.Lambda.AspNetCoreServer.Hosting with FastEndpoints, FastEndpoints.Swagger and ValueOf packages.
Adding the Domain
We will add a Domain folder to the project. In this folder, we will add a User class and a Common folder.
In the Common folder, we will add UserId, FullName, EmailAddress and Password classes. You can find the code for these classes in the here.
|-- Domain
    |-- Common
        |-- EmailAddress.cs
        |-- FullName.cs
        |-- Password.cs
        |-- UserId.cs
    |-- User.cs
Adding the Contracts
We will add a Contracts folder to the project. In this folder, we will add Data, Requests and Responses folders.
In the Data folder, we will add UserDto class. In the Requests folder, we will add CreateUserRequest, DeleteUserRequest, GetUserRequest and UpdateUserRequest classes.
In the Responses folder, we will add UserResponse,GetAllUsersResponse and ValidationFailureResponse classes. You can find the code for these classes in the here.
|-- Contracts
    |-- Data
        |-- UserDto.cs
    |-- Requests
        |-- CreateUserRequest.cs
        |-- DeleteUserRequest.cs
        |-- GetUserRequest.cs
        |-- UpdateUserRequest.cs
    |-- Responses
        |-- GetAllUsersResponse.cs
        |-- UserResponse.cs
        |-- ValidationFailureResponse.cs
Adding the Mapping
We will add a Mapping folder to the project. In this folder, we will add ApiContractToDomainMapper, DomainToApiContractMapper, DomainToDtoMapper and DtoToDomainMapper classes.
You can find the code for these classes in the here.
|-- Mapping
    |-- ApiContractToDomainMapper.cs
    |-- DomainToApiContractMapper.cs
    |-- DomainToDtoMapper.cs
    |-- DtoToDomainMapper.cs
Adding the Repositories
We will add a Repositories folder to the project. In this folder, we will add IUserRepository interface and UserRepository class.
You can find the code for this interface and class in the here.
|-- Repositories
    |-- IUserRepository.cs
    |-- UserRepository.cs
Adding the Services
We will add a Services folder to the project. In this folder, we will add IUserService interface and UserService class.
You can find the code for this interface and class in the here.
|-- Services
    |-- IUserService.cs
    |-- UserService.cs
Adding the Endpoints
We will add a Endpoints folder to the project. In this folder, we will add CreateUserEndpoint, DeleteUserEndpoint, GetUserEndpoint and UpdateUserEndpoint classes.
You can find the code for these classes in the here.
|-- Endpoints
    |-- CreateUserEndpoint.cs
    |-- DeleteUserEndpoint.cs
    |-- GetUserEndpoint.cs
    |-- UpdateUserEndpoint.cs
Adding the Summaries
We will add a Summaries folder to the project. In this folder, we will add CreateUserSummary, DeleteUserSummary, GetUserSummary and UpdateUserSummary classes.
You can find the code for these classes in the here.
|-- Summaries
    |-- CreateUserSummary.cs
    |-- DeleteUserSummary.cs
    |-- GetUserSummary.cs
    |-- UpdateUserSummary.cs
Adding the Validators
We will add a Validation folder to the project. In this folder, we will add CreateUserRequestValidator, UpdateUserRequestValidator and ValidationExceptionMiddleware classes.
You can find the code for these classes in the here.
|-- Validation
    |-- CreateUserRequestValidator.cs
    |-- UpdateUserRequestValidator.cs
    |-- ValidationExceptionMiddleware.cs
Program.cs Configurations
Enabling Lambda Hosting
We need to enable Lambda hosting in Program.cs file.
builder.Services.AddAWSLambdaHosting(LambdaEventSource.HttpApi);
FastEndpoints Configuration
Now we add FastEndpoints and swagger services.
builder.Services.AddFastEndpoints();
builder.Services.AddSwaggerDoc();
DynamoDB Configuration
We need to configure DynamoDB in Program.cs file. We will use AmazonDynamoDBClient to connect to DynamoDB.
builder.Services.AddSingleton<IAmazonDynamoDB>(_ => new AmazonDynamoDBClient(RegionEndpoint.EUWest1));
Adding Repository and Service
We will add UserRepository and UserService to the services.
builder.Services.AddSingleton<IUserRepository>(provider =>
    new UserRepository(provider.GetRequiredService<IAmazonDynamoDB>(),
        config.GetValue<string>("Database:TableName")));
builder.Services.AddSingleton<IUserService, UserService>();
Adding Validators
We will add ValidationExceptionMiddleware to the services.
app.UseMiddleware<ValidationExceptionMiddleware>();
app.UseFastEndpoints(x =>
{
    x.ErrorResponseBuilder = (failures, _) =>
    {
        return new ValidationFailureResponse
        {
            Errors = failures.Select(y => y.ErrorMessage).ToList()
        };
    };
});
Adding Database Table Name to Configuration
We will add Database:TableName to the appsettings.json configuration file.
{
  "Database": {
    "TableName": "users"
  }
}
Deploying the project
We will deploy the project to AWS Lambda using the following command.
dotnet lambda deploy-function
Creating the Database Table
In AWS Console, go to DynamoDB service and create a table with the name users. The table should have a part key with the name pk and type String. The table should have a sort key with the name sk and type String.
After creating the table, click the Actions button and select Create access control policy. Identity provider should be Login with Amazon and all permissions should be selected. Click Generate policy button## SimpleApiWithDynamoDB

We are going to create a new project with a simple API and a DynamoDB table. We will use the `serverless.AspNetCoreMinimalAPI` template. 

In this project we need some NuGet packages. We will use `AWSSDK.DynamoDBv2` and `Amazon.Lambda.AspNetCoreServer.Hosting` with `FastEndpoints`, `FastEndpoints.Swagger` and `ValueOf` packages.


#### Adding the Domain

We will add a `Domain` folder to the project. In this folder, we will add a `User` class and a `Common` folder. 

In the `Common` folder, we will add `UserId`, `FullName`, `EmailAddress` and `Password` classes. You can find the code for these classes in the [here](/SimpleApiWithDynamoDb/src/SimpleApiWithDynamoDb/Domain/).

```
|-- Domain
    |-- Common
        |-- EmailAddress.cs
        |-- FullName.cs
        |-- Password.cs
        |-- UserId.cs
    |-- User.cs
```

#### Adding the Contracts

We will add a `Contracts` folder to the project. In this folder, we will add `Data`, `Requests` and `Responses` folders. 

In the `Data` folder, we will add `UserDto` class. In the `Requests` folder, we will add `CreateUserRequest`, `DeleteUserRequest`, `GetUserRequest` and `UpdateUserRequest` classes. 

In the `Responses` folder, we will add `UserResponse`,`GetAllUsersResponse` and `ValidationFailureResponse` classes. You can find the code for these classes in the [here](/SimpleApiWithDynamoDb/src/SimpleApiWithDynamoDb/Contracts/).

```
|-- Contracts
    |-- Data
        |-- UserDto.cs
    |-- Requests
        |-- CreateUserRequest.cs
        |-- DeleteUserRequest.cs
        |-- GetUserRequest.cs
        |-- UpdateUserRequest.cs
    |-- Responses
        |-- GetAllUsersResponse.cs
        |-- UserResponse.cs
        |-- ValidationFailureResponse.cs
```

#### Adding the Mapping

We will add a `Mapping` folder to the project. In this folder, we will add `ApiContractToDomainMapper`, `DomainToApiContractMapper`, `DomainToDtoMapper` and `DtoToDomainMapper` classes.

You can find the code for these classes in the [here](/SimpleApiWithDynamoDb/src/SimpleApiWithDynamoDb/Mapping/).

```
|-- Mapping
    |-- ApiContractToDomainMapper.cs
    |-- DomainToApiContractMapper.cs
    |-- DomainToDtoMapper.cs
    |-- DtoToDomainMapper.cs
```

#### Adding the Repositories

We will add a `Repositories` folder to the project. In this folder, we will add `IUserRepository` interface and `UserRepository` class.

You can find the code for this interface and class in the [here](/SimpleApiWithDynamoDb/src/SimpleApiWithDynamoDb/Repositories/).

```
|-- Repositories
    |-- IUserRepository.cs
    |-- UserRepository.cs
```
 
#### Adding the Services

We will add a `Services` folder to the project. In this folder, we will add `IUserService` interface and `UserService` class.

You can find the code for this interface and class in the [here](/SimpleApiWithDynamoDb/src/SimpleApiWithDynamoDb/Services/).

```

|-- Services
    |-- IUserService.cs
    |-- UserService.cs
```

#### Adding the Endpoints

We will add a `Endpoints` folder to the project. In this folder, we will add `CreateUserEndpoint`, `DeleteUserEndpoint`, `GetUserEndpoint` and `UpdateUserEndpoint` classes.

You can find the code for these classes in the [here](/SimpleApiWithDynamoDb/src/SimpleApiWithDynamoDb/Endpoints/).

```
|-- Endpoints
    |-- CreateUserEndpoint.cs
    |-- DeleteUserEndpoint.cs
    |-- GetUserEndpoint.cs
    |-- UpdateUserEndpoint.cs
```


#### Adding the Summaries

We will add a `Summaries` folder to the project. In this folder, we will add `CreateUserSummary`, `DeleteUserSummary`, `GetUserSummary` and `UpdateUserSummary` classes.

You can find the code for these classes in the [here](/SimpleApiWithDynamoDb/src/SimpleApiWithDynamoDb/Summaries/).

```
|-- Summaries
    |-- CreateUserSummary.cs
    |-- DeleteUserSummary.cs
    |-- GetUserSummary.cs
    |-- UpdateUserSummary.cs
```

#### Adding the Validators

We will add a `Validation` folder to the project. In this folder, we will add `CreateUserRequestValidator`, `UpdateUserRequestValidator` and `ValidationExceptionMiddleware` classes.

You can find the code for these classes in the [here](/SimpleApiWithDynamoDb/src/SimpleApiWithDynamoDb/Validation/).

```
|-- Validation
    |-- CreateUserRequestValidator.cs
    |-- UpdateUserRequestValidator.cs
    |-- ValidationExceptionMiddleware.cs
```

#### Program.cs Configurations

##### Enabling Lambda Hosting

We need to enable Lambda hosting in `Program.cs` file.

```csharp
builder.Services.AddAWSLambdaHosting(LambdaEventSource.HttpApi);
```

##### FastEndpoints Configuration

Now we add `FastEndpoints` and swagger services.

```csharp
builder.Services.AddFastEndpoints();
builder.Services.AddSwaggerDoc();
```

##### DynamoDB Configuration

We need to configure DynamoDB in `Program.cs` file. We will use `AmazonDynamoDBClient` to connect to DynamoDB.

```csharp
builder.Services.AddSingleton<IAmazonDynamoDB>(_ => new AmazonDynamoDBClient(RegionEndpoint.EUWest1));
```

##### Adding Repository and Service

We will add `UserRepository` and `UserService` to the services.

```csharp
builder.Services.AddSingleton<IUserRepository>(provider =>
    new UserRepository(provider.GetRequiredService<IAmazonDynamoDB>(),
        config.GetValue<string>("Database:TableName")));
builder.Services.AddSingleton<IUserService, UserService>();
```

##### Adding Validators

We will add ValidationExceptionMiddleware to the services.

```csharp
app.UseMiddleware<ValidationExceptionMiddleware>();
app.UseFastEndpoints(x =>
{
    x.ErrorResponseBuilder = (failures, _) =>
    {
        return new ValidationFailureResponse
        {
            Errors = failures.Select(y => y.ErrorMessage).ToList()
        };
    };
});

```

##### Adding Database Table Name to Configuration

We will add `Database:TableName` to the `appsettings.json` configuration file.

```
{
  "Database": {
    "TableName": "users"
  }
}
```

#### Deploying the project

We will deploy the project to AWS Lambda using the following command.

```
dotnet lambda deploy-function
```

#### Creating the Database Table

In AWS Console, go to DynamoDB service and create a table with the name `users`. The table should have a part key with the name `pk` and type `String`. The table should have a sort key with the name `sk` and type `String`. 

After creating the table, click the `Actions` button and select `Create access control policy`. `Identity provider` should be `Login with Amazon` and all permissions should be selected. Click `Generate policy` button. 

The generated policy will be like this:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "dynamodb:BatchGetItem",
        "dynamodb:BatchWriteItem",
        "dynamodb:DeleteItem",
        "dynamodb:GetItem",
        "dynamodb:PutItem",
        "dynamodb:Query",
        "dynamodb:UpdateItem"
      ],
      "Resource": [
        "arn:aws:dynamodb:eu-west-1:YOUR_ACCOUNT:table/users"
      ],
      "Condition": {
        "ForAllValues:StringEquals": {
          "dynamodb:LeadingKeys": [
            "${www.amazon.com:user_id}"
          ]
        }
      }
    }
  ]
}
```

We don't need the `Condition` part. So we will remove it. The policy will be like this:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "dynamodb:BatchGetItem",
        "dynamodb:BatchWriteItem",
        "dynamodb:DeleteItem",
        "dynamodb:GetItem",
        "dynamodb:PutItem",
        "dynamodb:Query",
        "dynamodb:UpdateItem"
      ],
      "Resource": [
        "arn:aws:dynamodb:eu-west-1:YOUR_ACCOUNT:table/users"
      ]
    }
  ]
}
```

Now copy the policy. We will use it in the next step.

#### Configuring the Policy

In AWS Console, go to Lambda service and select the function we created. In the `Configuration` tab, click the `Permissions` page. Click the execution role and it will open the IAM service. In the IAM service, click the `Add permissions` button then click the `Create inline policy` button. 

Go to JSON tab and paste the policy we created in the previous step. Click `Review policy` button. Give a name to the policy and click `Create policy` button.

#### Congratulations!

We have created a simple API with DynamoDB. You can test the API using the Postman.