# Assistant Bot

Commands to support continuous assessment of assignments based on VCS.

# Information architurecture

The data is organized in subjects, and each subject in courses.

```
$TEACHING_HOME
│
├── <subject>
│   └── courses
│       ├── 2020-2021
│       ├── 2021-2022
│       ├── 2022-2023
│       ...
│
├── <subject>
│   └── courses
│       ├── 2020-2021
│       ├── 2021-2022
│       ├── 2022-2023
│       ...
...
```

And the main sections of each course are:

```
<subject>/courses/2020-2021
│
├── de
│
├── di
│   ├── assessments
│   ├── assignments
│   └── data
├── exams
│
└── gradinds
```


# User Interface

The only interface is a CLI. It includes commands for common and
repetitive tasks like creating a new course, start an assessment,
collecting grading info, retreiving data for a student, ...

The basic format is:

```shell
$ <script> [...args] <verb> <noun> [...args]
```

Where usual _verbs_ are `create`, `update`, `cd`, ... and some common
_nouns_: `assessment`, `course`, ...

The application favors convention and context over configuration. So
instead of specify the subject, course, assignment, ...:

  * When the user runs a simbolic link to the script. The name of the
    link is the name of the subject.

    The magic incantation:

    ```shell
    $ <script> -s IPM create course 2020-201 
    ```

    is equivalent to:

    ```shell
    $ IPM create course 2020-2021
    ```
    
    providing `IPM` is a symbolic link to `<script>`


  * The subject and course is implicit in the current directory path.

    The magic incantation:

    ```shell
    $ <script> -s IPM -c 2020-2021 create assigment 01-desktop
    ```

    is equivalent to:

    ```shell
    .../IPM/courses/2020-2021$ IPM create assigment 01-desktop
    ```

  * The course is implict in the current academic period.

    The magic incantation:

    ```shell
    $ <script> -s IPM create course 2020-2021
    ```
 
    is equivalent to:

    ```shell
    $ IPM create course
    ```

    providing current date is between 09/2020 and 07/2021.


The preference order of the arguments is:

  1. Script arguments.
  2. Environment variables.
  3. Config file.
  4. Conventions and context.


# i18n

The user's locale decide the language of the IU and **the language of
the verbs and nouns**.

_TODO_: ¿ Permitimos una mezlca de idiomas en _verbos_ y _nombres_ ?
