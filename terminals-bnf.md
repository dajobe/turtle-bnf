Turtle / SPARQL Terminals Used by the grammar
=============================================

    ANON                    ::= '[' WS* ']'
    BLANK_NODE_LABEL        ::= '_:' BN_LABEL
    DECIMAL                 ::= [+-]? [0-9]* '.' [0-9]+
    DOUBLE                  ::= [+-]? ([0-9]+ '.' [0-9]* EXPONENT | '.' [0-9]+ EXPONENT | [0-9]+ EXPONENT)
    INTEGER                 ::= [+-]? [0-9]+
    IRIREF                  ::= '<' ([^#x00-#x20<>\"{}|^`\] | UCHAR)* '>'
    LANGTAG                 ::= '@' [a-zA-Z]+ ('-' [a-zA-Z0-9]+)*
    PNAME_LN                ::= PNAME_NS PN_LOCAL
    PNAME_NS                ::= PN_PREFIX? ':'
    STRING_LITERAL_LONG_QUOTE        ::= '"""' (('"' | '""')? [^"\] | ECHAR | UCHAR)* '"""'
    STRING_LITERAL_LONG_SINGLE_QUOTE ::= "'''" (("'" | "''")? [^'\] | ECHAR | UCHAR)* "'''"
    STRING_LITERAL_QUOTE             ::= '"' ([^#x22#x5C#xA#xD] | ECHAR | UCHAR)* '"'
    STRING_LITERAL_SINGLE_QUOTE      ::= "'" ([^#x27#x5C#xA#xD] | ECHAR | UCHAR)* "'"

Where

  * #x22 = " (double quote)
  * #x22 = ' (single quote)
  * #x5C = \


Turtle / SPARQL Terminals Only used inside terminals
====================================================

    EXPONENT         ::= [eE] [+-]? [0-9]+
    UCHAR            ::= '\u' HEX HEX HEX HEX | '\U' HEX HEX HEX HEX HEX HEX HEX HEX
      case sensitive
    ECHAR            ::= '\' [tbnrf\"']
      case sensitive
    WS               ::= #x20 | #x9 | #xD | #xA
    PN_CHARS_BASE    ::= [A-Z] | [a-z] | [#x00C0-#x00D6] | [#x00D8-#x00F6] | [#x00F8-#x02FF] | [#x0370-#x037D] | [#x037F-#x1FFF] | [#x200C-#x200D] | [#x2070-#x218F] | [#x2C00-#x2FEF] | [#x3001-#xD7FF] | [#xF900-#xFDCF] | [#xFDF0-#xFFFD] | [#x10000-#xEFFFF]
    PN_CHARS         ::= PN_CHARS_BASE | '_' | '-' | [0-9] | #x00B7 | [#x0300-#x036F] | [#x203F-#x2040]
    PLX              ::= '%' HEX HEX | '\' ('_' | '~' | '.' | '-' | '!' | '$' | '&' | "'" | '(' | ')' | '*' | '+' | ',' | ';' | '=' | '/' | '?' | '#' | '@' | '%')
    HEX              ::= [0-9] | [A-F] | [a-f]

Turtle / SPARQL Blank node Name
-------------------------------

    BN_LABEL         ::= BN_LABEL_START (BN_LABEL_MIDDLE* BN_LABEL_LAST)?
    BN_LABEL_START   ::= PN_CHARS_BASE | '_' | [0-9]
    BN_LABEL_MIDDLE  ::= PN_CHARS | '.'
    BN_LABEL_LAST    ::= PN_CHARS

Turtle / SPARQL Prefixed Name
-----------------------------

    PN_PREFIX        ::= PN_PREFIX_START (PN_PREFIX_MIDDLE* PN_PREFIX_LAST)?
    PN_PREFIX_START  ::= PN_CHARS_BASE
    PN_PREFIX_MIDDLE ::= PN_CHARS | '.'
    PN_PREFIX_LAST   ::= PN_CHARS

Turtle / SPARQL Local Name
--------------------------

    PN_LOCAL         ::= PN_LOCAL_START (PN_LOCAL_MIDDLE* PN_LOCAL_LAST)?
    PN_LOCAL_START   ::= PN_CHARS_BASE | '_' | [0-9] | ':' | PLX
    PN_LOCAL_MIDDLE  ::= PN_CHARS | '.' | ':' | PLX
    PN_LOCAL_LAST    ::= PN_CHARS | ':' | PLX

XML 1.1 QNames
--------------

    XML_NAME   ::= XML_START (XML_MIDDLE* XML_LAST)?
    XML_START  ::= PN_CHARS_BASE | '_'
    XML_MIDDLE ::= PN_CHARS | '.'
    XML_LAST   ::= PN_CHARS | '.'

SPARQL 1.1 Variable Name
------------------------

http://www.w3.org/TR/2012/PR-sparql11-query-20121108/#rVARNAME

    VARNAME       ::= VARNAME_START VARNAME_REST*
    VARNAME_START ::= PN_CHARS_BASE | '_' | [0-9]
    VARNAME_REST  ::= PN_CHARS EXCLUDING '-'


General name checking rules
---------------------------

Default (Prefixed Name)
   * Start: *PN_CHARS_BASE*
   * Middle: *PN_CHARS* | '.' (same as XML namechar)
   * Last: *PN_CHARS*

Flags:
   1. Allow _ and [0-9] at start (Blank node Name; Local Name)
   2. Allow ':' and hex and '\'+escapes everywhere (Local Name)
   3. Allow '.' at end (XML QName)
   4. Forbid '-' at middle and end (SPARQL Variable Name)
   
