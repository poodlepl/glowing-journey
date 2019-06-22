#FILE 	: 	grammar.cfg

#### Input format for newpgl

1. Comments:
..1. Single Line Comments : ??
..2. Multi Line Comments  : /* */

# expression Rules:

#### primary-expression
	identifier
	constant
	string literal

#### postfix-expression
	primary-expression
	postfix-expression [expression]
	postfix-expression ( )
	postfix-expression ( argument-expression-list)
	postfix-expression . identifier
	postfix-expression -> identifier
	postfix-expression pp  									(pp ==  ++)
	postfix-expression mm									(mm ==  --)

#### argument-expression-list
	assignment-expression
	argument-expression-list , assignment-expression

#### unary-expression 
	postfix-expression
	pp unary-expression
	mm unary-expression
	unary-operator cast-expression
	SO unary-expression 									(SO == sizeof)
	SO ( type-name )

#### unary-operator
	&
	mul  													( mul == *)
	add 													( add == +)
	sub 													( sub == -)
	~
	not 													( not == !)

#### cast-expression
	unary-expression
	( type-name ) cast-expression

#### multiplicative-expression
	cast-expression
	multiplicative-expression mul cast-expression
	multiplicative-expression div cast-expression
	multiplicative-expression mod cast-expression

#### additive-expression
	multiplicative-expression
	additive-expression add multiplicative-expression
	additive-expression sub multiplicative-expression

#### shift-expression
	additive-expression
	shift-expression << additive-expression
	shift-expression >> additive-expression

#### relational-expression
	shift-expression
	relational-expression lt shift-expression 				(lt == <)
	relational-expression gt shift-expression 				(gt == >)
	relational-expression lte shift-expression 				(lte == <=)
	relational-expression gte shift-expression 				(gte == >=)

#### equality-expression
	relational-expression
	equality-expression eqeq relational-expression			(eqeq == "==")
	equality-expression neq relational-expression			(neq == "!=")

#### AND-expression
	equality-expression
	AND-expression & equality-expression

#### exclusive-OR-expression
	AND-expression
	exclusive-OR-expression ^ AND-expression

#### inclusive-OR-expression
	exclusive-OR-expression
	inclusive-OR-expression | exclusive-OR-expression

#### logical-AND-expression
	inclusive-OR-expression
	logical-AND-expression && inclusive-OR-expression

#### logical-OR-expression
	logical-AND-expression
	logical-OR-expression || logical-AND-expression

#### conditional-expression
	logical-OR-expression
	logical-OR-expression ? expression : conditional-expression

#### assignment-expression
	conditional-expression
	unary-expression assignment-operator assignment-expression

#### assignment-operator
	eq 															(eq == "=")

	/* PLEASE DO THIS LATER */

#### expression
	assignment-expression
	expression , assignment-expression

#### constant-expression
	conditional-expression

#
# DECLARATION RULES
#

#### declaration
	declaration-specifiers
	declaration-specifiers init-declarator-list

#### declaration-specifiers
	storage-class-specifier
	type-specifier
	type-qualifier
	storage-class-specifier declaration-specifiers
	type-specifier 			declaration-specifiers
	type-qualifier			declaration-specifiers

#### init-declarator-list
	init-declarator
	init-declarator-list , init-declarator

#### init-declarator
	declarator
	declarator eq initializer

#### storage-class-specifier
	typedef
	extern
	static
	auto
	register

#### type-specifier
	void
	char
	short
	int
	long
	float
	double
	signed
	unsigned
	struct-or-union-specifier
	enum-specifier
	typedef-name

#### struct-or-union-specifier
	struct-or-union { struct-declaration-list }
	struct-or-union identifier { struct-declaration-list }
	struct-or-union identifier

#### struct-or-union
	struct
	union

#### struct-declaration-list
	struct-declaration
	struct-declaration-list struct-declaration

#### struct-declaration
	specifier-qualifier-list struct-declarator-list

#### specifier-qualifier-list
	type-specifier
	type-qualifier
	type-specifier specifier-qualifier-list
	type-qualifier specifier-qualifier-list

#### struct-declarator-list
	struct-declarator
	struct-declarator-list , struct-declarator

#### struct-declarator
	declarator
	constant-expression
	declarator constant-expression

#### enum-specifier
	enum { enumerator-list }
	enum identifier { enumerator-list }
	enum identifier

#### enumerator-list
	enumerator
	enumerator-list , enumerator

#### enumerator
	enumeration-constant
	enumeration-constant eq constant-expression

#### enumeration-constant
	identifier

#### type-qualifier
	const
	volatile

#### declarator
	direct-declarator
	point direct-declarator

#### direct-declarator
	identifier
	( declarator )
	direct-declarator [ constant-expression ]
	direct-declarator ( )
	direct-declarator ( parameter-type-list )
	direct-declarator ( identifier-list )

#### pointer
	* 
	* pointer
	* type-qualifier-list
	* type-qualifier-list pointer

#### type-qualifier-list
	type-qualifier
	type-qualifier-list type-qualifier

#### parameter-type-list
    parameter-list
    parameter-list , ...

####parameter-list
    parameter-declaration
    parameter-list , parameter-declaration

####parameter-declaration
    declaration-specifiers declarator
    declaration-specifiers
    declaration-specifiers abstract-declarator

#### identifier-list
    identifier
    identifier-list , identifier

####type-name
    specifier-qualifier-list
    specifier-qualifier-list abstract-declarator

#### abstract-declarator
    pointer
    direct-abstract-declarator
    pointer direct-abstract-declarator

#### direct-abstract-declarator
    ( abstract-declarator )
    [ ]
    [ constant-expression ]
    ( )
    ( parameter-type-list )
    direct-abstract-declarator [ ]
    direct-abstract-declarator [ constant-expression ]
    direct-abstract-declarator ( )
    direct-abstract-declarator ( parameter-type-list )

#### typedef-name
    identifier

#### initializer
    assignment-expression
    { initializer-list }
    { initializer-list , }

#### initializer-list
    initializer
    initializer-list , initializer

# STATEMENT RULES

