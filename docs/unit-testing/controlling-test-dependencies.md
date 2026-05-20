# Controlling Test Dependencies

## Controlling the Test Environment

We've discussed that our tests must operate as controlled experiments. This means that we need the same inputs to the test each time it runs. But what happens if our function communicates with a database, a file system, or a web service? How can we control the data that our test depends on?

## Refactoring toward a Decoupled Design

The first step is to refactor the system under test to decouple it from any external dependencies. Let's walk through two examples. We will provide a before and after version of the code for each example.

There are two issues that we will address in both cases:

- The functions violate the **Single Responsibility Principle (SRP)**. They do more than one thing.
- The functions carry details about their environmental context rather than accepting dependencies as parameters.

### Example 1: A Date Dependent Function

**Before Refactoring**

```csharp
public string GetGreeting()
{
    // Gets the current date and time
    var currentDate = DateTime.Now;

    // Returns the appropriate greeting based on the current time
    if (currentDate.Hour >= 17)
        return "Good evening";
    else if (currentDate.Hour >= 12)
        return "Good afternoon";
    else
        return "Good morning";
}
```

What happens when we try to test this function? If we test it in the morning, it will return "Good morning". If we test it in the afternoon, it will return "Good afternoon". What would we assert the result against?

**After Refactoring**

```csharp
public string GetGreeting(DateTime currentDate)
{
    // Returns the appropriate greeting based on the current time
    if (currentDate.Hour >= 17)
        return "Good evening";
    else if (currentDate.Hour >= 12)
        return "Good afternoon";
    else
        return "Good morning";
}
```

The solution is to refactor the function to accept the current date as a parameter. The result _depends on_ the date, therefore the date should be input to the function.

This is now a **pure function** that only depends on the input parameter. It will always return the same output when provided the same input.

**Example Unit Test**

```csharp
[Test]
public void GetGreeting_ReturnsGoodMorning_WhenCurrentDateIsBeforeNoon()
{
    var inputDate = new DateTime(2026, 1, 1, 11, 59, 59);
    var result = GetGreeting(inputDate);
    Assert.Equal("Good morning", result);
}
```

To test the function, we can create a Date object for whichever greeting we want to test. In this example we test the boundary condition: 11:59 AM at 59 seconds past the minute should return "Good morning".

We could test the other greetings as well, possibly using parameterized tests.

### Example 2: A Database Dependent Function

**Before Refactoring**

```csharp
public decimal CalculateDiscount(int customerId, int productId)
{
    Customer customer = GetCustomerFromDatabase(customerId);
    Product product = GetProductFromDatabase(productId);

    decimal discountRate = 0.0;
    decimal price = product.Price;

    if (customer.IsMember)
        discountRate = 0.1;

    return price * discountRate;
}
```

This function depends on a database to fetch the customer and product. We want the unit tests to run quickly and independently of each other. We also need the test to be repeatable. What happens if the data in the database changes between tests? How can we ensure that our test customer (e.g. customerId = 1) is a member every time the test runs?

**After Refactoring**

```csharp
public decimal CalculateDiscount(Customer customer, Product product)
{
    decimal discountRate = 0.0;
    decimal price = product.Price;

    if (customer.IsMember)
        discountRate = 0.1;

    return price * discountRate;
}
```

The solution is to refactor the function to accept the customer and product as parameters. The result _depends on_ the customer and product, therefore the customer and product should be inputs to the function.

In many systems we would take this a step further and pass in the discount rate as a parameter. This would ensure that `CalculateDiscount` truly has only one responsibility and does not hold its own assumptions.

**Example Unit Test**

```csharp
[Test]
public void discount_is_correct_for_member_customer()
{
    var customer = new Customer { IsMember = true };
    var product = new Product { Price = 100 };
    var result = CalculateDiscount(customer, product);
    Assert.Equal(90, result);
}
```

To test the function, we can create a Customer and Product object for whichever discount we want to test. In this example we test that a member purchasing a $100 product gets a $10 discount.
