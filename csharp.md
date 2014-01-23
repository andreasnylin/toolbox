C#
===

## Validate e-mail address

```cs
public static bool ValidateEmailAddress(string email)
{
    try
    {
        MailAddress m = new MailAddress(email);
        return true;
    }
    catch (FormatException)
    {
        return false;
    }
}
```

## Get string value of enum

```cs
Enum.GetName(typeof(MyEnumType), MyEnumType.SomeValue);
```

## Get int value of enum

```cs
var blue = Colors.Blue;
var blueInt = (int)blue;
```

## Parse an enum

```cs
(MyEnum)Enum.Parse(typeof(MyEnum), myEnum.Value.ToString())
```

## Get all values for a enum

```cs
Enum.GetValues(typeof(MyEnum))
```

## Check if debug is enabled

```cs
HttpContext.Current.IsDebuggingEnabled

#if DEBUG

#else

#endif
```

## Get culture name

```cs
System.Threading.Thread.CurrentThread.CurrentCulture.Name // => "en-US"
System.Threading.Thread.CurrentThread.CurrentCulture.TwoLetterISOLanguageName // => "en"
```

## Get querystring parameters from a URL
```cs
var query = HttpUtility.ParseQueryString(someUri.Query)
```

## Create a query string from NameValueCollection
```cs
private string BuildQueryString(NameValueCollection nvc)
{
    var array = (from key in nvc.AllKeys
                 from value in nvc.GetValues(key)
                 select string.Format("{0}={1}", HttpUtility.UrlEncode(key), HttpUtility.UrlEncode(value)))
        .ToArray();
    return "?" + string.Join("&", array);
}
```

