# pallet.thread-expr

A library containing macros for use in clojure threading expressions (using ->).

See [reference documentation](http://pallet.github.com/thread-expr/autodoc/index.html)
and [annotated source](http://pallet.github.com/thread-expr/marginalia/uberdoc.html).

## Examples

**Threaded arg exposure:**

`arg->` exposes the threaded arg, binding it to the supplied variable. For example:

```clojure
(-> 2
   (arg-> [x]
     (* (inc x))))

;=> 6
```

Expands to:

```clojure
(-> 2 
   ((fn [arg] (let [x arg] (-> arg (* inc x))))))

;=> 6
```
Note the extra set of parens in the expansion; the threading macro feeds the current argument in as `arg`, binds it to the supplied var using `let`, and resumes threading for all forms inside of `arg->`.

**Threaded list comprehension:**

The following use of `for->`:

```clojure
(-> 1
   (for-> [x [1 2 3]]
     (+ x)))

;=> 7
```

Expands to:

```clojure
(-> 1
   (+ 1)
   (+ 2)
   (+ 3))

;=> 7
```

## Installation

thread-expr is distributed as a jar, and is available in the
[sonatype repository](http://oss.sonatype.org/content/repositories/releases/org/cloudhoist).

Installation is with maven or your favourite maven repository aware build tool.

### lein/cake project.clj

    :dependencies [[org.cloudhoist/thread-expr "1.1.0"]]
    :repositories {"sonatype"
                   "http://oss.sonatype.org/content/repositories/releases"}

### maven pom.xml

    <dependencies>
      <dependency>
        <groupId>org.cloudhoist</groupId>
        <artifactId>thread-expr</artifactId>
        <version>1.1.0</version>
      </dependency>
    <dependencies>

    <repositories>
      <repository>
        <id>sonatype</id>
        <url>http://oss.sonatype.org/content/repositories/releases</url>
      </repository>
    </repositories>

## License

Licensed under [EPL](http://www.eclipse.org/legal/epl-v10.html)

Copyright 2011 Hugo Duncan.
