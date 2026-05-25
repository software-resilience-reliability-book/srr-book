# Establishing the API

## Creating the `WordReplacer` Class

The next step is to formalize the functionality of the application by establishing its API. The informal requirements for the application are as follows:

> The application must accept as input a sentence containing token placeholders for parts of speech, and output a new sentence with the tokens replaced with randomized words corresponding to the part of speech.

An example run might look like this:

```
Enter a sentence: The [adjective] [noun] [verb].
The slow chicken dances.
```

We can manage this with one class containing a single public method: `WordReplacer.Replace`.

Let's create the new class for this functionality. Be sure to put this class in the `WordSub.App` directory.

```csharp
public class WordReplacer
{
    public string Replace(string text)
    {
        throw new NotImplementedException();
    }
}
```

As a placeholder, we will throw a `NotImplementedException`, so that anyone trying to call this method while it is under development will be met with a clear error message.

## Calling the New Class

Now we can call this method from the `Program.cs` file:

```csharp
var wordReplacer = new WordReplacer();
var result = wordReplacer.Replace("The [adjective] [noun] [verb].");
Console.WriteLine(result);
```

The file structure should now look like this:

```text
word-sub/
└── WordSub.App
    ├── Program.cs
    ├── WordReplacer.cs
    └── WordSub.App.csproj
```

If you run the program now you will see the NotImplementedException error.

Success! We have a starter shell in place for the application. Just creating a minimal working program is the first milestone in building the solution.

<!-- prettier-ignore -->
!!! warning "Garbage In, Garbage Out"
    The requirements that we have provided are very lax. In reality we would want to define behavior in more detail. For example: What tense should be used? What do we do if we hit a token placeholder without a valid identifier? Should we allow duplicate replacement words?

    Without proper requirements, we don't know if we have met acceptance criteria and cannot properly confirm that the system works through testing.
