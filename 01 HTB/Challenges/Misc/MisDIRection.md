# 🧩 MisDIRection

Tags: #🧩
Related to: [[awk]], [[base64]], [[find]], [[grep]], [[sort]], [[tr]]
See also:
Previous: [[HTB]]

# Description

During an assessment of a unix system the HTB team found a suspicious directory. They looked at everything within but couldn't find any files with malicious intent.

## Validate checksum

	echo " " | sha256sum -c -

```text

```

## Unzip

	unzip misDIRection.zip
	tree

```text
.
├── 0
│   └── 6
├── 1
│   ├── 22
│   └── 30
├── 2
│   └── 34
├── 3
├── 4
├── 5
│   └── 16
├── 6
├── 7
├── 8
├── 9
│   └── 36
├── a
├── A
├── b
├── B
│   └── 23
├── c
├── C
│   └── 4
├── d
│   └── 13
├── D
│   └── 26
├── e
│   └── 5
├── E
│   └── 14
├── f
├── F
│   ├── 19
│   ├── 2
│   └── 27
├── g
├── G
├── h
├── H
├── i
├── I
├── j
│   ├── 10
│   └── 12
├── J
│   └── 8
├── k
├── K
├── l
├── L
├── m
├── M
├── n
├── N
│   ├── 11
│   ├── 25
│   ├── 31
│   └── 33
├── o
├── O
├── p
│   └── 32
├── P
├── q
├── Q
├── r
├── R
│   ├── 3
│   └── 7
├── s
│   └── 24
├── S
│   └── 1
├── t
├── T
├── u
│   ├── 20
│   └── 28
├── U
│   └── 9
├── v
├── V
│   └── 35
├── w
├── W
├── x
│   └── 15
├── X
│   ├── 17
│   ├── 21
│   └── 29
├── y
├── Y
├── z
│   └── 18
└── Z

62 directories, 36 files
```

## Examine

Unzipping the files sends out a large amount of folders. Some have files in them, and some do not. Interestingly enough, each file is empty, but numbered. A quick `find` and `sort` revealed that these numbers are unique. I made the assumption that the folder the file was in represented a letter/number and the number of the file was the order in which it was to be read.

## Solving

1. Find all files and the parent folder
2. Separate the file and folder into columns
3. Sort by the file
4. Filter out the ordering number
5. Put all rows into a single line
6. Decode the base64 string

1. find all the files: `find` and only list files with `-type f`
2. use `awk` to split on `/` and only print the folder and file
3. `sort` by the file column
4. use `awk` to split on `' '` (a space) and only print the folder (there are other ways to do this, `grep -E` for example)
5. delete all the `\n` of every row with `tr`
6. decode with `base64 -d`

Piping it all together looks like this:

	find . -type f | awk -F'/' '{ print $2 " " $3 }' | sort -n -k2 | awk -F' ' '{ print $1 }' | tr -d '\n' | base64 -d

###  1. Find all files and the parent folder

	find

```text
.
./K
./j
./j/10
./j/12
./G
./l
./W
./I
./d
./d/13
./z
./z/18
./Q
./s
./s/24
./e
./e/5
./v
./0
./0/6
./E
./E/14
./7
./1
./1/30
./1/22
./Z
./A
./h
./c
./q
./J
./J/8
./X
./X/29
./X/21
./X/17
./Y
./u
./u/28
./u/20
./F
./F/19
./F/2
./F/27
./V
./V/35
./S
./S/1
./m
./2
./2/34
./o
./8
./g
./H
./f
./3
./T
./O
./U
./U/9
./n
./M
./r
./a
./6
./L
./4
./D
./D/26
./5
./5/16
./i
./w
./b
./p
./p/32
./P
./x
./x/15
./R
./R/7
./R/3
./k
./B
./B/23
./C
./C/4
./y
./9
./9/36
./t
./N
./N/31
./N/33
./N/11
./N/25
```

	find -type f

```text
./j/10
./j/12
./d/13
./z/18
./s/24
./e/5
./0/6
./E/14
./1/30
./1/22
./J/8
./X/29
./X/21
./X/17
./u/28
./u/20
./F/19
./F/2
./F/27
./V/35
./S/1
./2/34
./U/9
./D/26
./5/16
./p/32
./x/15
./R/7
./R/3
./B/23
./C/4
./9/36
./N/31
./N/33
./N/11
./N/25
```

### 2. Separate the file and folder into columns

	find -type f | awk -F '/' '{ print $2 " " $3 }'

```text
j 10
j 12
d 13
z 18
s 24
e 5
0 6
E 14
1 30
1 22
J 8
X 29
X 21
X 17
u 28
u 20
F 19
F 2
F 27
V 35
S 1
2 34
U 9
D 26
5 16
p 32
x 15
R 7
R 3
B 23
C 4
9 36
N 31
N 33
N 11
N 25
```

### 3. Sort by the file

	find -type f | awk -F '/' '{ print $2 " " $3 }' | sort -n -k2

```text
S 1
F 2
R 3
C 4
e 5
0 6
R 7
J 8
U 9
j 10
N 11
j 12
d 13
E 14
x 15
5 16
X 17
z 18
F 19
u 20
X 21
1 22
B 23
s 24
N 25
D 26
F 27
u 28
X 29
1 30
N 31
p 32
N 33
2 34
V 35
9 36
```

### 4. Filter out the ordering number

	find -type f | awk -F '/' '{ print $2 " " $3 }' | sort -n -k2 | awk -F ' ' '{ print $1 }'

```text
S
F
R
C
e
0
R
J
U
j
N
j
d
E
x
5
X
z
F
u
X
1
B
s
N
D
F
u
X
1
N
p
N
2
V
9
```

### 5. Put all rows into a single line

	find -type f | awk -F '/' '{ print $2 " " $3 }' | sort -n -k2 | awk -F ' ' '{ print $1 }' | tr -d '\n'

```text
SFRCe0RJUjNjdEx5XzFuX1BsNDFuX1NpN2V9
```

### 6. Decode the base64 string

	find -type f | awk -F '/' '{ print $2 " " $3 }' | sort -n -k2 | awk -F ' ' '{ print $1 }' | tr -d '\n' | base64 -d

```text
HTB{...}
```