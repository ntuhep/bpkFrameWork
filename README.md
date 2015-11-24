# bpkFrameWork

The bpkFrameWork is a dummy repository that is used to sync all of the bprimeKit related packages to be deployed in a CMSSW environment, they are:

   * [bprimeKit](https://github.com/ntuhep/bprimeKit): A standalone package for producing bprimeKit flavoured n-tuples.
   * [bpkUtility](https://github.com/ntuhep/bpkUtility): Various utility functions/classes and scripts for using and maintaining the bprimeKit main package.
   * [bpkHitFit](https://github.com/ntuhep/bpkHitFit)
   * [bpkHitFitAnalysis](https://github.com/ntuhep/bpkHitFitAnalysis)


The below are notes for the package maintainers.


## Structural Design

Do NOT keep source code in this repository! Source code must be store in the different repositories under the following philosophy:

   * The [bprimeKit](https://github.com/ntuhep/bprimeKit) repository should be a minimal standalone package for testing and production. Nothing more, nothing less.
   * The [bpkUtility](https://github.com/ntuhep/bpkUtility) includes three main functionalities:
      + Example code for using the bprimeKit ntuples 
      + Maintanance code for handling the large header files required by the bprimeKit code 
      + Helper classes for using the bprimeKit code (eventSelector and objectSelector)
      Due to this decision, the bpkUtility package should have redundant files that my or may not be out of sync with the bprimeKit main package, it is up to the maintainer to ensure that the correct files are used.


## Package structure:

In each of the packages that interface with the CMSSW environment, the maintainers are encouraged to follow the following rules:
   * The `interface` directory should include all header files of the package. 
   * The `plugins` directory should only contain the source code of the EDM-Plugins classes
   * The `src` directory should include all other source code such as helper classes, additional functions etc
   * Write a separate `BuildFile.xml` for the `plugins` and `src` directories.
   * A `test` directory with a minimal working configuration files with a additional README listing all the input options.

## Performance issues:
For performance issue we will say that as of 2015-11-20, avoid using global variables static or otherwise in your code.
It is know to mess with crab 3 jobs since it might spawn multiple instances of your plugin class. The only exception would be constant global variables


## Code style:
We are only going to specify the naming scheme that should be kept throughout the packages: namely
the [Taligent Rules](https://root.cern.ch/TaligentDocs/TaligentOnline/DocumentRoot/1.0/Docs/books/WM/WM_63.html#HEADING77):

   * User defined data member begin with `f` such as `fMuonList`
   * User defined method member must being with capital such as `IsGoodMuon()`
   * Local objects should be begin with lower-case letters
   * `edm::Handle` objects will be postfixed with `_H`

We do not wish to enforce too many concrete coding styles, but here are some general recommendations commonly neglected by physicists:

   * *Restrain from copy and paste code from outside*: Find if a functionality is provided by a CMSSW function or another package, use that function! Don't try and implement it yourself. 
   * *Do NOT copy and paste code within the packages*: If you are NOT certain that some section will be used only once, write it into a function! (or a class if it requires many variables)
   * *Keep small parenthesis`()` small* : Parenthesis should not span more than two lines, long conditions write a boolean function for a wrapper. 
   * *Keep large parenthesis`{}` small* : A rule of thumb is that any scope should not span for than two pages on your editor. Try splitting statement blocks into functions.
   * *Keep the indention count small*: Multiple nested scopes is difficult to read, avoid monotonous nested `if` statements, and functions and recursion for complicated loops.
   * *Keep files small* Large files are annoying to open, difficult to read, laggy to edit and difficult to track differences. Split function by similarity into different files.
   * *Keep comments small* The best comment is not comment. If you need a big block of comments explaining what your code does, then your code should be cleaned up. Keep comments bite sized and for labeling sections of logics and for documentation
   * *Use common sense* Before you jump into writing code, think about how to layout your code so that it is clear for your and other to read.


