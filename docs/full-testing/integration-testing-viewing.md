# Viewing the Test Code

For this example we will look at the `tests/ColorTransform.Tests/Integration/IndexPageTests.cs` file. This file contains a single integration test for the `Index` page of the web application.

There's a lot of code to unpack here, so let's break it down step by step. Only a snippet is shown here, but you can access the rest of the full version [here](https://github.com/software-resilience-reliability-book/color-transform/blob/main/tests/ColorTransform.Tests/Integration/IndexPageTests.cs) :

```csharp
[Fact]
public async Task post_with_invert_returns_transformed_color_string_in_returned_html()
{
    // The "_client" object is an HttpClient that can be used to send HTTP requests to the test server.
    // Here we get the initial "index" page from the in-memory test server.
    var getResponse = await _client.GetAsync("/");

    // Get the HTML response body as a string.
    var html = await getResponse.Content.ReadAsStringAsync();

    // The form submission needs a token to prevent CSRF attacks, so we parse it from the HTML.
    var token = ParseAntiforgeryToken(html);

    // Here we assemble the form variables for submission.
    var form = new Dictionary<string, string>
    {
        ["TransformType"] = "invert",
        ["InputColor"] = "#336699",
        ["__RequestVerificationToken"] = token,
    };

    // The "PostAsync" method sends the form variables to the server.
    // This is what the browser would do, but we're doing it programmatically.
    var postResponse = await _client.PostAsync("/", new FormUrlEncodedContent(form));

    // Get the HTML response body as a string.
    var resultHtml = await postResponse.Content.ReadAsStringAsync();

    // Finally, assert that the result HTML string contains the transformed color.
    Assert.Contains("#CC9966", resultHtml, StringComparison.OrdinalIgnoreCase);
}
```

Take a moment to read through the code comments before moving on to the next section.

The test code starts up a web server in-memory on your local machine, and runs the web application inside of it. We can use this in-memory server to make "fake" HTTP requests to the web application and confirm results that are returned. This simulates what is happening when the live web server is running and the user actually submits the main form.

<!-- prettier-ignore -->
!!! info "Review of Web Forms"
    If you have not studied web forms in depth, that's okay. When you submit a web form, the `Input` HTML elements, which correspond to the form fields, are collected and sent to the web server. It then uses those values to do work on the back end and form a correct response.

    In our case, the Index page needs to know the input color, which transform we want from the dropdown, and an extra value that's hidden from view in the HTML form that is used to prevent CSRF attacks. If you look at the rendered page HTML after runnin the web application, you will see all of these values in the form as `Input` elements, including the hidden CSRF token:

    ```html
    <input name="__RequestVerificationToken" type="hidden" value="CfDJ8P-E2Z-Pg0RLrYr5PDlKEihSM_3W1BTSVKIcAD3CI08x3RsiXORxaYAKP1TnqcOEsHFnTXpwVPhqWUyoVm6sulyGtPDIZeRHBPQFzDAWxs7zEzj8vfUhqW1YROULIC6NiTePMIeAq9gx7WDVXEB26IQ" />
    ```
