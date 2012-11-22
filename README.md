Form Descriptor Specification
=============================

Form Descriptor is a proposed specification defining the structure of a
form using various format. The format can be consumed by application to
render a form in a human-friendly visualization such as html's forms or
form in a native-UI mobile application.

## Overview

Let's say you build a drag-and-drop form builder. Your app provides a set
of fields in toolbox to be dragged into workspace in which user get
preview of rendered form. The app expands by allowing the form exported
into desktop and mobile forms. This form descriptor can be used as a
exported files that will be imported in desktop and mobile apps.

In any apps, the layout form is viewed as a pages consist of rows and
columns. The specification states that the most nested columns MUST be
an input field.

~~~
    -------------------------------------
    | # Form                            | layout: [
    | # 1st page                        |   [ // 1st page
    | --------------------------------- |
    | | # 1st row                     | |     [ // 1st row
    | | ----------------------------- | |
    | | | # 1st col    |  # 2nd col | | |       [ "field_text_1" ], // 1st col
    | | ----------------------------- | |       [ "textarea_1" ] // 2nd col
    | | | field_text_1 | textarea_1 | | |
    | | ----------------------------- | |     ]
    | --------------------------------- |   ]
    ------------------------------------- ]
~~~

The "field_text_1" and "textarea_1" fields must be defined in `fields`
as the specification describes. The defined properties include name of
the field, validation rules, default value, or your own specific property
that's understandable by your own app.

## Specifications

* [JSON Form Descriptor](#)
* [YAML Form Descriptor](#)
* [XML Form Descriptor](#)

## In this repo:

* README.md &mdash; You're reading it now
* JSON_Form_Descriptor.md &mdash; JSON Form Descriptor Specification
* YAML_Form_Descriptor.md &mdash; YAML Form Descriptor Specification
* XML_Form_Descriptor.md &mdash; XML Form Descriptor Specification
* IMPLEMENTATIONS.md &mdash; A library/framework/app implementing or
  demonstrating Form Descriptor specification.
* schema
  * README.md &mdash; Information about schema
