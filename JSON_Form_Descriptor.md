JSON Form Descriptor Specification
==================================


## Abstract

JSON Form descriptor is a JSON based format for defining the structure
of a `form`. The structure of a `form` provides a contract on how the
`form` should be interpreted for a given application. Form descriptor
is intended to define form's layout and fields.


## 1. Introduction

This specification describes `form` descriptor using JSON. A `form`
descriptor is a JSON data defining the structure of a `form`.
The structure of a `form` provides a contract on how the `form` should
be interpreted for a given application. Form descriptor is intended to
define form's layout and fields.

The goal of this specification is to provide metadata about a `form`
such that an application consumer of the descriptor can present
it in a rich human-friendly format. This may include constructing
visual representation of the `form`.

The basic properties that comprise the description of a `form` are
defined in the following sections. 


## 2. Notational Conventions

The text of this specification provides sole definition of
conformance. Examples in this specification are non-normative.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in [RFC2119].


## 3. JSON Serialization

A `form` descriptor is serialized using the JSON format, as defined in
[RFC4627]. Alternative serialization MAY be used but are outside of
this specification.

In its simplest structure, a `form` MUST consists of a `layout` and
a `fields`. A `layout`'s value is an `array` of pages. Each `page`
consists of an `array` of `row`. A `row` consists of an `array` of
`column`. A `column` consists of either an `array` of `field`'s key,
in JSON [RFC4627] String, or an `array` of `row`. Thus, a `column`
MAY forms nested rows/columns structure. A nested rows/columns
structure MUST ends in a `column` containing an `array` of `field`'s
key.

A `fields`'s value is an `object` consists of field's key / `field`
pairs. A `field` is an `object` whose properties are defined in the
following sections.

In the JSON serialization, absent properties MAY be presented by an
explicit declaration of the property whose value is `null` or by
omitting the property declaration; these two representations are
semantically equivalent. If a property is having a value whose type is
a JSON `array`, the absence of any items in that `array` MUST be
represented by omitting the property entirely or publishing it with
the value `null`, and MUST NOT be represented as an empty `array`,
except as otherwise stated in the definition of a specific property.


### 3.1 Example Form Descriptor

Following is a simple, minimal example of a `form` descriptor:

~~~
{
    "layout": [
        [ // 1st page
            [ // 1st row in 1st page
                [
                    // 1st col of 1st row in 1st page
                    "text_1", "text_2", "textarea_1"
                ]
            ]
        ]
    ],
    "fields": {
        "text_1": {
            "name": "Input text",
            "type": "text@large",
            "label": "Full Name",
            "description": "Your full name, accept alphanumeric",
            "validations": [
                {
                    "rule": "alphanumeric",
                    "message": "Only accept alphanumeric"
                },
                {
                    "rule": "between",
                    "params": [5, 20],
                    "message": "Min 5 chars, max 20 chars"
                }
            ]
        },
        "text_2": {
            "id": "email",
            "type": "text@medium",
            "name": "Input text",
            "label": "Email",
            "placeholder": "me@example.com"
            "description": "Your valid email address",
            "validations": [
                {
                    "rule": "email",
                    "message": "Invalid email address",
                    "foo": "some extension property"
                },
            ]
        },
        "textarea_1": {
            "label": "Address",
            "type": "textarea",
            "defaultValue": "LOUIS NEWTON\n455\nCALIFORNIA BELL",
            "foo2": "some other extension property"
        }
    }
}
~~~

The example above contains a number of required and optional core
properties plus additional extension properties "foo" and "foo2" for
illustrative purposes only.


### 3.2 Form Descriptor Serialization

### 3.2 Layout Serialization

### 3.3 Page Serialization

### 3.4 Container Serialization

### 3.5 Field Serialization


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
{ // fields
    field_key: { field },
    ...,
}
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
    [ // page-1
        [ // row-1
            [ // col-1-of-row-1
                'field_key',
            ],
            [ // col-2-of-row-1
                [ // row-1-of-col-2-of-row-1
                    // cols
                ]
            ],
        ],
        [ // row 2
            ...
        ],
        ...,
        [ // row n ]
    ],
    [ // page 2 ],
    ...
    [ // page n ]
]
~~~
