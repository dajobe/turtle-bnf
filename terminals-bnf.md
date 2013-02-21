Terminals Used by the grammar
=============================

	ANON  ::=  '[' WS* ']'
	BLANK_NODE_LABEL  ::=  '_:' BLANK_NODE_LABEL_START (BLANK_NODE_LABEL_MIDDLE* BLANK_NODE_LABEL_LAST)?
	BLANK_NODE_LABEL_START  ::=  PN_CHARS_U | [0-9]
	BLANK_NODE_LABEL_MIDDLE ::= PN_CHARS | '.'
	BLANK_NODE_LABEL_LAST   ::=  PN_CHARS
	DECIMAL  ::=  [+-]? [0-9]* '.' [0-9]+
	DOUBLE  ::=  [+-]? ([0-9]+ '.' [0-9]* EXPONENT | '.' [0-9]+ EXPONENT | [0-9]+ EXPONENT)
	INTEGER  ::=  [+-]? [0-9]+
	IRIREF  ::=  '<' ([^#x00-#x20<>\"{}|^`\] | UCHAR)* '>'
	LANGTAG  ::=  '@' [a-zA-Z]+ ('-' [a-zA-Z0-9]+)*
	PNAME_LN  ::=  PNAME_NS PN_LOCAL
	PNAME_NS  ::=  PN_PREFIX? ':'
	STRING_LITERAL_LONG_QUOTE  ::=  '"""' (('"' | '""')? [^"\] | ECHAR | UCHAR)* '"""'
	STRING_LITERAL_LONG_SINGLE_QUOTE  ::=  "'''" (("'" | "''")? [^'\] | ECHAR | UCHAR)* "'''"
	STRING_LITERAL_QUOTE  ::=  '"' ([^#x22#x5C#xA#xD] | ECHAR | UCHAR)* '"'
	STRING_LITERAL_SINGLE_QUOTE  ::=  "'" ([^#x27#x5C#xA#xD] | ECHAR | UCHAR)* "'"

Terminals Only used inside terminals
====================================

	EXPONENT  ::=  [eE] [+-]? [0-9]+
	UCHAR  ::=  '\u' HEX HEX HEX HEX | '\U' HEX HEX HEX HEX HEX HEX HEX HEX
	  case sensitive
	ECHAR  ::=  '\' [tbnrf\"']
	  case sensitive
	WS  ::=  #x20 | #x9 | #xD | #xA
	PN_CHARS_BASE  ::=  [A-Z] | [a-z] | [#x00C0-#x00D6] | [#x00D8-#x00F6] | [#x00F8-#x02FF] | [#x0370-#x037D] | [#x037F-#x1FFF] | [#x200C-#x200D] | [#x2070-#x218F] | [#x2C00-#x2FEF] | [#x3001-#xD7FF] | [#xF900-#xFDCF] | [#xFDF0-#xFFFD] | [#x10000-#xEFFFF]
	PN_CHARS_U  ::=  PN_CHARS_BASE | '_'
	PN_CHARS  ::=  PN_CHARS_U | '-' | [0-9] | #x00B7 | [#x0300-#x036F] | [#x203F-#x2040]
	PN_PREFIX        ::=  PN_PREFIX_START (PN_PREFIX_MIDDLE* PN_PREFIX_LAST)?
	PN_PREFIX_START  ::=  PN_CHARS_BASE
	PN_PREFIX_MIDDLE ::=  PN_CHARS | '.'
	PN_PREFIX_LAST   ::=  PN_CHARS
	PN_LOCAL        ::= PN_LOCAL_START (PN_LOCAL_MIDDLE* PN_LOCAL_LAST)?
	PN_LOCAL_START  ::= PN_CHARS_U | ':' | [0-9] | PLX
	PN_LOCAL_MIDDLE ::= PN_CHARS | '.' | ':' | PLX
	PN_LOCAL_LAST   ::= PN_CHARS | ':' | PLX
	PLX  ::=  '%' HEX HEX | '\' ('_' | '~' | '.' | '-' | '!' | '$' | '&' | "'" | '(' | ')' | '*' | '+' | ',' | ';' | '=' | '/' | '?' | '#' | '@' | '%')
	HEX  ::=  [0-9] | [A-F] | [a-f]