<h2>fastutil</h2>

<h3>Introduction</h3>
<HR WIDTH="90%">
`fastutil` extends the `Java™ Collections Framework` by providing type-specific `maps`, `sets`, `lists` and `queues` with a small memory footprint and fast access and insertion; provides also big (64-bit) `arrays`, `sets` and `lists`, and fast, practical I/O classes for binary and text files. It is free software distributed under the `Apache License 2.0`. It requires `Java 6` or newer.

The classes implement their standard counterpart interface (e.g., `Map` for `maps`) and can be plugged into existing code. Moreover, they provide additional features (such as bidirectional `iterators`) that are not available in the standard classes.

Besides objects and primitive types, `fastutil` classes provide support for references, that is, `objects` that are compared using the equality operator rather than the `equals()` method.

The sources are generated using a C preprocessor, starting from a set of driver files. You can peek at the `javadoc`-generated documentation. In particular, the overview explains the design choices used in `fastutil`.

<h3>Big data structures</h3>
<HR WIDTH="90%">
With `fastutil 6`, a new set of classes makes it possible to handle very large collections: in particular, collections whose size exceeds 2^31. `Big arrays` are arrays-of-arrays handled by a wealth of static methods that act on them as if they were monodimensional arrays with 64-bit indices, and big lists provide 64-bit list access. The size of a `hash big set` is limited only by the amount of core memory. The usual methods from `java.util.Arrays` and similar classes have been extended to `big arrays`: have a look at the `Javadoc` documentation of `BigArrays` and `IntBigArrays` to get an idea of the generic and type-specific methods available.

<h3>Java™ 5</h3>
<HR WIDTH="90%">
The release 5 of `fastutil` needs `Java 5`, and marks a revolution in the way the classes are organized. Besides full support for generics, which can help with object-based classes (but is rather irrelevant in type-specific classes), `fastutil` is now strongly based on what is probably the less hyped and most important feature of `Java 5`: covariant return-type overriding. A method `x()` returning an object of type `T` can now be overriden by a method returning an object of type `U`, where `U` is a subclass of (or implements) `T`.

Covariant return-type overriding has always been supported by the JVM, but was inaccessible at the syntax level. In `Java 5` this irritating limitation has been lifted, opening a new world of clarity and orthogonality in organizing collection classes. In particular, interface strengthening makes it possible to use all features of `fastutil` classes without type casting: for instance, `IntSet.iterator()` is strengthened, w.r.t. `Set.iterator()`, so that it returns an IntIterator instead of a simple Iterator. Although type casting was previosuly used to simulate this feature, it made using the hundreds of classes in `fastutil` difficult and error-prone, as every type cast had to be checked against the documentation.

Another advantage of covariant return-type overriding is that implementations can declare to return more specific (usually, more powerful) types than those specified by their interface. For instance, `IntAVLTreeSet.iterator()` returns actually an `IntListIterator`, whereas `IntSortedSet.iterator()` is specified as returning just an `IntBidirectionalIterator`.

<h3>Installation</h3>
<HR WIDTH="90%">
You can grab fastutil from Maven Central. Otherwise, you just have to install the `.jar` file coming with the distribution.

Note that the `jar` file is huge, due to the large number of classes: if you plan to ship your own jar with some `fastutil` classes included, you should look at `AutoJar` or similar tools.

<h3>History and Motivation</h3>
<HR WIDTH="90%">
`fastutil` came up as a necessity during the development of `UbiCrawler`, as we needed to manage structures with dozens of millions of items very efficiently. The same reasons led to the development of the high-performance classes of `dsiutils` and `MG4J` (e.g., `MutableString`).
