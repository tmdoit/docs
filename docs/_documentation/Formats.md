---
slug: formats
title: Content Types
---

ServiceStack supports the following formats:

- [JSON](https://github.com/ServiceStack/ServiceStack.Text)
- XML
- [SOAP 1.1/1.2](/soap-support)
- [JSV](/jsv-format) _(hybrid CSV-style escaping + JSON format that is optimized for both size and speed)_
- [CSV](/csv-format)
- HTML
    - [Templates](http://templates.servicestack.net) _(Simple, clean, fast alternative to Razor)_
    - [Razor](http://razor.servicestack.net) _(Microsoft's Razor View Engine)_
    - [Markdown Razor](/markdown-razor) _(Razor-inspired syntax combined with markdown)_
    - [HTML5 Report](/html5reportformat) _(Human-friendly HTML auto-layout to quickly visualize data returned by services)_
- [Message Pack](/messagepack-format)
- [Protocol Buffers](/protobuf-format)
- [Wire](/wire-format)

### .NET Service Clients

The different Content Types can be easily consumed using [ServiceStack's Typed Generic Service Clients](/csharp-client#httpwebrequest-service-clients).

## HTTP/REST Endpoints

You can define which format should be used by adding a `.{format}` extension:

 - `.json`
 - `.xml`
 - `.jsv`
 - `.csv`
 - `.html`

Or by appending `?format={format}` to the end of the URL:

- `?format=json`
- `?format=xml`
- `?format=jsv`
- `?format=csv`
- `?format=html`

> Example: http://test.servicestack.net/hello/World!?format=json

Alternatively ServiceStack also recognizes which format should be used with the `Accept` [http header](http://en.wikipedia.org/wiki/List_of_HTTP_header_fields):

- `Accept: application/json`
- `Accept: application/xml`

As you can see, this approach only works with `json` and `xml`.

## Pre-defined Routes

    /[xml|json|html|jsv|csv]/[reply|oneway]/[servicename]

Examples:

 - /json/reply/Hello (JSON)
 - /xml/oneway/SendEmail (XML)

### Forcing a Content Type

Whilst ServiceStack Services are typically available on any endpoint and format, there are times when you only want adhoc Services available in a particular format, for instance you may only want the View Models for your dynamic Web Views available in HTML. This can now be easily enabled with the new `[HtmlOnly]` Request Filter Attribute, e.g:
    
```cshtml
[HtmlOnly]
public class HtmlServices : Service
{
    public object Any(MyRequest request) => new MyViewModel { .. };
}
```

This feature is also available for other built-in Content Types: `[JsonOnly]`, `[XmlOnly]`, `[JsvOnly]` and `[CsvOnly]`.

## [SOAP Endpoint](/soap-support)

Consume ServiceStack Services via [SOAP](/soap-support) using WCF Add Service Reference or [ServiceStack generic SOAP Clients](/csharp-client#httpwebrequest-service-clients).

## [MQ Endpoint](/messaging)

Consume ServiceStack Services via [Message Queue](/messaging).
