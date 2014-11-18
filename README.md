java-util
=========
Rarely available and hard-to-write Java utilities, written correctly, and thoroughly tested

To include in your project:
```
<dependency>
  <groupId>com.cedarsoftware</groupId>
  <artifactId>java-util</artifactId>
  <version>1.13.0</version>
</dependency>
```
<a class="coinbase-button" data-code="95fd9e409d5eb4160314a7c6030be682" data-button-style="custom_large" data-custom="java-util" href="https://coinbase.com/checkouts/95fd9e409d5eb4160314a7c6030be682">Feed hungry developers...</a><script src="https://coinbase.com/assets/button.js" type="text/javascript"></script>

Also, check out json-io at https://github.com/jdereg/json-io

Including in java-util:
* **ArrayUtilities** - Useful utilities for working with Java's arrays [ ]
* **ByteUtilities** - Useful routines for converting byte[] to HEX character [] and visa-versa.
* **CaseInsensitiveMap** - When Strings are used as keys, they are compared without case. Can be used as regular Map with any Java object as keys, just specially handles Strings.
* **CaseInsensitiveSet** - Set implementation that ignores String case for contains() calls, yet can have any object added to it (does not limit you to adding only Strings to it).
* **DateUtilities** - Robust date String parser that handles date/time, date, time, time/date, string name months or numeric months, skips comma, etc. English month names only (plus common month name abbreviations), time with/without seconds or milliseconds, y/m/d and m/d/y ordering as well.
* **DeepEquals** - Compare two object graphs and return 'true' if they are equivalent, 'false' otherwise.  This will handle cycles in the graph, and will call an equals() method on an object if it has one, otherwise it will do a field-by-field equivalency check for non-transient fields.
* **EncryptionUtilities** - Makes it easy to compute MD5 checksums for Strings, byte[], as well as making it easy to AES-128 encrypt Strings and byte[]'s.
* **IOUtilities** - Handy methods for simplifying I/O including such niceties as properly setting up the input stream for HttpUrlConnections based on their specified encoding.  Single line .close() method that handles exceptions for you.
* **MathUtilities** - Handy mathematical alrogithms to make your code smaller.  For example, minimum of array of values.
* **ReflectionUtils** - Simple one-liners for many common reflection tasks.
* **SafeSimpleDateFormat** - Instances of this class can be stored as member variables and reused without any worry about thread safety.  Fixing the problems with the JDK's SimpleDateFormat and thread safety (no reentrancy support).
* **StringUtilities** - Helpful methods that make simple work of common String related tasks.
* **SystemUtilities** - A Helpful utility methods for working with external entities like the OS, environment variables, and system properties.
* **Traverser** - Pass any Java object to this Utility class, it will call your passed in anonymous method for each object it encounters while traversing the complete graph.  It handles cycles within the graph. Permits you to perform generalized actions on all objects within an object graph.
* **UniqueIdGenerator** - Generates a Java long unique id, that is unique across server in a cluster, never hands out the same value, has massive entropy, and runs very quickly.
* **UrlUtitilies** - Fetch cookies from headers, getUrlConnections(), HTTP Response error handler, and more.
* **UrlInvocationHandler** - Use to easily communicate with RESTful JSON servers, especially ones that implement a Java interface that you have access to.

Version History
* 1.13.0
 * DateUtilities - Strengthened date parsing
  * Day of week allowed (properly ignored).
  * First (st), second (nd), third (rd), and fourth (th) ... supported.
  * The default toString() standard date / time displayed by the JVM is now supported as a parseable format.
  * Extra whitespace can exist within the date string.
  * Full time zone support added.
  * The date (or date time) is expected to be in isolation. Whitespace on either end is fine, however, once the date time is parsed from the string, no other content can be left (prevents accidently parsing dates from dates embedded in text).
 * Removed proxy from calls to URLUtilities.  These are now done through the JVM.
* 1.12.0
 * `UniqueIdGenerator` uses 99 as the cluster id when the JAVA_UTIL_CLUSTERID environment variable or System property is not available.  This speeds up execution on developer's environments when they do not specify JAVA_UTIL_CLUSTERID.
 * All the 1.11.x features rolled up.
* 1.11.3
 * UrlUtilities - separated out call that resolves res:// to a public API to allow for wider use.
* 1.11.2
 * Updated so headers can be set individually by the strategy (UrlInvocationHandler)
 * InvocationHandler set to always uses POST method to allow additional HTTP headers.
