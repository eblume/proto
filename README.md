proto
=====

`proto` gives Go operations like `Map`, `Reduce`, `Filter`, `De/Multiplex`, etc.
without sacrificing idiomatic harmony or speed. It also introduces a convenience
type for these functions, `Proto`, which is a stand-in for the empty interface
(interface{}), which is used to box values being sent to these operations.

Examples
--------

* Double every integer a slice:

      inputs := []Proto{0, 1, 2, 3, 4, 5, 6}
      sent := Send(inputs)
      doubler := func(a Proto) Proto {
          return a.(int) * 2
      }
      mapped := Map(doubler, sent)
      doubled := Gather(mapped)

* Double every integer, chained:

      inputs := []Proto{0, 1, 2, 3, 4, 5, 6}
      doubled := Gather(Map(func(a Proto) Proto {
          return a.(int) * 2
      }, Send(inputs)))

License
-------

Please see COPYING for more details on the licensing of this software.
