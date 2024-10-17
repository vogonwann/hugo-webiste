---
title: "Resolving 'Cannot access a disposed context instance' Error in ASP.NET Core"
date: 2024-10-17T12:00:00+01:00
tags: ["ASP.NET Core", "Entity Framework", "GraphQL", "HotChocolate"]
---

## Introduction

When developing an ASP.NET Core application and using Entity Framework (especially when using HotChocolate GraphQL library) to manage your database, you may encounter the following error:

```
Cannot access a disposed context instance. A common cause of this error is disposing a context instance that was resolved from dependency injection and then later trying to use the same context instance elsewhere in your application.
```

## Cause

This error typically occurs when a database context (`DbContext`) is attempted to be used after it has been disposed. This often happens in scenarios where the `DbContext` instance is not properly managed within your Dependency Injection (DI) system.

## Solution

### Use the Factory Pattern

The solution to this error is to use factory pattern to create a new instance of the `DbContext` each time it is needed. This way, you can avoid issues with managing the lifecycle of instances.

1. **Register the Factory in the DI Container**:

   In your `Program.cs`:

   ```csharp
   var connectionString = builder.Configuration.GetConnectionString("DefaultConnection");
   builder.Services..AddDbContextFactory<LibreBorrDbContext>(options => {
           options.UseSqlServer(connectionString); // or whatever DB server you are using
   });
   ```

2. **Use the Factory in Your Service**:

   In your service (`BookService`):

   ```csharp
   public class BookService : IBookService
   {
       private readonly IDbContextFactory _dbContextFactory;

       public BookService(IDbContextFactory dbContextFactory)
       {
           _dbContextFactory = dbContextFactory;
       }

       public async Task<List<Book>> GetBooks()
       {
           await using var context = _dbContextFactory.CreateDbContext();
           return await context.Books.ToListAsync();
       }
   }
   ```

## Conclusion

Using the factory pattern for managing `DbContext` instances allows you to avoid issues with disposal and lifecycle management of the context. This method provides greater control over the context and helps you eliminate errors like `Cannot access a disposed context instance`.

If you have any further questions or need assistance, feel free to reach out! 😊
