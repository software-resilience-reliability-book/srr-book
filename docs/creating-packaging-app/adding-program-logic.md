# Adding the Program Logic

## Updating `WordReplacer.cs`

Copy and paste the following code into the `WordReplacer.cs` file:

```csharp
using Bogus;

namespace WordSub;

public class WordReplacer
{
    private readonly Faker _faker = new Faker();

    public string Replace(string text)
    {
        return text
            .Replace("[adjective]", _faker.Commerce.ProductAdjective().ToLower())
            .Replace("[noun]", _faker.Commerce.Product().ToLower())
            .Replace("[verb]", _faker.Hacker.Verb().ToLower());
    }
}
```

Run the program again a few times and you should see the random words being replaced in the output. It's not perfect, but it's good enough for this demo.

## Updating `Program.cs`

The last step is to get input from the user and replace the words in the input text. Modify the `Program.cs` file to look like the following:

```csharp
using WordSub;

var replacer = new WordReplacer();

Console.Write("Enter a sentence: ");
string input = Console.ReadLine();

string output = replacer.Replace(input);
Console.WriteLine(output);
```

We now have our full program. After running it you can enter console input such as: "The [adjective] [noun] [verb]!" and you will see the words replaced with random words.
