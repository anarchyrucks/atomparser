# atomparser

A Dart library for parsing Atom feeds.

Inspired by [xqwzts/feedparser](https://github.com/xqwzts/feedparser).

## Usage

```dart
import 'package:atomparser/atomparser.dart';

void main() {
  AtomFeed feed = parse(r'''
    <?xml version="1.0" encoding="utf-8"?>
    <feed xmlns="http://www.w3.org/2005/Atom">

      <title>Example Feed</title>
      <link href="http://example.org/"/>
      <updated>2003-12-13T18:30:02Z</updated>
      <author>
        <name>John Doe</name>
      </author>
      <id>urn:uuid:60a76c80-d399-11d9-b93C-0003939e0af6</id>

      <entry>
        <title>Atom-Powered Robots Run Amok</title>
        <link href="http://example.org/2003/12/13/atom03"/>
        <id>urn:uuid:1225c695-cfb8-4ebb-aaaa-80da344efa6a</id>
        <updated>2003-12-13T18:30:02Z</updated>
        <summary>Some text.</summary>
      </entry>

    </feed>
  ''');

  print(feed);

  // Output:
  //      id: urn:uuid:60a76c80-d399-11d9-b93C-0003939e0af6
  //      title: Example Feed
  //      updated: 2003-12-13T18:30:02Z
  //      authors: [
  //        name: John Doe
  //        uri: null
  //        email: null
  //      ]
  //      links: [
  //        href: http://example.org/
  //        rel: null
  //        type: null
  //        hreflang: null
  //        title: null
  //        length: null
  //      ]
  //      category: null
  //      icon: null
  //      logo: null
  //      rights: null
  //      subtitle: null
  //      entries: [
  //        id: urn:uuid:1225c695-cfb8-4ebb-aaaa-80da344efa6a
  //        title:  text: Atom-Powered Robots Run Amok
  //                type: null
  //        updated: 2003-12-13T18:30:02Z
  //        author: null
  //        content: null
  //          link: href: http://example.org/2003/12/13/atom03
  //            rel: null
  //            type: null
  //            hreflang: null
  //          title: null
  //          length: null
  //          summary: text: Some text.
  //                   type: null
  //        category: null
  //        published: null
  //        rights: null
  //      ]
}
```

## Strict mode

As long as the input string provided is a valid XML string, atomparser will attempt to parse it and return a AtomFeed object. In strict mode atomparser instead throws ArgumentErrors for missing mandatory fields [as defined by the [Atom ](https://validator.w3.org/feed/docs/atom.html) spec]. This is useful for testing feeds to ensure they meet the spec, but impractical when dealing with feeds not under your control.

```dart
AtomFeed feed = parse(xmlString, strict: true);
```