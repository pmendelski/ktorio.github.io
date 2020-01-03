---
title: Jtwig
caption: Using Jtwig Templates
category: servers
keywords: html
feature:
  artifact: io.ktor:ktor-jtwig:$ktor_version
  class: io.ktor.jtwig.Jtwig
redirect_from:
- /features/jtwig.html
- /features/templates/jtwig.html
ktor_version_review: 1.0.0
---

Ktor includes support for [Jtwig](http://jtwig.org/) templates through the Jtwig
feature.  Initialize the Jtwig feature with an optional configuration:

```kotlin
    install(Jtwig) {
        templatePrefix = "classpath:templates/"
        templateSuffix = ".twig.html"
    }
```

This configuration sets up Jtwig to look for the template files on the classpath in the
"templates" package, relative to the current class path.  A basic template looks like this:

{% include feature.html %}

```html
<html>
<h2>Hello {{user.name}}!</h2>

Your email address is {{user.email}}
</html>
```

With that template in `resources/templates/index.twig.html` it is accessible elsewhere in the the application
using the `call.respond()` method:

```kotlin
    get("/{...}") {
        val user = User("user name", "user@example.com")
        call.respond(JtwigContent("index", mapOf("user" to user), "e"))
    }
```
