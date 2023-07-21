***
请参阅[MajdataView](https://github.com/LingFeng-bbben/MajdataView)
***
今后的更新和说明也将在那个页面发布。请留意。

## Modifications and implementations

### Adjustable waiting time

It is now possible to adjust the waiting time for slides using length divisors based on the current BPM.

`(sh)(ss)(sn)[(ld)###(ld)],`

#### Before

```
(170) {4}
,,,,
1-5[1.412##0.353],
```

#### After

```
(170) {4}
,,,,
1-5[1:1###4:1],
```

### Single-note HSpeed

It is now possible to adjust the HSpeed for a single note in a single statement instead of writing it twice.

`(n)hs*(hs)>,`

#### Before

```
(170) {4}
,,,,
1,2,3,4,

<HS*1.5>
5,

<HS*1>
6,7,8,
```

#### After

```
(170) {4}
,,,,
1,2,3,4,5hs*1.5>,6,7,8,
```

### Invisible notes

It is now possible to add invisible notes which is actually just a note with an HSpeed of 1000.

`(n)i,` note is invisible.

`(n)ii,` note and judgement is invisible.

#### Before

```
(170) {4}
,,,,
1,2,

<HS*1000>
3,

<HS*1>
4,5,6,

<HS*-1000>
7,

<HS*1>
8,
```

#### After

```
(170) {4}
,,,,
1,2,3i,4,5,6,7ii,8,
```

### Note chains

It is now possible to chain notes in a single sequence and return the timeline pointer to the next beat of the initial position afterwards. However, simultaneous notes will not be considered Each when using this method.

`(n)'(n)...,`

#### Before

```
(170) {8}
,,,,,,,,,,,,,,,,
1,2,3/7,4,5/1,6,7/3,8,1/5,2,3/7,4,5/1,6,7/3,8,1/5,
```

#### After

```
(170) {8}
,,,,,,,,,,,,,,,,
1'2'3'4'5'6'7'8'1'2'3'4'5'6'7'8'1
,,7,,1,,3,,5,,7,,1,,3,,5,
```

### Labels and Gotos

It is now possible to label the current position in the timeline and move the pointer to that position later in the fumen.

`label: (name)` Set the position of the label
`goto: (name)` Move the pointer to the position of the label

#### Before

```
(170) {8}
,,,,,,,,,,,,,,,,
1,2,3/7,4,5/1,6,7/3,8,1/5,2,3/7,4,5/1,6,7/3,8,1/5,
```

#### After

```
(170) {8}
,,,,,,,,,,,,,,,,

label: start;
1,2,3,4,5,6,7,8,

goto: start; {4}
,7,1,3,
5,7,1,3,5,
```
