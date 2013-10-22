# C#

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
