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

* `true`
* `false`
* `null`

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

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Zsolt Pentz** - *Initial work* - [pentzzsolt](https://github.com/pentzzsolt)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* [Legends tell](https://stackoverflow.com/questions/10669351/test-if-value-is-an-integer-in-sass) that the wonderful [Chris Eppstein](https://twitter.com/chriseppstein) is the original author of this problem. He's awesome and you should follow him on Twitter.