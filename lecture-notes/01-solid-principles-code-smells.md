# 01: SOLID Principles and Code Smells

## GitHub

This course will use **GitHub** and **GitHub Classroom** to manage our development. Begin by clicking this link [https://classroom.github.com/a/CSDw80kn](https://classroom.github.com/a/CSDw80kn). You will be prompted to accept an assignment. Click on the **Accept this assignment** button. **GitHub Classroom** will create a new repository. You will use this repository to submit your formative (non-graded) and summative (graded) assessments.

---

### Development Workflow

By default, **GitHub Classroom** creates an empty repository. Firstly, you must create a **README** and `.gitignore` file. **GitHub** allows new files to be created once the repository is created.

---

### Create a README

Click the **Add file** button, then the **Create new file** button. Name your file `README.md` (Markdown), then click on the **Commit new file** button. You should see a new file in your formative assessments repository called `README.md` and the `main` branch.

> **Resource:** <https://guides.github.com/features/mastering-markdown/>

---

### Create a .gitignore File

Like before, click the **Add file** button and then the **Create new file** button. Name your file `.gitignore`. A `.gitignore` template dropdown will appear on the right-hand side of the screen. Select the **Unity** `.gitignore` template. Click on the **Commit new file** button. You should see a new file in your formative assessments repository called `.gitignore`.

> **Resource:** <https://git-scm.com/docs/gitignore>

---

### Clone a Repository

Open up **Git Bash** or whatever alternative you see fit on your computer. Clone your formative assessments repository to a location on your computer using the command: `git clone <repository URL>`.

> **Resource:** <https://git-scm.com/docs/git-clone>

---

### Commit Message Conventions

You should follow the **conventional commits** convention when committing changes to your repository. A **conventional commit** consists of a **type**, **scope** and **description**. The **type** and **description** are mandatory, while the **scope** is optional. The **type** must be one of the following:

- **build**: Changes that affect the build system or external dependencies
- **chore**: Regular code maintenance, such as refactoring or updating dependencies
- **ci**: Changes to our CI configuration files and scripts
- **docs**: Documentation only changes
- **feat**: A new feature
- **fix**: A bug fix
- **perf**: A code change that improves performance
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- **test**: Adding missing tests or correcting existing tests

The **scope** is a phrase describing the codebase section affected by the change. For example, you can use the scope `pong` if you are working on the **formative assessment** for **Pong**. If you are working on the **formative assessment** for **Space Invaders**, use the scope `space invaders`.

The **description** is a short description of the change. It should be written in the imperative mood, meaning it should be written as if you are giving a command or instruction. For example, "add a new feature" instead of "added a new feature".

Here are some examples of **conventional commits**:

- `feat(pong): add a new feature`
- `fix(space invaders): fix a bug`
- `docs(breakout): update documentation`

> **Resource:** <https://www.conventionalcommits.org/en/v1.0.0/>

---

## SOLID Principles

**SOLID** is an acronym for five design principles intended to make software designs more understandable, flexible, and maintainable. The principles are a subset of many principles promoted by **Robert C. Martin**.

> **Resource:** <https://en.wikipedia.org/wiki/SOLID>

---

### Single Responsibility Principle (SRP)

A class should have one, and only one, reason to change. This means that a class should have only one job. Here is an example of a class that violates the **Single Responsibility Principle**:

```csharp
public class User
{
    private string name;
    private string email;

    public string Name { get => name; set => name = value; }
    public string Email { get => email; set => email = value; }

    public void Save()
    {
        // Save the user to the database
    }

    public void SendEmail()
    {
        // Send an email to the user
    }

    public void Register()
    {
        Save();
        SendEmail();
    }
}
```

The `User` class has two responsibilities: saving the user to the database and sending an email to the user. It would be better to split the class into two separate classes, each with a single responsibility.

Here is an example of a class that follows the **Single Responsibility Principle**:

```csharp
public class User
{
    private string name;
    private string email;

    public string Name { get => name; set => name = value; }
    public string Email { get => email; set => email = value; }
}

public class UserRepository
{
    public void Save(User user)
    {
        // Save the user to the database
    }
}

public class EmailService
{
    public void SendEmail(User user)
    {
        // Send an email to the user
    }
}

public class RegistrationService
{
    private UserRepository userRepository;
    private EmailService emailService;

    public RegistrationService(UserRepository userRepository, EmailService emailService)
    {
        this.userRepository = userRepository;
        this.emailService = emailService;
    }

    public void Register(User user)
    {
        userRepository.Save(user);
        emailService.SendEmail(user);
    }
}
```

---

### Open/Closed Principle (OCP)

Software entities should be open for extension but closed for modification. This means that you should be able to extend the behavior of a class without modifying its source code. Here is an example of a class that violates the **Open/Closed Principle**:

```csharp
public class Shape
{
    protected string type;

    public string Type { get => type; set => type = value; }

    public double Area()
    {
        if (type == "Circle")
        {
            return CalculateCircleArea();
        }
        else if (type == "Rectangle")
        {
            return CalculateRectangleArea();
        }
        else
        {
            throw new Exception("Unknown shape type");
        }
    }

    private double CalculateCircleArea()
    {
        // Calculate the area of a circle
    }

    private double CalculateRectangleArea()
    {
        // Calculate the area of a rectangle
    }
}
```

The `Shape` class has a method called `Area` that calculates the area of a shape. The method uses a conditional statement to determine the type of shape and calculate the area accordingly. If you want to add a new shape, you would have to modify the `Area` method, which violates the **Open/Closed Principle**.

Here is an example of a class that follows the **Open/Closed Principle**:

```csharp
public abstract class Shape
{
    public abstract double Area();
}

public class Circle : Shape
{
    public override double Area()
    {
        // Calculate the area of a circle
    }
}

public class Rectangle : Shape
{
    public override double Area()
    {
        // Calculate the area of a rectangle
    }
}
```

The `Shape` class is now an abstract class with an abstract method called `Area`. The `Circle` and `Rectangle` classes inherit from the `Shape` class and implement the `Area` method. If you want to add a new shape, you can create a new class that inherits from the `Shape` class and implements the `Area` method without modifying the existing code.

---

### Liskov Substitution Principle (LSP)

Subtypes must be substitutable for their base types. This means that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. Here is an example of a class that violates the **Liskov Substitution Principle**:

```csharp
public class Rectangle
{
    private int width;
    private int height;

    public int Width { get => width; set => width = value; }
    public int Height { get => height; set => height = value; }

    public int Area()
    {
        return width * height;
    }
}
```

The `Rectangle` class has a `Width` and `Height` property and an `Area` method that calculates the area of the rectangle. The `Square` class inherits from the `Rectangle` class and overrides the `Width` and `Height` properties to ensure that they are always equal. This violates the **Liskov Substitution Principle** because a `Square` is not a proper substitute for a `Rectangle`.

Here is an example of a class that follows the **Liskov Substitution Principle**:

```csharp

public abstract class Shape
{
    public abstract int Area();
}

public class Rectangle : Shape
{
    private int width;
    private int height;

    public int Width { get => width; set => width = value; }
    public int Height { get => height; set => height = value; }

    public override int Area()
    {
        return width * height;
    }
}

public class Square : Shape
{
    private int side;

    public int Side { get => side; set => side = value; }

    public override int Area()
    {
        return side * side;
    }
}
```

The `Shape` class is now an abstract class with an abstract method called `Area`. The `Rectangle` and `Square` classes inherit from the `Shape` class and implement the `Area` method. Both classes are proper substitutes for the `Shape` class because they implement the `Area` method correctly.

---

### Interface Segregation Principle (ISP)

Clients should not be forced to depend on interfaces they do not use. This means that you should split large interfaces into smaller, more specific interfaces so that clients only have to implement the methods they are interested in. Here is an example of an interface that violates the **Interface Segregation Principle**:

```csharp
public interface IShape
{
    void Draw();
    void Resize();
    void Rotate();
}
```

The `IShape` interface has three methods: `Draw`, `Resize`, and `Rotate`. If a client is only interested in drawing shapes and does not need to resize or rotate them, they are forced to implement those methods anyway, which violates the **Interface Segregation Principle**.

Here is an example of an interface that follows the **Interface Segregation Principle**:

```csharp
public interface IDrawable
{
    void Draw();
}

public interface IResizable
{
    void Resize();
}

public interface IRotatable
{
    void Rotate();
}
```

The `IDrawable`, `IResizable`, and `IRotatable` interfaces are smaller, more specific interfaces that represent different aspects of a shape. Clients can now implement only the interfaces they are interested in without being forced to implement unnecessary methods.

---

### Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions. This means that you should use interfaces or abstract classes to decouple high-level modules from low-level modules. Here is an example of a class that violates the **Dependency Inversion Principle**:

```csharp
public class UserService
{
    private UserRepository userRepository;

    public UserService()
    {
        userRepository = new UserRepository();
    }

    public void SaveUser(User user)
    {
        userRepository.Save(user);
    }
}
```

The `UserService` class depends directly on the `UserRepository` class, which violates the **Dependency Inversion Principle**. If you want to use a different type of repository, you would have to modify the `UserService` class.

Here is an example of a class that follows the **Dependency Inversion Principle**:

```csharp
public interface IUserRepository
{
    void Save(User user);
}

public class UserRepository : IUserRepository
{
    public void Save(User user)
    {
        // Save the user to the database
    }
}

public class UserService
{
    private IUserRepository userRepository;

    public UserService(IUserRepository userRepository)
    {
        this.userRepository = userRepository;
    }

    public void SaveUser(User user)
    {
        userRepository.Save(user);
    }
}
```

The `UserService` class now depends on the `IUserRepository` interface instead of the `UserRepository` class. The `UserRepository` class implements the `IUserRepository` interface, and the `UserService` class can use any class that implements the `IUserRepository` interface without modification.

---

## Code Smells

**Code smells** are symptoms of poor design or implementation choices that can lead to maintainability problems. They are not bugs, but they indicate that there may be a problem with the code that needs to be addressed. 

---

### Long Method

**Long Method** is a method that is too long and does too many things. It can be hard to understand and maintain.

```csharp
public void CalculateTotalPrice(List<Product> products)
{
    double totalPrice = 0;

    foreach (Product product in products)
    {
        totalPrice += product.Price;
    }

    if (totalPrice > 100)
    {
        totalPrice *= 0.9;
    }

    Console.WriteLine($"Total price: {totalPrice}");
}
```

This method calculates the total price of a list of products and applies a discount if the total price is greater than 100. It would be better to split the method into smaller, more focused methods.

**Task:** Refactor the code to be more maintainable and easier to understand.

<details> <summary>Click here to see an example answer</summary>

```csharp

public void CalculateTotalPrice(List<Product> products)
{
    double totalPrice = CalculatePrice(products);

    totalPrice = ApplyDiscount(totalPrice);

    DisplayTotalPrice(totalPrice);
}

private double CalculatePrice(List<Product> products)
{
    double totalPrice = 0;

    foreach (Product product in products)
    {
        totalPrice += product.Price;
    }

    return totalPrice;
}

private double ApplyDiscount(double totalPrice)
{
    if (totalPrice > 100)
    {
        totalPrice *= 0.9;
    }

    return totalPrice;
}

private void DisplayTotalPrice(double totalPrice)
{
    Console.WriteLine($"Total price: {totalPrice}");
}
```
</details>

---

### Large Class

**Large Class** is a class that has too many responsibilities and does too many things. It can be hard to understand and maintain.

```csharp
public class Order
{
    private List<Product> products;
    private Customer customer;

    public Order(List<Product> products, Customer customer)
    {
        this.products = products;
        this.customer = customer;
    }

    public void CalculateTotalPrice()
    {
        double totalPrice = 0;

        foreach (Product product in products)
        {
            totalPrice += product.Price;
        }

        if (totalPrice > 100)
        {
            totalPrice *= 0.9;
        }

        Console.WriteLine($"Total price: {totalPrice}");
    }

    public void SendConfirmationEmail()
    {
        // Send a confirmation email to the customer
    }

    public void SaveToDatabase()
    {
        // Save the order to the database
    }
}
```

This class has too many responsibilities: calculating the total price, sending a confirmation email, and saving to the database. It would be better to split the class into smaller, more focused classes.

**Task:** Refactor the code to be more maintainable and easier to understand.

<details> <summary>Click here to see an example answer</summary>

```csharp
public class Order
{
    private List<Product> products;
    private Customer customer;

    public Order(List<Product> products, Customer customer)
    {
        this.products = products;
        this.customer = customer;
    }

    public void CalculateTotalPrice()
    {
        double totalPrice = CalculatePrice();

        totalPrice = ApplyDiscount(totalPrice);

        DisplayTotalPrice(totalPrice);
    }

    private double CalculatePrice()
    {
        double totalPrice = 0;

        foreach (Product product in products)
        {
            totalPrice += product.Price;
        }

        return totalPrice;
    }

    private double ApplyDiscount(double totalPrice)
    {
        if (totalPrice > 100)
        {
            totalPrice *= 0.9;
        }

        return totalPrice;
    }

    private void DisplayTotalPrice(double totalPrice)
    {
        Console.WriteLine($"Total price: {totalPrice}");
    }
}

public class EmailService
{
    public void SendConfirmationEmail(Customer customer)
    {
        // Send a confirmation email to the customer
    }
}

public class OrderRepository
{
    public void SaveToDatabase(Order order)
    {
        // Save the order to the database
    }
}
```

</details>

---

### Switch Statements

**Switch Statements** are a code smell that can indicate that a class is violating the **Open/Closed Principle**. If you find yourself adding new cases to a switch statement every time you add a new type of object, you are violating the **Open/Closed Principle**.

```csharp
public class Shape
{
    private string type;

    public string Type { get => type; set => type = value; }

    public double Area()
    {
        switch (type)
        {
            case "Circle":
                return CalculateCircleArea();
            case "Rectangle":
                return CalculateRectangleArea();
            default:
                throw new Exception("Unknown shape type");
        }
    }

    private double CalculateCircleArea()
    {
        // Calculate the area of a circle
    }

    private double CalculateRectangleArea()
    {
        // Calculate the area of a rectangle
    }
}
```

This class has a switch statement that determines the type of shape and calculates the area accordingly. If you want to add a new shape, you would have to modify the switch statement, which violates the **Open/Closed Principle**.

---

### Comments

**Comments** can be a code smell if they are used to explain what the code is doing instead of why it is doing it. If the code is not self-explanatory, it may be a sign that the code is too complex and needs to be refactored.

```csharp
public void CalculateTotalPrice(List<Product> products)
{
    double totalPrice = 0;

    foreach (Product product in products)
    {
        totalPrice += product.Price;
    }

    // Apply discount if total price is greater than 100
    if (totalPrice > 100)
    {
        totalPrice *= 0.9;
    }

    // Display the total price
    Console.WriteLine($"Total price: {totalPrice}");
}
```

In this example, the comments explain what the code is doing (calculating the total price, applying a discount, and displaying the total price) instead of why it is doing it. The code could be refactored to be more self-explanatory.

---

### Magic Numbers

**Magic Numbers** are hard-coded values in the code that are not self-explanatory. They can be a code smell because they make the code less readable and maintainable.

```csharp
public void CalculateTotalPrice(List<Product> products)
{
    double totalPrice = 0;

    foreach (Product product in products)
    {
        totalPrice += product.Price;
    }

    if (totalPrice > 100)
    {
        totalPrice *= 0.9;
    }

    Console.WriteLine($"Total price: {totalPrice}");
}
```

In this example, the numbers 100 and 0.9 are hard-coded in the code without any explanation of what they represent. It would be better to define constants with meaningful names to make the code more readable.

**Task:** Refactor the code to use constants instead of magic numbers.

<details> <summary>Click here to see an example answer</summary>

```csharp
public class Constants
{
    public const double DISCOUNT_THRESHOLD = 100;
    public const double DISCOUNT_RATE = 0.9;
}

public void CalculateTotalPrice(List<Product> products)
{
    double totalPrice = 0;

    foreach (Product product in products)
    {
        totalPrice += product.Price;
    }

    if (totalPrice > Constants.DISCOUNT_THRESHOLD)
    {
        totalPrice *= Constants.DISCOUNT_RATE;
    }

    Console.WriteLine($"Total price: {totalPrice}");
}
```

</details>

---

## Formative Assessment

If you get stuck on any of the following tasks, feel free to use an AI tool permitting, you are aware of the following:

- If you provide an AI tool with a prompt that is not refined enough, it may generate a not-so-useful response
- Do not trust the AI tool's responses blindly. You must still use your judgement and may need to do additional research to determine if the response is correct
- Acknowledge that you are using an AI tool. In the **README.md** file, please include what prompt(s) you provided to the AI tool and how you used the response(s) to help you with your work

---

### Task 1

In this task, you will use a project from a course you have previously taken. Identity at one example where you have violated the **Single Responsibility Principle** and **Open/Closed Principle**. Describe the violation and how you would refactor the code to adhere to the principle.

Share how you violated the **Single Responsibility Principle** and **Open/Closed Principle** [here](https://github.com/otago-polytechnic-bit-courses/ID737001-game-development/discussions/2)

---

### Task 2

Here is a list of other **code smells**:

- Duplicated Code
- Feature Envy
- Inappropriate Intimacy
- Data Clumps
- Primitive Obsession
- Long Parameter List
- Message Chains

Choose three of the code smells from the list above and describe what they are. 

---

### Submission

Create a new pull request and assign **grayson-orr** to review your submission. Please do not merge your own pull request.

---

## Next Class

Link to the next class: [Week 02]()
