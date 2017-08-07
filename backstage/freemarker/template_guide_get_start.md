## getting started

### 1. template + data-model = output

To recapitulate,a template and a data-model is needed for FreeMarker to generate the output(like the HTML).


### 2. the data-model at a glance(一瞥)

As you have seen, the data-model is basically a tree.This tree can be  arbitrarily complicated and deep. for example:

```bash

    (root)
    |
    +- animals
    |   |
    |   +- mouse
    |   |   |
    |   |   +- size = "small"
    |   |   |
    |   |   +- price = 50
    |   |
    |   +- elephant
    |   |   |
    |   |   +- size = "large"
    |   |   |
    |   |   +- price = 5000
    |   |
    |   +- python
    |       |
    |       +- size = "medium"
    |       |
    |       +- price = 4999
    |
    +- message = "It is a test"
    |
    +- misc
        |
        +- foo = "Something"

```


### 3. The template at a glance

**1.)the if directive**

```html

    <html>
        ...
        <h1>welcome ${user}<#if user == "big joe"}>, our beloved leader</#if></h1>
        ...
    </html>

```

Here you have rold FreeMarker that the ", our beloved leader" should be there only if the value of the variable user is equalto the string "big joe".In general, things between <#if condition>and </#if>tags are skipped if condition is false(the boolean value).

With the <#else>tag you can specify what to do if the condition is false.For example:

```html

    <#if animals.python.price < animals.elephant.price >
        Pythons are cheaper than elephants today.
    <#else>
        Pythons are not cheaper than elephants today.
    </#if>

```

you can refine this further by using `elseif`:

```html

    <#if animals.python.price < animals.elephant.price >
        Pythons are cheaper than Elephants today.
    <#elseif animals.elephant.price < animals.python.price >
        Elephants are cheaper than Pythons today.
    <#else>
        Elephants and Python cost the same today.
    </#if>

```

**2.)the list directive**

This is needed when you want to list something. For example if you merge this template withe `data-model used earlier to demonstrate sequences`:

```html

    <!--template-->
    <p>We have these animals:</p>
    <table border=1>
        <#list animals as animal>
            <tr><td>${animal.name}</td><td><td>${animal.price}</td></tr>
        </#list>
    </table>

```

then the output will be:

```html

    <p>We have these animals:
    <table border=1>
        <tr><td>mouse<td>50 Euros
        <tr><td>elephant<td>5000 Euros
        <tr><td>python<td>4999 Euros
    </table>

```

Another example:

```html

    <ul>
    <#list misc.fruits as fruit>
    <li>${fruit}
    </#list>
    </ul>

```

A problem with the above example is that if we happen to have `0` fruits, it wil still print an empty `<ul></ul>` instead of just nothing. To avoid that, you can use this form of `list`:

```html

<!--template-->
    <#list misc.fruits>
    <ul>
        <#items as fruit>
        <li>${fruit}
        </#items>
    </ul>
    </#list>

```

Here, the `list` directive represent the listing as a whole, and only the part inside the `items` directive is repeated for each fruit.If we have 0 fruit, everything inside `list` is skipped, hence(因此) we will not have `ul` tags in case.

Another frequent listing-related task:let's list the fruits separating them with something,like a comma(逗号):

```html

    <!--template-->
    <p>Fruits: <#list misc.fruits as fruit>${fruit}<#sep>, </#list>

```

```html

    <!--output-->
    <p>Fruits: orange, banana

```

The section covered by `sep`(which we could be written like this too:`...<#sep>,</#sep></#list>)`will be only excuted when there will be a next item.Hence there's no comma after the last fruit.

All these directive `(list,items,sep,else)`can be used together:

```html

    <#list misc.fruits>
    <p>Fruits:
    <ul>
        <#items as fruit>
        <li>${fruit}<#sep> and</#sep>
        </#items>
    </ul>
    <#else>
    <p>We have no fruits.
    </#list>

```


**3.)the include directive**

With the `include` directive you can insert the content of another file into the template.

Here a file named `copyright_footer.html`:

```html

    <hr>
    <i>
    Copyright (c) 2000 <a href="http://www.acmee.com">Acmee Inc</a>,
    <br>
    All Rights Reserved.
    </i>

```

Whenever you need thatfile you simply insert it with the `include` directive:

```html

    <html>
    <head>
    <title>Test page</title>
    </head>
    <body>
    <h1>Test page</h1>
    <p>Blah blah...
    <#include "/copyright_footer.html">
    </body>
    </html>

```

and the output file will be:

```html

    <html>
    <head>
    <title>Test page</title>
    </head>
    <body>
    <h1>Test page</h1>
    <p>Blah blah...
    <hr>
    <i>
    Copyright (c) 2000 <a href="http://www.acmee.com">Acmee Inc</a>,
    <br>
    All Rights Reserved.
    </i>
    </body>
    </html>

```

If you change the `copyright_footer.html`,then the visitor will see the new copyright notice on all pages.
