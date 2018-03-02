---
layout: post
title: "Groups in Typelevel/Cats"
author: "Yesid Botero"
---
# Group

`Group` extends of `Monoid` by providing an `inverse` for each element that fits into `A`.

```
trait Monoid[A] extends Semigroup[A] {
  def empty: A
}

trait Group[A] extends Monoid[A] {
  def inverse(a: A): A
}
```
Let's see an example of this using Group `Int` with respect to the binary operation `+`

```
import cats._

val intGroup = Group.apply[Int]

intGroup.inverse(10)
```

The `empty` element should be the result of combining an element with its respective `inverse`. Because a Group is also a Semigroup, we can use an associative binary operation for check this.

```
combine(x, inverse(x)) = combine(inverse(x), x) = empty
```
The `remove` method helps us to remove a element from another, let's see the sign of this method  
```
  def remove(a: A, b: A): A = combine(a, inverse(b))
```
Let's see a example removing the element `5` of `10`
```
import cats._

val intGroup = Group.apply[Int]

intGroup.remove(5, 10) ///as it was expected we obtained another Int element
```
N.B.
Cats defines the `Group` type class in cats-kernel. The
[`cats` package object](https://github.com/typelevel/cats/blob/master/core/src/main/scala/cats/package.scala)
defines type aliases to the `Group` from cats-kernel, so that you can simply import `cats.Group`.