* 1.11.1
 * Better IPv6 support (UniqueIdGenerator)
 * Fixed UrlUtilities.getContentFromUrl() (byte[]) no longer setting up SSLFactory when http protocol used.
* 1.11.0
 * `UrlInvocationHandler`, `UrlInvocationStrategy` - Updated to allow more generalized usage. Pass in your implementation of `UrlInvocationStrategy` which allows you to set the number of retry attempts, fill out the URL pattern, set up the POST data, and optionally set/get cookies.
 * Removed dependency on json-io.  Only remaining dependency is Apache commons-logging.
* 1.10.0
 * Issue #3 fixed: `DeepEquals.deepEquals()` allows similar `Map` (or `Collection`) types to be compared without returning 'not equals' (false).  Example, `HashMap` and `LinkedHashMap` are compared on contents only.  However, compare a `SortedSet` (like `TreeMap`) to `HashMap` would fail unless the Map keys are in the same iterative order.
 * Tests added for `UrlUtilities`
 * Tests added for `Traverser`
* 1.9.2
 * Added wildcard to regex pattern to `StringUtilities`.  This API turns a DOS-like wildcard pattern (where * matches anything and ? matches a single character) into a regex pattern useful in `String.matches()` API.
* 1.9.1
 * Floating-point allow difference by epsilon value (currently hard-coded on `DeepEquals`.  Will likely be optional parameter in future version).
* 1.9.0
 * `MathUtilities` added.  Currently, variable length `minimum(arg0, arg1, ... argn)` and `maximum()` functions added.  Available for `long`, `double`, `BigInteger`, and `BigDecimal`.   These cover the smaller types.
 * `CaseInsensitiveMap` and `CaseInsensitiveSet` `keySet()` and `entrySet()` are faster as they do not make a copy of the entries.  Internally, `CaseInsensitiveString` caches it's hash, speeding up repeated access.
 * `StringUtilities levenshtein()` and `damerauLevenshtein()` added to compute edit length.  See Wikipedia for understand of the difference.  Currently recommend using `levenshtein()` as it uses less memory.
 * The Set returned from the `CaseInsensitiveMap.entrySet()` now contains mutable entry's (value-side). It had been using an immutable entry, which disallowed modification of the value-side during entry walk.
* 1.8.4
 * `UrlUtilities`, fixed issue where the default settings for the connection were changed, not the settings on the actual connection.
* 1.8.3
 * `ReflectionUtilities` has new `getClassAnnotation(classToCheck, annotation)` API which will return the annotation if it exists within the classes super class hierarchy or interface hierarchy.  Similarly, the `getMethodAnnotation()` API does the same thing for method annotations (allow inheritance - class or interface).
* 1.8.2
 * `CaseInsensitiveMap` methods `keySet()` and `entrySet()` return Sets that are identical to how the JDK returns 'view' Sets on the underlying storage.  This means that all operations, besides `add()` and `addAll()`, are supported.
 * `CaseInsensitiveMap.keySet()` returns a `Set` that is case insensitive (not a `CaseInsensitiveSet`, just a `Set` that ignores case).  Iterating this `Set` properly returns each originally stored item.
* 1.8.1
 * Fixed `CaseInsensitiveMap() removeAll()` was not removing when accessed via `keySet()`
* 1.8.0
 * Added `DateUtilities`.  See description above.
* 1.7.4
 * Added "res" protocol (resource) to `UrlUtilities` to allow files from classpath to easily be loaded.  Useful for testing.
* 1.7.2
 * `UrlUtilities.getContentFromUrl() / getContentFromUrlAsString()` - removed hard-coded proxy server name
* 1.7.1
 * `UrlUtilities.getContentFromUrl() / getContentFromUrlAsString()` - allow content to be fetched as `String` or binary (`byte[]`).
* 1.7.0
 * `SystemUtilities` added.  New API to fetch value from environment or System property
 * `UniqueIdGenerator` - checks for environment variable (or System property) JAVA_UTIL_CLUSTERID (0-99).  Will use this if set, otherwise last IP octet mod 100.
* 1.6.1
 * Added: `UrlUtilities.getContentFromUrl()`
* 1.6.0
 * Added `CaseInsensitiveSet`.
* 1.5.0
 * Fixed: `CaseInsensitiveMap's iterator.remove()` method, it did not remove items.
 * Fixed: `CaseInsensitiveMap's equals()` method, it required case to match on keys.
* 1.4.0
 * Initial version

By: John DeRegnaucourt and Ken Partlow
