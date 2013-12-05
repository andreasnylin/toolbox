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

## Check if debug is enabled

```cs
HttpContext.Current.IsDebuggingEnabled

#if DEBUG

#else

#endif
```
