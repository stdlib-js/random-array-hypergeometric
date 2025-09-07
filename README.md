<!--

@license Apache-2.0

Copyright (c) 2024 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# Hypergeometric Random Numbers

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Create an array containing pseudorandom numbers drawn from a [hypergeometric][@stdlib/random/base/hypergeometric] distribution.



<section class="usage">

## Usage

To use in Observable,

```javascript
hypergeometric = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/random-array-hypergeometric@umd/browser.js' )
```

To vendor stdlib functionality and avoid installing dependency trees for Node.js, you can use the UMD server build:

```javascript
var hypergeometric = require( 'path/to/vendor/umd/random-array-hypergeometric/index.js' )
```

To include the bundle in a webpage,

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/random-array-hypergeometric@umd/browser.js"></script>
```

If no recognized module system is present, access bundle contents via the global scope:

```html
<script type="text/javascript">
(function () {
    window.hypergeometric;
})();
</script>
```

#### hypergeometric( len, N, K, n\[, options] )

Returns an array containing pseudorandom numbers drawn from a [hypergeometric][@stdlib/random/base/hypergeometric] distribution.

```javascript
var out = hypergeometric( 10, 20, 10, 7 );
// returns <Float64Array>
```

The function has the following parameters:

-   **len**: output array length.
-   **N**: population size.
-   **K**: subpopulation size.
-   **n**: number of draws.
-   **options**: function options.

The function accepts the following `options`:

-   **dtype**: output array data type. Must be a [real-valued data type][@stdlib/array/typed-real-dtypes] or "generic". Default: `'float64'`.

By default, the function returns a [`Float64Array`][@stdlib/array/float64]. To return an array having a different data type, set the `dtype` option.

```javascript
var opts = {
    'dtype': 'generic'
};

var out = hypergeometric( 10, 20, 10, 7, opts );
// returns [...]
```

#### hypergeometric.assign( N, K, n, out )

Fills an array with pseudorandom numbers drawn from a [hypergeometric][@stdlib/random/base/hypergeometric] distribution.

```javascript
var zeros = require( '@stdlib/array-zeros' );

var x = zeros( 10, 'float64' );
// returns <Float64Array>

var out = hypergeometric.assign( 20, 10, 7, x );
// returns <Float64Array>

var bool = ( out === x );
// returns true
```

The function has the following parameters:

-   **N**: population size.
-   **K**: subpopulation size.
-   **n**: number of draws.
-   **out**: output array.

#### hypergeometric.factory( \[N, K, n, ]\[options] )

Returns a function for creating arrays containing pseudorandom numbers drawn from a [hypergeometric][@stdlib/random/base/hypergeometric] distribution.

```javascript
var random = hypergeometric.factory();

var out = random( 10, 20, 10, 7 );
// returns <Float64Array>

var len = out.length;
// returns 10
```

If provided distribution parameters, the returned generator returns random variates from the specified distribution.

```javascript
var random = hypergeometric.factory( 20, 10, 7 );

var out = random( 10 );
// returns <Float64Array>

out = random( 10 );
// returns <Float64Array>
```

If not provided distribution parameters, the returned generator requires that distribution parameters be provided at each invocation.

```javascript
var random = hypergeometric.factory();

var out = random( 10, 20, 10, 7 );
// returns <Float64Array>

out = random( 10, 20, 10, 7 );
// returns <Float64Array>
```

The function accepts the following `options`:

-   **prng**: pseudorandom number generator for generating uniformly distributed pseudorandom numbers on the interval `[0,1)`. If provided, the function **ignores** both the `state` and `seed` options. In order to seed the underlying pseudorandom number generator, one must seed the provided `prng` (assuming the provided `prng` is seedable).
-   **seed**: pseudorandom number generator seed.
-   **state**: a [`Uint32Array`][@stdlib/array/uint32] containing pseudorandom number generator state. If provided, the function ignores the `seed` option.
-   **copy**: `boolean` indicating whether to copy a provided pseudorandom number generator state. Setting this option to `false` allows sharing state between two or more pseudorandom number generators. Setting this option to `true` ensures that an underlying generator has exclusive control over its internal state. Default: `true`.
-   **dtype**: default output array data type. Must be a [real-valued data type][@stdlib/array/typed-real-dtypes] or "generic". Default: `'float64'`.

To use a custom PRNG as the underlying source of uniformly distributed pseudorandom numbers, set the `prng` option.

```javascript
var minstd = require( '@stdlib/random-base-minstd' );

var opts = {
    'prng': minstd.normalized
};
var random = hypergeometric.factory( 20, 10, 7, opts );

var out = random( 10 );
// returns <Float64Array>
```

To seed the underlying pseudorandom number generator, set the `seed` option.

```javascript
var opts = {
    'seed': 12345
};
var random = hypergeometric.factory( 20, 10, 7, opts );

var out = random( 10, opts );
// returns <Float64Array>
```

The returned function accepts the following `options`:

-   **dtype**: output array data type. Must be a [real-valued data type][@stdlib/array/typed-real-dtypes] or "generic". This overrides the default output array data type.

To override the default output array data type, set the `dtype` option.

```javascript
var random = hypergeometric.factory( 20, 10, 7 );

var out = random( 10 );
// returns <Float64Array>

