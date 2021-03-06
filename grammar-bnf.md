Turtle BNF
==========

From _Turtle - Terse RDF Triple Language_
W3C Candidate Recommendation 19 February 2013

http://www.w3.org/TR/2013/CR-turtle-20130219/#sec-grammar-grammar


       [1]  turtleDoc ::= statement*
       [2]  statement ::= directive | triples '.'
       [3]  directive ::= prefixID | base | sparqlPrefix | sparqlBase
       [4]  prefixID ::= '@prefix' PNAME_NS IRIREF '.'
       [5]  base ::= '@base' IRIREF '.'
       [5s] sparqlBase ::= "BASE" IRIREF
       [6s] sparqlPrefix ::= "PREFIX" PNAME_NS IRIREF
       [6]  triples ::= subject predicateObjectList | blankNodePropertyList predicateObjectList?
       [7]  predicateObjectList ::= verb objectList (';' (verb objectList)?)*
       [8]  objectList ::= object (',' object)*
       [9]  verb ::= predicate | 'a'
      [10]  subject ::= iri | BlankNode | collection
      [11]  predicate ::= iri
      [12]  object ::= iri | BlankNode | collection | blankNodePropertyList | literal
      [13]  literal ::= RDFLiteral | NumericLiteral | BooleanLiteral
      [14]  blankNodePropertyList ::= '[' predicateObjectList ']'
      [15]  collection ::= '(' object* ')'
      [16]  NumericLiteral ::= INTEGER | DECIMAL | DOUBLE
      [17]  String ::= STRING_LITERAL_QUOTE | STRING_LITERAL_SINGLE_QUOTE | STRING_LITERAL_LONG_SINGLE_QUOTE | STRING_LITERAL_LONG_QUOTE
    [128s]  RDFLiteral ::= String (LANGTAG | '^^' iri)?
    [133s]  BooleanLiteral ::= 'true' | 'false'
    [135s]  iri ::= IRIREF | PrefixedName
    [136s]  PrefixedName ::= PNAME_LN | PNAME_NS
    [137s]  BlankNode ::= BLANK_NODE_LABEL | ANON

