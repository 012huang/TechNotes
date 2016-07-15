

# graph-easy

## 命令

```
$ cat fig （一个纯文本文件）
[ A ] -> [ B ] -> [ C ]
$ graph-easy fig
or
$ echo "[ A ] -> [ B ] -> [ C ]" | graph-easy
+---+     +---+     +---+
| A | --> | B | --> | C |
+---+     +---+     +---+
```

## example 1

```
graph { flow: west; }
[ A ] -> [ B ] -> [ C ]

+---+     +---+     +---+
| C | <-- | B | <-- | A |
+---+     +---+     +---+
```

## example 2

```
graph { flow: west; }

[ Duisburg ] -> [ Siegen ] { flow: left; } -> [ Adenau ]
[ Siegen ] -> { flow: up; } [ Monschau ]

+----------+
| Monschau |
+----------+
  ^
  |
  |
+----------+     +----------+
|  Siegen  | <-- | Duisburg |
+----------+     +----------+
  |
  |
  v
+----------+
|  Adenau  |
+----------+
```

## example 3

```
[ A | B | C || D]

[ 1 ] -> [ ABCD.2]

         +---+
         | 1 |
         +---+
           |
           |
           v
+---+---+----+
| A | B |  C |
+---+---+----+
| D |
+---+
```

## example 4

```
[ A || D]

[ 1 ] -> [ AD.1]

          +---+
          | A |
          +---+
+---+     |   |
| 1 | --> | D |
+---+     +---+
```


## example 5

```
[ C ] -- text --> { start: south; } [ S ] { origin: C; offset: 1,2; }
[ C ] -> { start: north; } [ N ] { origin: C; offset: 0,-2; }
[ C ] -> { start: east; }  [ E ] { origin: C; offset: 2,0; }
[ C ] -> { start: west; }  [ W ] { origin: C; offset: -2,0; }

          +-------+
          |   N   |
          +-------+
            ^
            |
            |
+---+     +-------+     +---+
| W | <-- |   C   | --> | E |
+---+     +-------+     +---+
            |
            | text
            |
            |      +---+
            +----> | S |
                   +---+

```

## example 6

```
[ Bonn ] -> [ Berlin ]
[ Berlin ] -> [ Frankfurt ] { border: 1px dotted black; }
[ Frankfurt ] -> [ Dresden ]
[ Berlin ] ..> [ Potsdam ]
[ Potsdam ] => [ Cottbus ]

+------+     +---------+     .............     +---------+
| Bonn | --> | Berlin  | --> : Frankfurt : --> | Dresden |
+------+     +---------+     :...........:     +---------+
               :
               :
               v
             +---------+     +-----------+
             | Potsdam | ==> |  Cottbus  |
             +---------+     +-----------+

```


## Reference
1. [Graph::Easy - Manual](http://bloodgate.com/perl/graph/manual/syntax.html)
2. [create specific graph layouts](http://bloodgate.com/perl/graph/manual/hinting.html#size)