var opts = {
    'dtype': 'generic'
};
out = random( 10, opts );
// returns [...]
```

#### hypergeometric.PRNG

The underlying pseudorandom number generator.

```javascript
var prng = hypergeometric.PRNG;
// returns <Function>
```

#### hypergeometric.seed

The value used to seed the underlying pseudorandom number generator.

```javascript
var seed = hypergeometric.seed;
// returns <Uint32Array>
```

If the `factory` method is provided a PRNG for uniformly distributed numbers, the associated property value on the returned function is `null`.

```javascript
var minstd = require( '@stdlib/random-base-minstd-shuffle' ).normalized;

var random = hypergeometric.factory( 20, 10, 7, {
    'prng': minstd
});

var seed = random.seed;
// returns null
```

#### hypergeometric.seedLength

Length of underlying pseudorandom number generator seed.

```javascript
var len = hypergeometric.seedLength;
// returns <number>
```

If the `factory` method is provided a PRNG for uniformly distributed numbers, the associated property value on the returned function is `null`.

```javascript
var minstd = require( '@stdlib/random-base-minstd-shuffle' ).normalized;

var random = hypergeometric.factory( 20, 10, 7, {
    'prng': minstd
});

var len = random.seedLength;
// returns null
```

#### hypergeometric.state

Writable property for getting and setting the underlying pseudorandom number generator state.

```javascript
var state = hypergeometric.state;
// returns <Uint32Array>
```

If the `factory` method is provided a PRNG for uniformly distributed numbers, the associated property value on the returned function is `null`.

```javascript
var minstd = require( '@stdlib/random-base-minstd-shuffle' ).normalized;

var random = hypergeometric.factory( 20, 10, 7, {
    'prng': minstd
});

var state = random.state;
// returns null
```

#### hypergeometric.stateLength

Length of underlying pseudorandom number generator state.

```javascript
var len = hypergeometric.stateLength;
// returns <number>
```

If the `factory` method is provided a PRNG for uniformly distributed numbers, the associated property value on the returned function is `null`.

```javascript
var minstd = require( '@stdlib/random-base-minstd-shuffle' ).normalized;

var random = hypergeometric.factory( 20, 10, 7, {
    'prng': minstd
});

var len = random.stateLength;
// returns null
```

#### hypergeometric.byteLength

Size (in bytes) of underlying pseudorandom number generator state.

```javascript
var sz = hypergeometric.byteLength;
// returns <number>
```

If the `factory` method is provided a PRNG for uniformly distributed numbers, the associated property value on the returned function is `null`.

```javascript
var minstd = require( '@stdlib/random-base-minstd-shuffle' ).normalized;

var random = hypergeometric.factory( 20, 10, 7, {
    'prng': minstd
});

var sz = random.byteLength;
// returns null
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   If PRNG state is "shared" (meaning a state array was provided during function creation and **not** copied) and one sets the underlying generator state to a state array having a different length, the function returned by the `factory` method does **not** update the existing shared state and, instead, points to the newly provided state array. In order to synchronize the output of the underlying generator according to the new shared state array, the state array for **each** relevant creation function and/or PRNG must be **explicitly** set.
-   If PRNG state is "shared" and one sets the underlying generator state to a state array of the same length, the PRNG state is updated (along with the state of all other creation functions and/or PRNGs sharing the PRNG's state array).

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/console-log-each@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/random-array-hypergeometric@umd/browser.js"></script>
<script type="text/javascript">
(function () {

// Create a function for generating random arrays originating from the same state:
var random = hypergeometric.factory( 20, 10, 7, {
    'state': hypergeometric.state,
    'copy': true
});

// Generate 3 arrays:
var x1 = random( 5 );
var x2 = random( 5 );
var x3 = random( 5 );

// Print the contents:
logEach( '%f, %f, %f', x1, x2, x3 );

// Create another function for generating random arrays with the original state:
random = hypergeometric.factory( 20, 10, 7, {
    'state': hypergeometric.state,
    'copy': true
});

// Generate a single array which replicates the above pseudorandom number generation sequence:
var x4 = random( 15 );

// Print the contents:
logEach( '%f', x4 );

})();
</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

* * *

## See Also

-   <span class="package-name">[`@stdlib/random-base/hypergeometric`][@stdlib/random/base/hypergeometric]</span><span class="delimiter">: </span><span class="description">hypergeometric distributed pseudorandom numbers.</span>

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2025. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/random-array-hypergeometric.svg
[npm-url]: https://npmjs.org/package/@stdlib/random-array-hypergeometric

[test-image]: https://github.com/stdlib-js/random-array-hypergeometric/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/random-array-hypergeometric/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/random-array-hypergeometric/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/random-array-hypergeometric?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/random-array-hypergeometric.svg
[dependencies-url]: https://david-dm.org/stdlib-js/random-array-hypergeometric/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/random-array-hypergeometric/tree/deno
[deno-readme]: https://github.com/stdlib-js/random-array-hypergeometric/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/random-array-hypergeometric/tree/umd
[umd-readme]: https://github.com/stdlib-js/random-array-hypergeometric/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/random-array-hypergeometric/tree/esm
[esm-readme]: https://github.com/stdlib-js/random-array-hypergeometric/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/random-array-hypergeometric/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/random-array-hypergeometric/main/LICENSE

[@stdlib/random/base/hypergeometric]: https://github.com/stdlib-js/random-base-hypergeometric/tree/umd

[@stdlib/array/typed-real-dtypes]: https://github.com/stdlib-js/array-typed-real-dtypes/tree/umd

[@stdlib/array/uint32]: https://github.com/stdlib-js/array-uint32/tree/umd

[@stdlib/array/float64]: https://github.com/stdlib-js/array-float64/tree/umd

</section>

<!-- /.links -->
