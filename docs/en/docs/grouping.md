---
title: Layers for Grouping
description: Learn how to use Laravel Orchid's layer functionality to group and organize your administration application's pages and functionality for improved navigation and usability. Explore the benefits of using layers in your Orchid project.
---


## Split 

Allows you to divide the screen into two customizable sections. 
This layout is particularly useful when you want to display two separate pieces of information side-by-side.

Orchid provides a shortcut method for creating a Split layout with two views using the `Layout::split()` method. 
To create a Split layout, simply pass an array of two Layout objects as the first parameter to the `split()` method. 
You can also set the ratio of the two sections using the optional `ratio()` method as the second parameter.

Here's an example of how to create a Split layout:

```php
use Orchid\Support\Facades\Layout;

Layout::split([
    Layout::view('first-view'),
    Layout::view('second-view'),
]);
```

### Customizing the Ratio

By default, the Split layout divides the screen with a `50/50` ratio. However, you can easily customize this ratio using the `ratio()` method. 
This method takes a string argument that specifies the desired ratio. Here are the valid ratios:

- 20/80
- 30/70
- 40/60
- 50/50
- 60/40
- 70/30
- 80/20

For example, to create a `Split` layout with a `40/60` ratio:

```php
use Orchid\Support\Facades\Layout;

Layout::split([
    Layout::view('first-view'),
    Layout::view('second-view'),
])->ratio('40/60'),
```


### Reversing the Order on Mobile

By default, the order of the two sections in a `Split` layout is fixed. 
However, you can reverse the order of the sections on mobile devices by calling the `reverseOnPhone()` method. Here's an example:

```php
use Orchid\Support\Facades\Layout;

Layout::split([
    Layout::view('first-view'),
    Layout::view('second-view'),
])->ratio('40/60')->reverseOnPhone(),
```

This will create a `Split` layout with a `40/60` ratio, and the order of the sections will be reversed on mobile devices.


## Columns

Columns are useful when you want to group content horizontally. They allow you to divide the layout into multiple columns of equal width, which can be used to display content side by side.

> Columns differ from `Split` in that they always have the same width and there can be many of them.

Here is an example of columns:

![Columns](/img/layouts/columns.png)

To create columns in Orchid, you can use the `Layout::columns()` method. This method accepts an array of content, which will be displayed in the columns.

Here is an example of how to create columns using the short syntax:

```php
use Orchid\Support\Facades\Layout;

public function layout(): array
{
    return [
        Layout::columns([
           TableExample::class,
           RowExample::class,
        ]),
    ];
}
```

In the example above, the layout is divided into two columns, and the content of each column is specified as the lowercase name of a class.

## Tabs

Tabs group content and help with navigation. Useful when you want to switch between hiding and displaying a some of content:

![Tabs](/img/layouts/tabs.png)

Tabs support short syntax by calling a static method,
which does not require creating a separate class:

```php
use Orchid\Support\Facades\Layout;

public function layout(): array
{
    return [
        Layout::tabs([
            'Personal Information' => [
                Layout::rows([
                    Input::make('user.name')
                        ->type('text')
                        ->required()
                        ->title('Name')
                        ->placeholder('Name'),

                    Input::make('user.email')
                        ->type('email')
                        ->required()
                        ->title('Email')
                        ->placeholder('Email'),
                ]),
            ],
            'Billing Address'      => [
                Layout::rows([
                    Input::make('address')
                        ->type('text')
                        ->required(),
                ]),
            ],
        ]),
    ];
}
```

Keys will be used as headers.

Please note that you can specify the lowercase name of the class as values:

```php
public function layout(): array
{
    return [
        Layout::tabs([
            'Personal Information' => PersonalInformationRow::class,
            'Billing Address'      => BillingAddressRow::class,
        ]),
    ];
}
```

By default, the active tab will be either the first or the last active one. 
If you need to define the active tab explicitly, you can do this using the `->activeTab($key)` method

```php
public function layout(): array
{
    return [
        Layout::tabs([
            'Personal Information' => PersonalInformationRow::class,
            'Billing Address'      => BillingAddressRow::class,
        ])->activeTab('Billing Address'),
    ];
}
```

## Accordion

Accordions are useful when you want to switch between hiding and displaying a lot of content in a compact space. They consist of a series of collapsible panels, each containing a header and content. When a panel is expanded, its content becomes visible, while the other panels are collapsed.

Here is an example of an accordion:

![Accordion](/img/layouts/accordion.png)

To create an accordion in Orchid, you can use the `Layout::accordion()` method. This method accepts an array of panel names and content, where the keys of the array will be used as the panel headers and the values will be used as the panel content.

Here is an example of how to create an accordion using the short syntax:



```php
use Orchid\Support\Facades\Layout;

public function layout(): array
{
    return [
        Layout::accordion([
            'Personal Information' => [
                Layout::rows([
                    Input::make('user.name')
                        ->type('text')
                        ->required()
                        ->title('Name')
                        ->placeholder('Name'),

                    Input::make('user.email')
                        ->type('email')
                        ->required()
                        ->title('Email')
                        ->placeholder('Email'),
                ]),
            ],
            'Billing Address'      => [
                Layout::rows([
                    Input::make('address')
                        ->type('text')
                        ->required(),
                ]),
            ],
        ]),
    ];
}
```

In the example above, the accordion has two panels: "Personal Information" and "Billing Address". The content of each panel is specified as an array of rows created using the `Layout::rows()` method.

You can also specify the content of each panel as the lowercase name of a class that returns an array of rows:

```php
public function layout(): array
{
    return [
        Layout::accordion([
            'Personal Information' => PersonalInformationRow::class,
            'Billing Address'      => BillingAddressRow::class,
        ]),
    ];
}
```
