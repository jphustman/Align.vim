                 [ALIGN/ALIGNMAPS NEEDS VIM 7.0 AS OF V29/34]

Align and AlignMaps lets you align statements on their equal signs, make comment boxes, align comments, align declarations, etc.

Note: this plugin is not a left&right margin justification tool!  See vimscript#177, vimscript#2324, or vimscript#3728 for that.
Note: if you have vim 7.1 or later, your vimball should unpack just fine without having to update it.

There are two basic commands provided by this package:

        AlignCtrl options sep1 sep2 sep3 ...
        [range]Align sep1 sep2 sep3 ...

The "sep#" are regular expressions which describe separators that delineate fields; Align will line up the separators. The range may be any Vim range, _including_ visual-blocks.  Align works on lines of the form:
(ws==whitespace, sep==separator, field==text)

    ws-field-ws-sep-ws-field-ws-sep-ws-field-...
    ws-field-ws-sep-ws-field-ws-sep-ws-field-...

Note that white-space (ws) surrounding separators is ignored.

The Align package includes:

  Align : the basic alignment command
  AlignCtrl : provides options for the next call to :Align
  AlignMaps : many three or four key maps which support aligning C/C++ style declarations, ()?..:.., expressions, C/C++ comments, numbers, C preprocessor definitions, tables based on tabs or spaces, and more.

In addition, AutoAlign (vimscript#884) uses the Align function to align =s as you type.

Align handles alignment on multiple separators, not just the first one, and the separators may be the same across the line or different.  With AlignCtrl one may specify that separators are cyclic (re-used sequentially) or equivalent (all separators are simultaneously active).

There are several options to help with deciding what to do with initial white space.   By default Align re-uses the first line's initial white space, but one may use AlignCtrl to retain or remove each line's initial white space.

The <Align.vim> and <AlignMaps.vim> files are plugins and require vim 6.1 or higher.


EXAMPLES:

:5,10Align =
    Align on '=' signs

:'<,'>Align = + - \* /
    Align on any of the five separator characters shown.
    Note that visual block mode was used to fire off Align.

:AlignCtrl =lp1P1I
    which means:
    = all separators are equivalent
    l fields will be left-justified
    p1 pad one space before each separator
    P1 pad one space after each separator
    I  preserve and apply the first line's leading white space to all
       Align'd lines

:help align
    Gives help for Align


ALIGNMENT CONTROL

Alignment control allows for left or right justification or centering of fields, cyclic (sequentially active) or equivalent (simultaneously active) regular expressions to specify field separators, initial white space control, optional visual-block use (ie. apply Alignment only within a block), user-specified white-space padding about separators, and multiple separators.

MANY ALIGNMENT MAPS

AlignMaps.vim provides a number of maps which make using this package easy.  They typically either apply to the range 'a,. (from mark a to current line) or use the visual-selection (V, v, or ctrl-v selected):

\t=  : align assignments (don't count logic, like == or !=)
\t,  : align on commas
\t|  : align on vertical bars (|)
\tsp : align on whitespace
\tt  : align LaTeX tabular tables

AlignMaps also provides some internally complex maps for aligning C declarations, Ansi C function arguments, html tables, LaTeX tabulars, and trailing comments:

\acom : align comments
\adec : align C declarations (one variable per line)
\afnc : align ansi-style C function input arguments
\Htd  : align html tables

To see some examples of this, check out

    http://www.drchip.org/astronaut/vim/align.html#Examples

(the proportional fonts used by most browsers in showing you this page preclude showing the examples here). The help for Align and AlignCtrl also contains many examples.
(for those of you who prefer not to have the maps that AlignMaps.vim provides, simply remove the AlignMapsPlugin.vim from .vim/plugin and AlignMaps.vim from .vim/autoload - that's why AlignMaps is separate from Align)

ALIGNMENT ON VISUAL BLOCKS AND g,v-LIKE CONTROL

Sometimes one wants to align only a subset of text in a range, based on patterns or column extents.  Align supports both types of restrictions!

    Visual-block selection may be used to restrict Align to operate only
    within that visual block.

    AlignCtrl supports "g" and "v" patterns that restrict Align to

    operate on lines which match (or don't match, respectively) those
    patterns.

NEW STUFF:

There's a number of new AlignCtrl options:

    - allows one to skip a separator (treat it as part of a field)
    + repeat the last lrc justification (ex. lr+ == lrrrrrr... )
    : treat the rest of the line as a field; acts as a modifier
      to the last lrc.
    < left-justify the separator
    > right-justify the separator
    | center the separator

These are, except for the ":", cyclic parameters.  In other words, >< is equivalent to ><><><><... .  Thus separators can be of differing lengths (ex.  -\+ as a separator pattern can match -, --, ---, etc and the separators will be left/right/center justified as you wish).

To get automatic, as-you-type, aligning of = in the C, vimL, and other languages, check out vimscript#884 for several ftplugins (which use Align).


Alternative Aligners:
    Gergely Kontra's vimscript#176

Thank you for rating Align!

---------------------------------------
DISCUSSION and COMMENTS:
---------------------------------------

Please use email for bugs.  Enjoy!

(alpha/beta version available at http://mysite.verizon.net/astronaut/vim/index.html#ALIGN)

install details
1. You'll need to have plugins enabled: in your home directory, have at least the following two lines in your .vimrc file:
   set nocp
   filetype plugin on

2. Using vim 7.1 or later:
  vim Align.vba.gz
   :so %
   :q

3. Using vim 7.0: see http://mysite.verizon.net/astronaut/vim/index.html#VIMBALL to get and install an up-to-date version of vimball.  Then follow the simple directions for installation of Align/AlignMaps above!  Or, preferably: upgrade your copy of vim.

(this version of Align/AlignMaps requires vim 7.0)
