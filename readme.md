#Useful classes

This is a small repository where I will upload pieces of code useful for me and my daily work.

##BasicAuthentication.cs

Class made with C# and useful for a MVC .NET C# Project. Use it when you need Basic Authentication in your application. 

HTTP Basic authentication (BA) implementation is the simplest technique for enforcing access controls to web resources because it doesn't require cookies, session identifiers, or login pages; rather, HTTP Basic authentication uses standard fields in the HTTP header, obviating the need for handshakes. [+info](https://en.wikipedia.org/wiki/Basic_access_authentication)

###How to use it? 

- Import the class into your project 
- Add these lines on your Web.config:

```xml
  <appSettings>    
    <add key="api_username" value="your-username"/>
    <add key="api_password" value="your-password"/>
    ...    
  </appSettings>
```

- Add [BasicAuthenticationAttribute] before your function.

```c#
[BasicAuthenticationAttribute]
[HttpGet]
public JsonResult Ping()
{
    return Json(new { IsSuccess = true }, JsonRequestBehavior.AllowGet);
}
```

##Email.cs

Class made with C# and useful for a MVC .NET C# Project. Use it when you need to send simple emails and you have your own SMTP server

You will also need the Log.cs class to use this class!

###How to use it? 

- Import the class into your project 
- Add these lines on your Web.config:

```xml
  <appSettings>    
    <add key="email_from" value="your@email.com"/>
    <add key="email_name" value="YOUR-NAME"/>
    <add key="smtp_host" value="smtp.host.com"/>
    <add key="smtp_user" value="user@host.com"/>
    <add key="smtp_password" value="your-password"/>
    ...    
  </appSettings>
```

- Use it like this:

```c#
Email.SimpleEmail("FATAL ERROR", "Kill all humans", "your@email.com");
```

##Log.cs

Class made with C# and useful for a MVC .NET C# Project. Use it when you need to store in a txt LOG simple messages.

###How to use it? 

- Import the class into your project 
- Use it like this:

```c#
try
{
    //STUFF
}
catch (Exception ex)
{
    Log.SimpleLog(ex.Message.ToString());
}
```

##ReCaptchaClass.cs

Class made with C# and useful for a MVC .NET C# Project. Use it when you need to use Google Recaptcha in your application. 

[+info Recaptcha](https://www.google.com/recaptcha/intro/index.html)

###How to use it? 

- Import the class into your project 
- Add these lines on your Web.config:

```xml
  <appSettings>    
    <add key="recaptcha_privatekey" value="your-privatekey"/>
    <add key="recaptcha_publickey" value="your-publickey"/>
    ...    
  </appSettings>
```

- Add these lines on your Controller function

```c#
[HttpPost]
public ActionResult Dummy(FormCollection form)
    string EncodedResponse = Request.Form["g-Recaptcha-Response"];
    bool IsCaptchaValid = (ReCaptchaClass.Validate(EncodedResponse) == "True" ? true : false);

    if (IsCaptchaValid)
    {
        //Recaptcha is valid
    }
}
```

- Add these line in your view

```html
<script src='https://www.google.com/recaptcha/api.js'></script>
<div class="g-recaptcha" data-sitekey="@System.Web.Configuration.WebConfigurationManager.AppSettings['recaptcha_publickey']"></div>
```
##Validator.cs

Class made with C# and useful for a MVC .NET C# Project. Use it when you need to create a string from a DbEntityValidationException.

###How to use it? 

- Import the class into your project 
- Use it like this:

```c#
try
{
    //STUFF
}
catch (DbEntityValidationException e)
{
    return Validator.ToString(e);
}
```
##CleanStrings.cs

Class made with C# and useful for a MVC .NET C# Project. Use it when you need to remove diacritics from a string or you need to create a string as a friendly url from any string.

###How to use it? 

- Import the class into your project 
- Use it like this:

```c#
//Friendly url
var friendly = CleanStrings.friendlyURL(new.title)
var nodiac = CleanStrings.RemoveAccent(new.title)
```

## Licenses

Distributed under the [MIT](http://en.wikipedia.org/wiki/MIT_License)

###MIT - Licence

Copyright (c) 2017 Eric Risco de la Torre

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.