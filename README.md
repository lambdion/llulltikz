# The *Tabula Generalis* of Ramon Llull

<img src="./1.svg" align="right" />

Ramon Llull (or Raimundus Lullius/Raymond Lully) was a 13<sup>th</sup>-century philosopher who spent his life developing a kind of theological-philosophical system based in the mathematics of combinatorics. This repository contains [TikZ](https://tikz.dev/) code that draws the four explanatory figures of the *Ars Brevis*, a 1290 work that reduced the elements of his system to only 9. These four figures are accompanied by a table which explains the meanings of the nine symbols (the letters B–K, omitting J). I made these for a translation/edition of Umberto Eco’s *La Ricerca della Lingua Perfetta nella Cultura Europea* because the graphics in that book are unsatisfying, some parts can barely be read. Only by comparing with other sources was I able to discern the small text. Therefore I created these higher-quality diagrams which can be easily used at large scales, whilst still preserving the text and layout of the versions in the book.

# Sources

The [Centre de Documentació Ramon Llull](https://quisestlullus.narpan.net/) has [modern versions of these diagrams](https://quisestlullus.narpan.net/en/ars-brevis) with text in Llull’s native Catalan, along with many other wonderful resources.

The Stanford Encyclopedia of Philosophy has [an extensive article on Llull](https://plato.stanford.edu/entries/llull/#AlphFiguTernArs), featuring photographed diagrams and explanations.

There is a [high quality scan of an original manuscript](https://archive.org/details/illuminatisacrep00llul/page/n33/) on the Internet Archive, which has helpful color additions, though the writing contains misleading scribal abbreviations.

[*Ramon Llull’s Ars Magna*](https://doi.org/10.1007/978-3-319-74718-7_3) (Jensen, 2018) also contains some very readable Latin scans, with non-handwritten text.

# Technical
The code uses at several points the following construction in order to print a given element of a list of strings within a `\foreach`:

``` tex
\pgfmathparse{{"A","B","C","D"}[\x]} % \x is the iterating index variable
\edef\letter{\pgfmathresult} % \letter can now be used within the loop to get the current letter
```

Furthermore, by scouring the [TikZ decorations manual](https://tikz.dev/library-decorations#pgf.decorations.text), I landed upon a way to add text that curves, essential for these radial diagrams.

``` tex
\draw [decoration={
       text along path,
       text={The quick brown fox jumps over the lazy dog.}, % Some formatting breaks when in this text field.
       text align={center} % Aligns the text to the center of the curve
       },
       decorate]
           
      (180:5cm) % Start location of the curve, here defined in polar coordinates to better match up with the arc values below
      
      arc[start angle=180, % Angle of the circle that the arc should begin at
          end angle=0, % Angle of the circle that the arc should end at
          % delta angle can be used in place of end angle to give a change-in value
          radius=5cm]; % Radius of the arc
```

## Building

All documents should typeset correctly with `pdflatex`, or the `diagram` environment can be inserted into another document.

``` sh
for f in ./*.tex; do pdflatex "$f"; done
```

The first diagram is available as an SVG, and a PDF is included that contains all four.
