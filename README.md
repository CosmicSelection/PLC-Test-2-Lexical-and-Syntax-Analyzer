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

LL Grammar:
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
