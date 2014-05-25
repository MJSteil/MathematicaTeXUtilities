# TeXUtilities


Set of tools useful for customizing TeX output of Mathematica.

Contains also patch fixing behavior of `TeXForm` for expressions with custom
formatting defined using `Format[expr, TeXForm]`.


* [Installation](#installation)
    * [Automatic installation (using ProjectInstaller)](#automatic-installation-using-projectinstaller)
    * [Semi-automatic installation](#semi-automatic-installation)
    * [Manual installation](#manual-installation)
    * [No installation](#no-installation)
* [Documentation](#documentation)
* [Usage example](#usage-example)



## Installation


### Automatic installation (using ProjectInstaller)

To install package using
[ProjectInstaller](https://github.com/lshifr/ProjectInstaller)
evaluate:
```Mathematica
ProjectInstall["https://github.com/jkuczm/MathematicaTeXUtilities/releases/download/v1.0.0/TeXUtilities.zip"]
```

To load the package evaluate:
```Mathematica
Needs["TeXUtilities`"]
```


### Semi-automatic installation

1. Download latest released
   [TeXUtilities.zip](https://github.com/jkuczm/MathematicaTeXUtilities/releases/download/v1.0.0/TeXUtilities.zip)
   file.

2. Open Mathematica and choose `File > Install...`

3. In "Install Mathematica Item" window, which should open, choose:
    * Type of Item to Install: Application
    * Source: From File (file chooser should open, choose downloaded `TeXUtilities.zip`)
    * Install Name: TeXUtilities (this field should be automatically filled after choosing file)
    * choose whether application should be installed for current user or for all users
      (to install for all users you may need root/administrator privileges)
    * click OK

To load the package evaluate:
```Mathematica
Needs["TeXUtilities`"]
```


### Manual installation

1. Download latest released
   [TeXUtilities.zip](https://github.com/jkuczm/MathematicaTeXUtilities/releases/download/v1.0.0/TeXUtilities.zip)
   file.

2. Extract downloaded `TeXUtilities.zip` to any directory which is on Mathematica `$Path`,
   e.g. to one obtained by evaluating `FileNameJoin[{$UserBaseDirectory,"Applications"}]`.


To load the package evaluate:
```Mathematica
Needs["TeXUtilities`"]
```


### No installation

To use package directly from the Web, without installation, evaluate:
```Mathematica
Get["https://raw.githubusercontent.com/jkuczm/MathematicaTeXUtilities/master/NoInstall.m"]
```

Note that, with this method of initialization,
package documentation will not be available in Mathematica Documentation Center.



## Documentation

This application comes with documentation integrated with Mathematica Documentation Center.
To use it search for "TeXUtilities" in documentation center
or press `F1` key with cursor on name of any of symbols introduced by this application.



## Usage example

Define custom TeX formatting for some symbols:

```Mathematica
Format[something, TeXForm] = TeXVerbatim["\\macro $1+1$ \\command[a=b]{c}"];

Format[f[x__], TeXForm] := TeXDelimited["\\left(", x, "\\right)", "DelimSeparator" -> ""]

Format[g[x__], TeXForm] := TeXCommand["g", {{a -> b}, x}]

Format[h[x__], TeXForm] := TeXEnvironment["myEnv", x]
```

Use `TeXForm` as usual:

```Mathematica
TeXForm[
    h[
        f[1 + alpha],
        5 - g[3, g[2]],
        something
    ]
]
```

Output is:
```TeX
\begin{myEnv}
    \left(\alpha +1\right)
    5-\g[a=b]{3}{\g[a=b]{2}}
    \macro $1+1$ \command[a=b]{c}
\end{myEnv}
```
