# MathGene
The JavaScript Open Source symbolic math calculation and rendering engine!

MathGene is a comprehensive JavaScript mathematics engine that delivers the power to perform advanced numerical 
and symbolic mathematics processing of LaTeX expressions and send the output to pure HTML for rendering publishing quality 
mathematics on a conventional web browser. 

MathGene has two modules:
- mg_translate.js, which translates between LaTeX, HTML, and native MG format.
- mg_calculate.js, which performs the calculations.

mg_translate.js can be used without mg_calculate.js to perform mathematics rendering only.
Both modules are required to perform calculations.


## MathGene Requirements

MathGene supports the following browsers, mobile devices, and Javascript engines:
- FireFox version 8 or higher (Windows, Mac, Linux)
- Google Chrome version 10 or higher (Windows, Mac, Linux, Android)
- Internet Explorer version 10 or higher (Windows)
- Safari version 5 or higher (Mac)
- Node.js 4.6
- Apple iPhone 3+
- Apple iPad 2+
- Android 4.3+

No additional modules, fonts, or privileges are required to run MathGene.


## MathGene JavaScript

MathGene is implemented entirely in JavaScript conforming to ECMAscript ECMA-262, edition 5.1. 

It is intended as either a client-side math processing engine for websites or a server-side/command-line driven engine for general purpose usage.

MathGene utilizes an unconventional 'lexical' design which exploits the unique characteristics of JavaScript to enable fast and compact algorithms
for translation and computation. For example, the entire derivative engine is a little over 100 lines of code.

MathGene does not incorporate any 3rd party code or algorithms outside of conventional math techniques.

Use the followng HTML statements to load MathGene into a web page (view file 'web_demo.html' for usage):

	<script type="text/javascript" src="mg_translate.js"></script>
	<script type="text/javascript" src="mg_calculate.js"></script>

MathGene is compatible with Node.js version 4.6 for server-side implementations. 

MathGene requires no additional Node.js modules and can be used with Node.js as a complete math processing engine.

The file node_demo.js shows the basic Node.js MathGene implementation.

To run the Node.js demo:

	node node_demo.js
	
For Node.js, use the following statements to link MathGene modules (view file 'node_demo.js' for usage):

	var translate = module.require('./mg_translate.js')
	var calculate = module.require('./mg_calculate.js')


## MathGene and Browsers

MathGene supports any modern browser that implements ECMAscript(JavaScript) ECMA-262, edition 5.1 and the Extended HTML Character Set.

Older browsers may or may not function correctly. 

- Internet Explorer versions 10 and 11 have been tested and verified. IE versions prior to version 10 will not operate properly with MathGene.
- Firefox has been tested back to version 8.
- Google Chrome has been tested back to version 10.
- Apple Safari has been tested back to version 5. 

There is some browser variablility in the implementation of math fonts in the Extended Character Set. HTML rendered math will not look identical on different
browsers but the differences are typically marginal. Some older browsers, particularly mobile browsers, 
may be missing some extended HTML symbols which will then render as blank squares.

There is also variablitiy in the implementation of IEEE754-2008 numeric math within different browsers. In some cases, integers are rendered as x.99999997 or similar.
There will be variablitiy in decimal rounding for different JavaScript engines. This will be typically in the 8+ decimal place. The Numeric test suite rounds all
tests to 8 decimal places to compensate for the different numeric rounding behavior.

Javascript performance varies quite significanly between browsers. Chrome and IE are the fastest while Firefox appears about 50% slower in math computations. 
HTML math rendering performance is good on all tested browsers. Mobile devices are typically far slower at calculations than desktops, 
particularly with advanced symbolic math such as evaluating integrals. Math rendering is fast on all supported mobile devices.


## MathGene LaTeX

MathGene will input and output expressions in LaTeX format for both translation and computation.
LaTeX is a computer mathematics publishing language that is also used for computer algebra systems.

LaTeX references can be found at these links:
- https://en.wikibooks.org/wiki/LaTeX/Mathematics
- https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols

MathGene supports a large subset of LaTeX symbols and operators. MathGene will input and output expressions formatted in LaTeX using conventional math notation.
Real numbers, complex numbers, constants, variables, and matrices are supported.

These exceptions apply to MathGene LaTeX:
- MathGene does not support LaTeX sizing features such as 'big'
- '\\usepackage' is not supported
- All matrix formats are converted to '{bmatrix}' at output
- {array} element is not supported
- Newline '\\\\' is currently not supported except in the matrix object
- all braces '{}' must be closed and terminated
- '/' slash divide symbol is always interpreted as equivalent to '\\frac'

