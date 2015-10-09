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

## Get file extension form URL

```cs
public static string GetUrlExtension(string url, bool includePeriod = true)
{
	if (url.IndexOf("?") != -1)
	{
		url = url.Substring(0, url.IndexOf("?"));
	}

	if (url.IndexOf("#") != -1)
	{
		url = url.Substring(0, url.IndexOf("#"));
	}

	var ext = Path.GetExtension(url);

	if (includePeriod)
	{
		return ext;
	}
	else
	{
		return ext.Substring(1);
	}
}
```

## Get querystring parameters from a URL
```cs
var query = HttpUtility.ParseQueryString(someUri.Query);
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

## Get the domain including protocol and port for the current page
```cs
HttpContext.Current.Request.Url.GetLeftPart(UriPartial.Authority);
```

## LINQ Split list into columns
```cs
// Credit: http://stackoverflow.com/a/13502615
public static class Extensions
{
    public static IEnumerable<IEnumerable<T>> Split<T>(this IEnumerable<T> source, int parts)
    {
        var list = new List<T>(source);
        int defaultSize = (int)((double)list.Count / (double)parts);
        int offset = list.Count % parts;
        int position = 0;

        for (int i = 0; i < parts; i++)
        {
            int size = defaultSize;
            if (i < offset)
                size++; // Just add one to the size (it's enough).

            yield return list.GetRange(position, size);

            // Set the new position after creating a part list, so that it always start with position zero on the first yield return above.
            position += size;
        }
    }
}

int[] b = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
b.split(4);

/*
| item 1 | item 4 | item 7 | item 9 |
| item 2 | item 5 | item 8 | item 10|
| item 3 | item 6 |        |        |
*/

```

## Get a list of years from x to current year
```cs
var startYear = 2000;
Enumerable.Range(startYear, DateTime.Now.Year - startYear + 1).Reverse();
```

## Check that a string does not contain certain characters
```cs
Regex rx = new Regex("^((?![aoueiy]).)*$");
Console.WriteLine(rx.IsMatch("abc")); // => False
Console.WriteLine(rx.IsMatch("def")); // => False
Console.WriteLine(rx.IsMatch("jkl")); // => True
```

## String helper
```cs
public static class StringHelper
{
	public static string FirstNotNullOrWhiteSpace(params string[] values)
	{
		return values.FirstOrDefault(value => !string.IsNullOrWhiteSpace(value));
	}
	
	public static string Shorten(string text, int maxLength, string suffix = null)
	{
		if(string.IsNullOrWhiteSpace(text) || text.Length <= maxLength)
			return text;
			
		var length = suffix != null ? maxLength - suffix.Length : maxLength;
		
		if(suffix != null)
		{
			return text.Substring(0, length) + suffix;
		}
		else
		{
			return text.Substring(0, length);
		}
	}
}
```
## Format bytes
```cs
public string FormatBytes(long bytes)
{
	const int scale = 1024;
	var orders = new[] { "GB", "MB", "kB", "Bytes" };
	var max = (long)Math.Pow(scale, orders.Length - 1);
	foreach (var order in orders)
	{
		if (bytes > max)
			return string.Format("{0:##.##} {1}", Decimal.Divide(bytes, max), order);
		max /= scale;
	}
	return "0 Bytes";
}
```

## CSS Class Helper
```cs
public class CssClassList
{

	private readonly HashSet<string> _classes;

	public CssClassList()
	{
		_classes = new HashSet<string>();
	}

	public CssClassList(string cssClass)
	{
		_classes = new HashSet<string>();

		Add(cssClass);
	}

	public void AddIf(bool condition, string truthyCssClass, string falsyCssClass = null)
	{
		if (condition)
		{
			Add(truthyCssClass);
		}
		else if (falsyCssClass != null)
		{
			Add(falsyCssClass);
		}
	}

	public void Add(string cssClass)
	{
		if (cssClass.Contains(" "))
		{
			foreach (var cssClassPart in cssClass.Split(' '))
			{
				Add(cssClassPart);
			}
		}
		else
		{
			_classes.Add(cssClass);
		}
	}

	public void Add(IEnumerable<string> classes)
	{
		foreach (var cssClass in classes)
		{
			_classes.Add(cssClass);
		}
	}

	public bool HasClass(string cssClass)
	{
		return _classes.Contains(cssClass);
	}

	public void Remove(string cssClass)
	{
		_classes.Remove(cssClass);
	}

	public void Remove(IEnumerable<string> classes)
	{
		foreach (var cssClass in classes)
		{
			_classes.Remove(cssClass);
		}
	}

	public string RenderList()
	{
		return !_classes.Any() ? null : string.Join(" ", _classes);
	}

	public string RenderClassAttribute(bool renderIfEmpty = false)
	{
		if (!renderIfEmpty && !_classes.Any())
			return null;

		return string.Format("class=\"{0}\"", RenderList());
	}
}

// Usage

var cssClasses = new CssClassList();

cssClasses.Add("apple");
cssClasses.Add("pear banana");
cssClasses.Add(new List<string>() { "peach", "plum" });
cssClasses.Remove("banana");
cssClasses.Remove(new List<string>() { "peach", "plum" });
cssClasses.AddIf(true, "kiwi");
cssClasses.AddIf(true, "lemon", "lime");
cssClasses.HasClass("lemon");
cssClasses.RenderList();
// result => "apple pear lemon kiwi"
cssClasses.RenderClassAttribute();
// result => class="apple pear lemon kiwi"

```
