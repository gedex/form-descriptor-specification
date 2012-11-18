Form Descriptor Specification
=============================


## Abstract

Form descriptor is a JSON based format for defining the structure of a `form`.
The structure of a `form` provides a contract on how the `form` should be
interpreted for a given application. Form descriptor

## 1. Introduction

This specification describes `form` descriptor using JSON. A `form` descriptor
is a JSON data defining 

In its simplest form, a form builder consists of a `layout` and a `schema`. A `layout` tells
how the form's layout should be rendered and a `schema` tells the fields, along with
theirs properties, to render in given layout. Hence, it's REQUIRED to tell relationship
between `layout` and `schema` by using the same field's key.

It is a goal of this specification to provide sufficient metadata about a form such that a 
consumer of the format can represent it to a user in rich form (typically in html).

The basic properties that comprimise the description of `layout` and `schema` are defined
in the following sections.

Within this specification, a `layout` is an `array` consists of `array` of pages. Each page
consists of `array` of rows and each row consists of `array` of columns. Each column MAY
contain either `array` of row or `array` of field keys.

Within this specification, a `schema` is an `array` of pages. Each page consists of
field_keys/field_attributes pairs. A field key MUST BE unique across pages. A field attribute
is an `object` describing a field.

The terms `object` and `array` come from conventions of JavaScript.


## 2. Notational Conventions

The text of this specification provides sole definition of conformance. Examples in this
specification are non-normative.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT",
"RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in
[RFC2119].

## 3. 


## Workspace for Form Builder

A workspace for a form consists at least one page with at least one row and one column.
~~~
	------------------------------
	| This is workspace area     |
	| -------------------------- |
	| | 1st row                | |
	| | ---------------------- | |
	| | | 1st col in 1st row | | |
	| | ---------------------- | |
	| -------------------------- |
	------------------------------
~~~

Rows grow vertically (up to down) while columns in a row grow horizontally (left to right).
A column MAY contains row(s).


A workspace contains at least one page.

~~~
	------------------------------
	| This is workspace area     |
	| # 1st page                 |
	| -------------------------- |
	| | 1st row                | |
	| | ---------------------- | |
	| | | 1st col in 1st row | | |
	| | ---------------------- | |
	| -------------------------- |
	| -------------------------- |
	| # 2nd page                 |
	| -------------------------- |
	| | 1st row                | |
	| | ---------------------- | |
	| | | 1st col in 1st row | | |
	| | ---------------------- | |
	| -------------------------- |
	------------------------------
~~~



~~~
[ // pages
	{ // page 1
		field_1_key: { field_1 },
		field_2_key: { field_2 },
		...,
		field_n_key: {field_n}
	},
	{ // page 2 },
	...
	{ // page n }
]
~~~


Field schema:
~~~
{
	'type': 'field_type',
	'field_name': 'field_type_n'
	'required': true|false,
	'rule': [ { rule_1 }, { rule_2 }, ..., { rule_n } ],
	'label': 'field_label',
	'description': 'field_description'
}
~~~


Field's rule schema:
~~~
{
	[
		{
		  // rule 1
		},
		{ // rule 2 },
		...
		{ // rule n }
	]
}
~~~
Please note that first rule will be injected with following key, iff the field is required:
~~~
	'allowEmpty': true|false, // implicitly set to false when 'required' is true
~~~


Form layout schema:
~~~
[ // pages
	[ // page 1
		'col_name_for_field_1', 'col_name_for_field_2', ..., 'col_name_for_field_n'
	],
	[ // page 2 ],
	...
	[ // page n ]
]
~~~
