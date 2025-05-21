<p align="center">
  <h3 align="center">Easy LaTeX Translate</h3>
  <p align="center">
    A simple method for translating LaTeX documents.
  </p>
</p>

## What?
This repository aims to describe how to translate LaTeX documents easily.

## Why?
- It is free.
- It does not rely on any external tool.
- Original and translated texts are bundled inside the same `.tex` file.


## How?
### Prerequisites
- I assume you know how to edit and produce LaTeX documents. If you don't, I recommend following [this online tutorial](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes). Once you get comfortable you can edit and compile LaTeX documents on your machine using a TeX distribution such as [MikTeX](https://miktex.org/).
- Translating text requires particular attention when it comes to modifications. 
  Although the suggested method allows to easily compare translated against original text, it does not track modifications. 
  Hence, it can become hard to edit already translated text.
  For this reason, I recommend using a version control system such as [git](https://git-scm.com/). 
  Although not necessary, it will save you a lot of time, especially for large projects.

### The method
The idea behind the method is that original and translated texts exist together (in the same file), and you get to decide which one to compile.

To reach this goal, the trick is to define a new command for each language at the very beginning of your project
```latex
\newcommand\en[1]{} % command for English language
\newcommand\fr[1]{} % command for French language
\newcommand\nl[1]{} % command for Dutch language
% etc.
 ```
and to use them everywhere translation is needed.
 ```latex
% ...
\section{\en{Tutorial}\fr{Tutoriel}\nl{Handleiding}}
\en{Welcome!}\fr{Bienvenue!}\nl{Welkom!}
% ...
 ```
 When you have finished editing your translations, the last step is to select the language for compilation. 
 This is done by inserting `#1` inside the command of your choice, and leave the others empty.
 ```latex
\newcommand\en[1]{}
\newcommand\fr[1]{#1} % document will be compiled in French 
\newcommand\nl[1]{} 
% etc.
 ```
In this example, all code inside the `\en{}` and `\nl{}` commands of your project will be ignored by the compiler. 
Only the code outside these commands and inside the `\fr{}` commands will be considered. The result is a french-only output. 

The same rule will apply if you select another language.
 ### Pro tips
 - Translate your project only when you have finished editing the original version, otherwise you will lose time translating text that will be modified or even removed later.
 - Some LaTeX packages depend on language. You can use the same trick to import them in one language or another.
 
	```latex
	% ...
	\en{
	\usepackage[english]{babel}
	}
	\fr{
	\usepackage[french]{babel}
	}
	\nl{
	\usepackage[dutch]{babel}
	}
	% ...
	```
	
	Same applies for material used in figures.
	
	```latex
	% ...
	\begin{figure}[h]
	\centering
	\includegraphics{\en{EN.png}\fr{FR.png}\nl{NL.png}}
	\caption{\en{Example}\fr{Exemple}\nl{Voorbeeld}}
	\label{fig:example}
	\end{figure}
	% ...
	```

 - Code that is common to all languages does not need be wrapped inside a language command, e.g. the `figure` environment above.
## The Future
In the future I aim to work on a GUI for easing translation of pieces of text.