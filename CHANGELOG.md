Change Log
==========

## Version 1.1.0

_2016-01-19_

 * New: Support [RFC 7159][rfc_7159], the latest JSON specification. This removes the constraint
   that the root value must be an array or an object. It may now take any value: array, object,
   string, number, boolean, or null. Previously this was only permitted if the adapter was
   configured to be lenient.
 * New: Enum constants may be annotated with `@Json` to customize their encoded value.
 * New: Create new builder from Moshi instance with `Moshi.newBuilder()`.
 * New: `Types.getRawType()` and `Types.collectionElementType()` APIs to assist in defining generic
   type adapter factories.

## Version 1.0.0

_2015-09-27_

 * **API Change**: Replaced `new JsonReader()` with `JsonReader.of()` and `new JsonWriter()` with
   `JsonWriter.of()`. If your code calls either of these constructors it will need to be updated to
   call the static factory method instead.
 * **API Change**: Don’t throw `IOException` on `JsonAdapter.toJson(T)`. Code that calls this method
   may need to be fixed to no longer catch an impossible `IOException`.
 * Fix: the JSON adapter for `Object` no longer fails when encountering `null` in the stream.
 * New: `@Json` annotation can customize a field's name. This is particularly handy for fields whose
   names are Java keywords, like `default` or `public`.
 * New: `Rfc3339DateJsonAdapter` converts between a `java.util.Date` and a string formatted with
   RFC 3339 (like `2015-09-26T18:23:50.250Z`). This class is in the new `moshi-adapters` subproject.
   You will need to register this adapter if you want this date formatting behavior. See it in
   action in the [dates example][dates_example].
 * New: `Moshi.adapter()` keeps a cache of all created adapters. For best efficiency, application
   code should keep a reference to required adapters in a field.
 * New: The `Types` factory class makes it possible to compose types like `List<Card>` or
   `Map<String, Integer>`. This is useful to look up JSON adapters for parameterized types.
 * New: `JsonAdapter.failOnUnknown()` returns a new JSON adapter that throws if an unknonw value is
   encountered on the stream. Use this in development and debug builds to detect typos in field
   names. This feature shouldn’t be used in production because it makes migrations very difficult.

## Version 0.9.0

_2015-06-16_

 * Databinding for primitive types, strings, enums, arrays, collections, and maps.
 * Databinding for plain old Java objects.
 * [JSONPath](http://goessner.net/articles/JsonPath/) support for both `JsonReader` and
   `JsonWriter`.
 * Throw `JsonDataException` when there’s a data binding problem.
 * Adapter methods: `@ToJson` and `@FromJson`.
 * Qualifier annotations: `@JsonQualifier` to permit different type adapters for the same Java type.
 * Imported code from Gson: `JsonReader`, `JsonWriter`. Also some internal classes:
   `LinkedHashTreeMap` for hash-collision avoidance and `Types` for typesafe databinding.


 [dates_example]: https://github.com/square/moshi/blob/master/examples/src/main/java/com/squareup/moshi/recipes/ReadAndWriteRfc3339Dates.java
 [rfc_7159]: https://tools.ietf.org/html/rfc7159
