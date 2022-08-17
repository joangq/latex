# Personal LaTeX Template

Custom blank LaTeX project template for writing essays.

This template was made using VSCode with the [LaTeX Workshop](https://github.com/James-Yu/LaTeX-Workshop) extension. The `.vscode\` folder is included, so that the `settings.json` configuration file is easily accessible.

It's basically an example of multi-file LaTeX documents. The global config, as well as all the `\usepackage` package imports, is located in the `jig.sty` style file.

Every part or section should go inside the `\sections` folder as a `.tex` file each one of them, should follow a simple structure:

```latex
\documentclass[../main.tex]{subfiles}

\begin{document}

% Your code here

\end{document}
```

Every section file is appended in the main file `blank_project.tex` using the `subfiles` package. Because the personal style package is loaded on the main file, all the packages and command definitions are shared between files. The section, chapter and part count is made globally, so it doesn't matter if the `\section` command is inside of the separate files, or used in the main file. Then, the main file has a very simple structure:

```latex
\documentclass{article}
\usepackage[utf8]{inputenc}

\usepackage{jig} % Global config
\usepackage{subfiles} % Best loaded last in the preamble

% Global configurations here

\begin{document}

    %...

    \subfile{sections/filename_1} % Only the filename should be included
    \subfile{sections/filename_2} % Don't include the '.tex' extension
    \subfile{sections/filename_3}

    % ...

\end{document}
```

The bibliography is managed by the `natbib` package. Whenever the references page has to be added, it's only necessary to use the `\bibliography{FILENAME.bib}` command. In this case, is used at the end of the file, so the file ends with:

```latex
% Bibliography
\newpage
\part{Bibliografía}
\bibliographystyle{unsrt}
\bibliography{bibliography.bib}
```

To hide the bibliography default title, custom command `\bibsectname{}` is used previously.

The `settings.json` file contains the arguments necessary to compile the main file using `latexmk` into the `.\out\` folder.

```js
{
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",           // <- Use latexmk
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",                     // <- Compile as pdf
                "-outdir=out",              // <- Compile files directory
                "%DOC%"
            ],
            "env": {}
        }
    ]
}
```
