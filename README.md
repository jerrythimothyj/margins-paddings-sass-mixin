# margins-paddings-sass-mixin
A sass mixin to create a bunch of margin and padding classes

## Description
We have developed a lot of projects where we needed a list of margins and paddings on each block and element. Why don't we create those classes with the help of sass-mixins and use those classes directly in the template files.

[Demo](https://plnkr.co/edit/6IndCd?p=preview) - Click the link for the code for creating a bunch of margin and padding classes 

### Implementation
* First, lets create a mixin which creates a css class like this:
```
.p-l-10 {
    padding-left: 10px;
}
```
It has a className, styleName, counter and unit.
```
#{$className + $i} { 
    #{$styleName}: #{$i + $unit};
}
```


* Now, we have to define how many such classes and the offset we require:
```
$max: 50;
$offset: 5;
```

* Lets say, we want to create padding from 0 to 50px, so we need a loop which does the job:
```
$i: 0;
@while $i <= $max {
    $i: $i + $offset;
}
```

* Combining all the above we get a nice juicy mixin:
```
$max: 50;
$offset: 5;
$unit: 'px'; // Feel free to change the unit.

@mixin list-loop($className, $styleName) {
  $i: 0;
  @while $i <= $max {
    #{$className + $i} { 
      #{$styleName}: #{$i + $unit};
    }
    $i: $i + $offset;
  }
}

@include list-loop('.p-l-', 'padding-left');

// Terrible name for mixin by the way.

```

This gives the CSS output:
```
.p-l-0 {
  padding-left: 0px;
}

.p-l-5 {
  padding-left: 5px;
}

.p-l-10 {
  padding-left: 10px;
}

.p-l-15 {
  padding-left: 15px;
}

.p-l-20 {
  padding-left: 20px;
}

.p-l-25 {
  padding-left: 25px;
}

.p-l-30 {
  padding-left: 30px;
}

.p-l-35 {
  padding-left: 35px;
}

.p-l-40 {
  padding-left: 40px;
}

.p-l-45 {
  padding-left: 45px;
}

.p-l-50 {
  padding-left: 50px;
}
```

* Similarly, we can create:
```
// Margins
@include list-loop('.m-t-', 'margin-top');
@include list-loop('.m-r-', 'margin-right');
@include list-loop('.m-b-', 'margin-bottom');
@include list-loop('.m-l-', 'margin-left');
@include list-loop('.m-x-', 'margin');

// Paddings
@include list-loop('.p-t-', 'padding-top');
@include list-loop('.p-r-', 'padding-right');
@include list-loop('.p-b-', 'padding-bottom');
@include list-loop('.p-l-', 'padding-left');
@include list-loop('.p-x-', 'padding');
```

### Output

![alt text](http://jerrythimothy.bigjapps.com/margins-paddings-sass-mixin/output.png)

Notice the padding-left: 50px near Bulbasaur...