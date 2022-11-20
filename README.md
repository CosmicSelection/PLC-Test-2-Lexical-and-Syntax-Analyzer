EBNF for my coding language
	includes lexeme names and syntax
	


Code -->    ~  <codeBlock> ~
codeBlock -->   { <assignment> | <selection> | <loop>}
assignment --> <variable> '=' (<variable>| <value>)';' <manipulation>
manipulation --> {<variable>=<equation>;}
selection -->{ 'OPTION'  (<bool>| 'Other') ':' [<codeBlock>]';'}
loop --> 'LOOP' <bool>  ':' {<codeBlock>} 'EXIT' (<bool>|<expr>)';' 
variable --> { _ | <letters>} 
bool --> <equation> ( <| >| <=| >=| ==) <equation>
equation -- > {<expr>| '(' <expr> ')' }
expr --> < term> { ( +| /)  <term>}
term --> <factor> {( *| -|%)  <factor>}
factor --> (<variable>|<value>)
value --> ( 0| 1| 2| 3| 4| 5| 6| 7| 8| 9){ 0| 1| 2| 3| 4| 5| 6| 7| 8| 9}<type>
type --> 'b'[ 2| 4| 8]
letters --> ( a| b| c| d| e| f| g| h| i| j| k| l| m| n| o| p| q| r| s| t| u| v| w| x| y| z)


	
LL Grammar
	No Left Hand Recursion:
    		direct or indirect
	pairwise disjointness test:
		Code --> first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z, OPTION, LOOP}
		codeBlock -->first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z}first{OPTION}first{LOOP}
		assignment --> first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z}
		manipulation --> first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z}
		selection --> first{OPTION}
		loop --> first{LOOP}
		variable --> first{ a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z}first{_}
		bool --> first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, (}
		equation -- > first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9,}first{(}
		expr --> first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9,}
		term --> first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9,}
		factor --> first{_, a , b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u ,v ,w, x, y, z}first{0, 1, 2, 3, 4, 5, 6, 7, 8, 9,}
		value --> first{0}first{1}first{2}first{3}first{4}first{5}first{6}first{7}first{8}first{9}
		type --> first{b}
		letters --> first{a}first{b}first{c}first{d}first{e}first{f}first{g}first{h}first{i}first{j}first{k}first{l}first{m}first{n}first{o}first{p}first{q}first{r}first{s}first{t}first{u}first{v}first{w}first{x}first{y}first{z}first{_}
	
	

4 Test Files
	2 Error Free
	1 with 5 lexical errors
		x4yzya- unrecognized variable with a number
		3$9b- number value with unrecgnized token
		x- variable too short to count as one
		2gb- number value with letter
		#- random unrecognized token
	1 with 6 syntax errors
		4253b4 = xzxser: value proceeds variable
		LOOP x_y_z_ < xzxser;- function ends with end of line character 		instead of function opening character
		OPTION x_y_z_ = 1b:- boolean contains an assignment character
		kvsfvf- uninitialized variable
		EXIT x_y_z_ = ;- unassigned value
				      
		
		
		