MathGene follows these conventions:
- 'e' is interpreted as Euler's number (2.718...)
- '\\pi' is interpreted as Archimedes constant (3.14...)
- '\\imath' is interpreted as the imaginary constant 'i'
- d is interpreted as a differential when followed by a variable as in 'dx' or as in 'd/dx'
- some functions like arctanh(x), erf(x), etc. lack LaTeX equivalents so they are handled as if they do: \\arctanh \\erf
- all plain variables are italicized

Expressions are evaluated from left to right. Math operators have a precedence value that determines which operations are performed first.

Operator precedence from first to last:
- () → Operations inside parentheses and functions
- x^n → Exponents
- -x → Negative numbers: -4^2 = -(4^2)
- xN → Terms such as 2π: 2π/4<i>i</i> = (2π)/(4<i>i</i>)
- / → Divide
- × → Multiply
- +- → Add/Subtract

NOTE: 
	
	All inputs to MathGene are via Javascript strings. 
	Javascript strings must escape the LaTeX backslash with another backslash such as "\\pi".
	
	Conventional LaTeX without escaped strings can be inputed from a web page using the following HTML tag:
	<textarea id='textareaID'></textarea> 
	
	Use this JavaScript statement to assign the <textarea> data expression to a variable:
	texVar = document.getElementById('textareaID').value
	
	View file 'web_demo.html' for <textarea> LaTeX input examples.

Examples of valid LaTeX expressions as JavaScript strings:

	"\\frac {21}{b}"
	"\\sqrt{\\frac{\\zeta}{\\mu}-\\frac{\\pi}{\\beta}}" 
	"\\int_{1}^{2} \\sin\\left(x\\right) dx"
	"\\coth^{-1}{\\frac {x}{y}}"
	"\\begin{ bmatrix}a&b&c \\\\ \\frac{\\pi}{2}&d&e  \\end{bmatrix}^{2}"


## MathGene HTML

MathGene has the unique ability to render pure HTML math output from a LaTeX input expression. 
This has many advantages over the conventional image-based approach or MathML for web mathematics publishing:

Advangages:
- no image or font download, instant rendering using built-in HTML extended ASCII characters
- fast rendering on mobile devices
- fully scalable math rendering without pixelation, math stays razor sharp after zooming
- easy insertion into HTML documents
- simple and compact markup language compared to MathML
- compatible with all modern browsers and mobile devices
- Released under GPL. No fees or licensing!

The following function is used to render HTML output from the input expression string in either LaTeX or native MG format:
- mgTranslate(expression).html

Example of embedding MathGene HTML in a web page:

	<html>
	<head>
	<script type="text/javascript" src="mg_translate.js"></script>
	</head>
	<body>
	<p>Here is a matrix:</p>
	<script>document.write(mgTranslate("\\begin{ bmatrix}a&b&c \\\\ \\frac{\\pi}{2}&d&e  \\end{bmatrix}").html)</script>
	<p>Here is an integral:</p>
	<script>document.write(mgTranslate("\\int_{1}^{2} \\sin\\left(x\\right) dx").html)</script>
	</body>
	</html>


## MathGene Numeric Math

MathGene 'mgNumeric(expression)' function will compute the numeric decimal value of an input expression.

Numeric computations are performed via IEEE754-2008 64bit floating point math as implemented in JavaScript engine. 
This provides 16 decimal places of precision with exponents from -322 to +302 in standard scientific notation.
Decimal precision can be set by changing the mgConfig.dPrecision paramter in the range of 1-16 at runtime. 
Any number in excess of 10^12 or 10^-9 will be converted to scientific notation by default.

The input expression can contain constants, real numbers, fractions, complex numbers, or matrices in any legitimate expression.

Examples can be seen in the test suite under 'Numeric' and 'Matrix'.

- All uninitialized variables will be evaluated with a '0' value unless the variable value is set prior to the operation.
- The returned value of mgNumeric() is an object containing the three output formats LaTeX, HTML, and MG.
- To output a computation in LaTeX use: mgNumeric(expression).latex
- To output a computation in HTML use: mgNumeric(expression).html.

Examples:

	mgNumeric("\\frac{8-8 \\imath }{2+ \\imath }").latex    =>     "1.6-4.8 \\imath"
	mgNumeric("\\begin{bmatrix}3&4&2 \\end{bmatrix} \\times \\begin{bmatrix}13&9&7&15 \\\\8&7&4&6 \\\\6&4&0&3 \\end{bmatrix}").latex  =>  "\\begin{bmatrix}3&4&2 \\end{bmatrix} \\times \\begin{bmatrix}13&9&7&15 \\\\8&7&4&6 \\\\6&4&0&3\\end{bmatrix}"


