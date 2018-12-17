# Dataset Repository

We provide several datasets of different sizes associated to their acceptable solutions (*i.e.* other solutions are possible, but you are more likely to find the one provided) for you to execute your code.

  - Small datasets are made for you to quickly check your implementation, and see how things go.
  - Big ones are more realistic, and such large data can have a huge impact on your execution time.

As a runtime reference, Christophe provided an *optimized* APB-solution that takes 3.7 seconds to compute a solution on the 100.000 dataset , and 78 seconds to parse, match, and output the result on the 1.000.000 dataset.

## Dataset Description

A dataset (or *input-file*) is made of 3 sections:

  1. metadata;
  2. student descriptions;
  3. and school descriptions.

The first section is a single line that contains 3 integers separated by spaces.
They respectively represent:

  - the number of students' profiles **P**,
  - the number of schools **S**,
  - the size of the wish-list **W** (the number of choices made by the students) of all and every students.

Then, the second section contains **P** lines, each describing a student profile.

A student profile is made of (5+**W**) data, spaces-separated, presented in the following order:

  - `first name` ;
  - `family name` ;
  - `gender` F or M ;
  - `birth-date` in the `yyyy-mm-dd` format ;
  - current `school academy` of the student ;
  - and finally W `school identifiers` which is modelled as a sequence of integers.

Then the third and last section contains **S** lines, each describing a school profile.

A school profile is made of 5 data, spaces-separated, presented in the following order:

  - `school name` ;
  - its `capacity` *i.e.* the number (integer) of students that the school can welcome this year ;
  -  `academy` of the school ;
  - `size` of the wish-list **N** ;
  - and the school `wish-list` which is **N** student identifiers.

In a school wish list, a given student is identified by her row-index in the **P** list.

*Note*: All text-fields can be upper/lower-cased letters with accents, dashes, and quotes.

## Examples

### Input file description

Below is an example of input file.

```
10 5 3
Geraldine   TELLIER          F 2000-02-25 Saint-Chamond     1 2 3
Filipe      DAVY             M 2000-08-18 Libourne          2 1 0
Brice       MANY             M 1998-12-20 Limoges           1 2 0
Erwan       GIRONDE          M 2000-08-24 Nice              1 2 3
Roxanne     FERNANDES        F 2001-08-21 Lanester          2 1 0
Thomas      BERTHET          M 2001-05-23 Dole              1 2 3
Marine      LOZACH           F 2000-01-30 Dijon             1 2 4
Clarisse    LEBAILLIF        F 1999-10-28 Avignon           0 1 3
Charlène    BENMANSOUR       F 2000-11-24 Marseille         4 3 1
Océane      BONNEFOY         F 1999-04-07 Villenave-d'Ornon 2 1 0
CPGE_Lycée_Bellevue          1 Toulouse         5 2 9 1 7 4
Université_Clermont-Auvergne 4 Clermont-Ferrand 10 7 9 1 3 2 5 0 4 6 8
Universitée_d’Angers         3 Angers           8 9 1 3 2 5 0 4 6
IUT_Chimie                   1 Grenoble         5 7 0 3 5 8
IUT_Environnement            1 Reims            2 6 8
```

As described in the previous section: 

  - they are 10 student profiles, each making 3 choices, across 5 different schools. 
  - The first line of the second section states that a girl named _Geraldine TELLIER_, born the _25th of february_ in _2000_, currently living in _Saint-Chamond_, wants to go to schools identified by ids _1_, _2_ and _3_. 
  - By looking at the third section, we can say that she wants to go to the _Université Clermont Auvergne_ (1) first, then to _Université d'Angers_ (2), then finally to _IUT Chimie of Grenoble_ (3); in that very order. 
  - We can also note that _IUT Chimie_ has ranked her in _third position_ and has a capacity of _1_ student.

### Expected output file

Here is an example of the expected solution file to compute based on the data of the previous input file. In this case, it implements a stable mariage between schools and students, based on their respective wish lists.

The output format is a single line sequence of integers representing recruitments according to a position-based approach:

```
1 2 1 1 2 1 4 0 3 2
```

It means that :

  - Student #0 (here Geraldine) is recruited by school #1 (here Université_Clermont-Auvergne)
  - Student #1 (Filipe) is recruited by school #2 (Universitée_d’Angers)
  - ...
  - Student #10 (Océane) is also recruited by school #2.

If a student cannot be recruited in any school, the associated output is an `X`.

