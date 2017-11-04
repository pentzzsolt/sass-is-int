# sass-is-int

A lightweight Sass function that determines whether a number is integer or not.

## Motivation

Unfortunately, at the time of writing, [Sass](http://sass-lang.com/) has no way of telling an integer from a fraction – they are both of `number` type.

This lightweight Sass function utilises the native functionality of Sass to determine whether a given value is an integer or not.

## Getting Started

### Prerequisites

This Sass function runs on Sass version 3.1.0 or higher. It has no dependencies and can be used in any kind of Sass code.

The code is currently published on [npm](https://www.npmjs.com/), a package manager for [Node.js](https://nodejs.org/en/), so make sure both of them are installed on your computer for easy use. You can download an installer for your operating system on the [Downloads page of Node.js](https://nodejs.org/en/download/).

### Installing

#### Via [npm](https://www.npmjs.com/)

In order to get a copy, all you need to do is install the package in your own [npm](https://www.npmjs.com/) project.

```
npm install sass-is-int
```

After this, the source will be downloaded into the project's `node_modules` folder. From there, you can simply include the code in your own codebase using Sass' `@import` directive.

If your project depends on Sass to create CSS code, it is recommended to save this package in your project's `package.json` file.

```
npm install sass-is-int --save-dev
```

However, if you happen to use this code in a project which is for instance a Sass framework and you want to include this work in that framework, save the package as a dependency.

```
npm install sass-is-int --save
```

#### Copying the source

Although I personally do not recommend doing this, but you can simply download the source file from this repository and use it in your project that way. Note however, that [npm](https://www.npmjs.com/) makes updating packages a breeze and you should probably use it anyway.

## Usage

### Parameters

`is-int()` expects one parameter of any type. You can pass one directly:

```scss
p {
    @if is-int(42) {
        color: orange;
    }
}
```

Because the expression evaluates to true, the output is as follows:

```css
p {
    color: orange;
}
```

Or you can pass the function a variable:

```scss
$number: 42;

p {
    @if is-int($number) {
        color: orange;
    }
}
```

Which in this case outputs:

```css
p {
    color: orange;
}
```

### Return values

There are three different return values that the function can produce:

* The function returns `true` if the parameter is of `number` type and an integer.
* The function returns `false` if the parameter is of `number` type but not an integer.
* The function returns `null` if the parameter is not of `number` type.

It is important to note that the function returns `null` only if the type of the parameter is not number – neither an integer nor a fraction –, but because `null` is a falsey value, you should probably check for specific return values.

If you are certain that your parameter is a number, you can use the shorter syntax of Sass:

```scss
//Import the partial source file.
@import 'sass-is-int';

$int: 1;
$float: 1.5;
$string: string;

.int {
    @if is-int($int) {
        color: red;
    }
    @else {
    	color: blue;
    }
}

.float {
    @if is-int($float) {
        color: red;
    }
    @else {
    	color: blue;
    }
}

.string {
    @if is-int($string) {
        color: red;
    }
    @else {
    	color: blue;
    }
}
```

The above compiles to:

```css
.int {
    color: red;
}

.float {
    color: blue;
}

.string {
    color: blue;
}
```

However, if you need to make sure your parameter's type is of number, you can use Sass' longer syntax and check for exact return values:

```scss
//Import the partial source file.
@import 'sass-is-int';

$int: 1;
$float: 1.5;
$string: string;

.int {
    @if is-int($int) == true {
        color: red;
    }
    @if is-int($int) == false {
        color: blue;
    }
    @if is-int($int) == null {
        color: green;
    }
}

.float {
    @if is-int($float) == true {
        color: red;
    }
    @if is-int($float) == false {
        color: blue;
    }
    @if is-int($float) == null {
        color: green;
    }
}

.string {
    @if is-int($string) == true {
        color: red;
    }
    @if is-int($string) == false {
        color: blue;
    }
    @if is-int($string) == null {
        color: green;
    }
}
```

The above compiles to:

```css
.int {
    color: red;
}

.float {
    color: blue;
}

.string {
    color: green;
}
```

### Example

The actual problem I wanted to solve and created this function for was generating grid classes. I used percentage-based width values in the grid classes and in order to avoid calculation issues in modern browsers, CSS `calc()` functions were used. But for backwards compatibility, plain old percentage values were also kept in the stylesheet.

In a widely-used 12 column setup, using percentage width values, a column spanning 4 of the 12 available columns would have a width of ⅓, which equals to roughly 33.3%. In order to make that calculation easier for the browser, `calc(100% / 12 * 4)` is a better value for the `width` property.

In order to generate these classes, I used a simple `@for` directive:

```scss
@for $i from 1 through 12 {
    .grid-#{$i} {
        width: 100% / 12 * $i;
        width: calc(100% / 12 * #{$i});
    }
}
```

And this compiles to:

```css
.grid-1 {
    width: 8.33333%;
    width: calc(100% / 12 * 1);
}

.grid-2 {
    width: 16.66667%;
    width: calc(100% / 12 * 2);
}

.grid-3 {
    width: 25%;
    width: calc(100% / 12 * 3);
}

.grid-4 {
    width: 33.33333%;
    width: calc(100% / 12 * 4);
}

.grid-5 {
    width: 41.66667%;
    width: calc(100% / 12 * 5);
}

.grid-6 {
    width: 50%;
    width: calc(100% / 12 * 6);
}

.grid-7 {
    width: 58.33333%;
    width: calc(100% / 12 * 7);
}

.grid-8 {
    width: 66.66667%;
    width: calc(100% / 12 * 8);
}

.grid-9 {
    width: 75%;
    width: calc(100% / 12 * 9);
}

.grid-10 {
    width: 83.33333%;
    width: calc(100% / 12 * 10);
}

.grid-11 {
    width: 91.66667%;
    width: calc(100% / 12 * 11);
}

.grid-12 {
    width: 100%;
    width: calc(100% / 12 * 12);
}
```

The problem here was, that some of those CSS `calc()` functions are completely unnecessary. The numbers that are integers are unnecessary to be translated into `calc()` functions. This is one example where a Sass function that checks for integers could be useful.

Using `is-int()`, the above example Sass code's output can be simplified and optimized as follows:

```scss
//Import the partial source file.
@import 'sass-is-int';

@for $i from 1 through 12 {
    .grid-#{$i} {
        width: 100% / 12 * $i;
        @if is-int(100% / 12 * $i) == false {
            width: calc(100% / 12 * #{$i});
        }
    }
}
```

And this compiles to:

```css
.grid-1 {
    width: 8.33333%;
    width: calc(100% / 12 * 1);
}

.grid-2 {
    width: 16.66667%;
    width: calc(100% / 12 * 2);
}

.grid-3 {
    width: 25%;
}

.grid-4 {
    width: 33.33333%;
    width: calc(100% / 12 * 4);
}

.grid-5 {
    width: 41.66667%;
    width: calc(100% / 12 * 5);
}

.grid-6 {
    width: 50%;
}

.grid-7 {
    width: 58.33333%;
    width: calc(100% / 12 * 7);
}

.grid-8 {
    width: 66.66667%;
    width: calc(100% / 12 * 8);
}

.grid-9 {
    width: 75%;
}

.grid-10 {
    width: 83.33333%;
    width: calc(100% / 12 * 10);
}

.grid-11 {
    width: 91.66667%;
    width: calc(100% / 12 * 11);
}

.grid-12 {
    width: 100%;
}
```

Notice how the classes `.grid-3`, `.grid-6`, `.grid-9` and `.grid-12` are now correctly missing the secondary and in those cases unnecessary `width` properties with a CSS `calc()` value as opposed to the first output.

That is because the Sass `@if` directive evaluates to `true`, since `25`, `50`, `75` and `100` are all integers.

## Contributing

Questions and feedback are welcome. If you have anything to add, want to correct something in the README, or just want to start a discussion about this project, feel free to [open an issue on GitHub](https://github.com/pentzzsolt/sass-is-int/issues).

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/pentzzsolt/sass-is-int/tags). 

## Authors

* **Zsolt Pentz** - *Initial work* - [pentzzsolt](https://github.com/pentzzsolt)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

## Acknowledgments

* [Legends tell](https://stackoverflow.com/questions/10669351/test-if-value-is-an-integer-in-sass) that the wonderful [Chris Eppstein](https://twitter.com/chriseppstein) is the original author of this solution. He's awesome and you should follow him on Twitter.