## MathGene Symbolic Math

The following MathGene functions compute symbolic math:

- mgSimplfy(expression) - reduces the expression to simplest form, evaluates all calculus, limits, summations, reduces fractions, etc.
- mgSolve(equation,variable) - solve the equation for the specified variable
- mgSubstitute(expression,substTarget,substSource) - substitute the expression in substTarget (which is a term in expression) with substSource
- mgFactor(expression) - factor symbolically 
- mgExpand(expression) - inverse of mgFactor
- mgTrigToExp(expression) - converts trig and hyperbolic functions to exponential equivalents
- mgRange(expression) - returns range of expression
- mgDomain(expression) - returns domain of expression

The returned value of all the above functions is an object containing the three output formats LaTeX, HTML, and MG.

Conventions:
- negative exponents 'x^(-n)' are simplified to '1/x^n'
- x^(1/2) and x^(1/3) are simplified to square and cube roots
- (-x)/y is simplified to -(x/y)
- (x+y)/z is simplified to x/z+y/z

Examples:

	mgSimplify("\\int  \\sqrt{5+ \\sqrt{x}} d x").latex  =>  "\\frac{4 { \\sqrt{x}+5}^{ \\frac{3}{2}} \\sqrt{x}}{3}- \\frac{8 { \\sqrt{x}+5}^{ \\frac{5}{2}}}{15}+C"
	mgSolve("\\frac{1}{ \\sigma  \\sqrt{2 \\pi }} e^{ \\frac{- \\left(x-m \\right)^{2}}{2 \\sigma^{2}}}=p","m").latex  =>  "m=x- \\sqrt{-2 { \\sigma }^{2} \\ln {p \\sigma  \\sqrt{2 \\pi }}}"

## MathGene Configuration

The configuration object 'mgConfig' contains the following parameters which can be set at run time:

- mgConfig.trigBase		default = 1, 			trig base 1=radians. Math.pi/180 for degrees, Math.pi/200 gradians
- mgConfig.divScale		default = 85, 			default scale factor for x/y division in percent
- mgConfig.divSymbol	default = "Over", 		default HTML divide symbol "Slash" or "Over"
- mgConfig.fnFmt		default = "fn x", 		function format "fn(x)" or "fn x"
- mgConfig.invFmt		default = "asin", 		inverse trig function format "asin" or "sin<sup>-1</sup>"
- mgConfig.cplxFmt		default = "Rect", 		complex number format "Rect" or "Polar" 	
- mgConfig.pctFactor	default = 100, 			percent factor 100 for percent, 1 for n.nn decimal
- mgConfig.dPrecision	default = 16, 			decimal precision 1-16
- mgConfig.Domain		default = "Complex", 	number domain "Complex" or "Real"
- mgConfig.editMode		default = false, 		edit mode formatting
- mgConfig.htmlFont		default = "Times,Serif",default HTML font-family

Function style format in mgConfig.fnFmt can be in two styles "fn(x)" which is computer-style such as 'sin(xy)' or default "fn x" which is the conventional 'sin xy'.

Inverse trig function style format in mgConfig.fnFmt can be either "asin" for 'asin x' or "sin<sup>-1</sup>" for 'sin^-1 x'.


## MathGene Tests

MathGene has an extensive test suite containing over 1400 individual tests that cover both translations and computations.
The test suite provides use cases for each of the MathGene functions as well as test coverage. 
Tests can be run either command-line via Node.js or via browser using a web interface.

To run the test suite via command-line (Node.js required, typical runtime 100 seconds):
	
	node mg_tests.js

To run the web interface, load the file 'test_suite.html' into a supported web browser.


## MathGene in Action

The website http://calcinator.com implements the full MathGene engine for both rendering and computation.

Calcinator is a mobile-friendly set of specialized math applets for use on both desktop and mobile devices.


## About the Author

MathGene was designed by George J. Paulos, a US-based Software Engineer and "JavaScript Junkie" who has a keen interest in mathematics and math education.
The MathGene project was initially just a hobby calculator project intended to learn Javascript and mobile web programming while brushing up on college math.
Over several years the project evolved into a full-function mathematics engine which is now released to the Open Source community under the GPL license.


## Future Enhancements

The following is a (slightly) prioritized list of desired enhancements.

- Statistical functions
- Advanced matrix functions
- Deeper LaTeX support
- Arbitrary precision arithmetic
- Differential equations
- Real and complex roots
- Inequalities
- Vectors
- Tensors
- Line and contour integrals


## MathGene GPL Licensing

Copyright (C) 2016  George J. Paulos

MathGene is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
any later version.

MathGene is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.


