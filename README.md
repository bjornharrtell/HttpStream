HttpStream
==========
This C# project implements randomly accessible stream on HTTP 1.1 transport.
Typically, HttpClient provides almost all HTTP features but it just provides us with a way to download a file completely.
The implementation take advantage of HTTP 1.1 range access or on fallback case, it uses HTTP/1.0 sequential download anyway.

## NuGet Package
A prebuilt NuGet package is available: [Espresso3389.HttpStream](https://www.nuget.org/packages/Espresso3389.HttpStream/).

To install espresso3389.HttpStream, run the following command in the Package Manager Console:
```
PM> Install-Package Espresso3389.HttpStream
```

## Supported Platforms
This module is built against .NET Platform Standard 1.1 (`netstandard1.1`) and it's compatible with the following platforms:

- .NET Core 1.0
- .NET Framework 4.5
- Universal Windows Platform 10.0
- Windows 8.0
- Windows Phone 8.1
- Mono/Xamarin Platforms

For more information, see the illustration on [Mapping the .NET Platform Standard to platforms - .NET Platform Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md#mapping-the-net-platform-standard-to-platforms).

### Simple Usage
```cs
// cache stream
var fs = File.Create("cache.jpg");

// The third parameter, true indicates that the httpStream will close the cache stream.
var uri = new Uri(@"https://dl.dropboxusercontent.com/u/150906/2007-01-28%2006.04.05.JPG");
var httpStream = new Espresso3389.HttpStream.HttpStream(uri, fs, true);

// RangeDownloaded is called on every incremental download
httpStream.RangeDownloaded += (sender, e) =>
{
  Console.WriteLine("Progress: {0}%", (int)(100 * httpStream.CachedRatio));
};

// The following code actually invokes download whole the file
var bmp = await BitmapFactory.DecodeStreamAsync(httpStream);
```

## License
The codes/binaries are licensed under [MIT License](https://github.com/espresso3389/HttpStream/blob/master/LICENSE).
