Dynamic Form JSON Schema
========================

This document contains dynamic fields schema stored in JSON.
~~~
[ // pages
	[ // page 1
		{ field_1 }, { field_2 }, ..., {field_n}
	],
	[ // page 2 ],
	...
	[ // page n ]
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
