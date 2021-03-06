# Form
## Input Types
- text
- email
- tel ( friendly to the phone browser )
- radio

## Options
-  select
- radio
- checkbox

# CSS
## box
- padding
- marging
- border
- box-sizing: border-box;  It makes sure that the padding or marging of the element won't change it's original size 
## Float
- .clearFix 
```CSS
.clearFix: before,
.clearFix: after {
        content: "";
        display: table;
}
.clearFix: after {
        clear: both;
}
.clearFix {
    zoom: 1;
}
```
## Position
**absolute** : it will find his closest ancestor who ueses the relative position as his reference frame, if this ancestor does not exist, it will chosse navigator window as his reference frame.

**relative** : the refrence of the a relative position element is himself.

- z-index

## Color
- rgba(_,_,_,_); red, green, blue, alpha(transparent)

## Selector
- table tr : nth-child(2) {   }
- input[type=''email''] {   }
- :hover
- :focus

## Typography
- font-size
- font-weight
- font-style: italic
- letter-spacing: 4px
- word-spacing: 10px
- text-shadow: 2px 10px 0 #999999;
- text-transform: lowercase;
- text-decoration: none;
- text-align: justify;
- text-indent: 20px;
- line-height: 1.5;

## Custom fonts
```css
@font-face {
        font-family: 'nameOfFont';
        src: url('fonts/nameOfFont.eot');
        src: url('fonts/nameOfFont.eot?#iefix') format('embedded-opentype'),
               url('fonts/nameOfFont.woff') format('woff'),
               url('fonts/nameOfFont.ttf') format('truetype'),        
               url('fonts/nameOfFont.svg#pt_sansregular') format('svg');        
        font-weight: normal;
        font-style: normal;    
}
```
Don't forget to add the bold / italic version of the font too.

## Background Images
```CSS
background-imag: url('yourURL');
background-repeat: repeat-x;     'no-repeat'
background-position: center center; 
background-size: cover;
```
The first 3 line can write as below:
```CSS
background: #c2bbb1 url('yourURL') center center no-repeat;
```

## Gradient Background
```CSS
background-color: #e5e9dc; /* if the navigator doesn't support gradient, it will show this color*/
background-image: linear-gradient(to bottom, #e5e9dc, #FFF);
```

## CSS Sprites
- Used for ''icon" art
- Reduces number of HTTP requests (makes the site load quicker)



![Image of sprites](https://github.com/Xx-william/Study-Notes/blob/master/CSS/images/sprites.png)

**Html code**
```HTML
<nav class="ui-menu">
    <ul claa="group">
        <li class="ui-home"><a href="#">Home</a></li>
        <li class="ui-profile"><a href="#">Profile</a></li>
        <li class="ui-settings"><a href="#">Settings</a></li>
    </ul>
</nav>
```
**CSS code**
```CSS
.ui-menu a {
    display: block;
    width: 50px;
    height: 50px;
    background-image: url(yourURL);
    text-indent: -9999px; /* make the text invisable */
    background-repeat: no-repeat;
}
.ui-home a:hover {background-position: -50px 0;}
.ui-profile a {
    background-position:  0 -50px;
}
.ui-profile a:hover {background-position: -50px -50px;}
.ui-settings a {
    background-position: 0 -100px;
}
.ui-settings a:hover {background-position: -50px -100px;}
```
- - - - -
## Responsive Web Design
1. Meta tag in <head> section of HTML
    ```HTML
    <meta name="viewport" content="width=device-width, initial-scale=1">
    ````

2. Media queries ( conditional CSS )
    ```CSS
    @media screen and ( max-width: 700px ) {  /* if the mobiel device in smaller than 700px  the code below will be applied*/
        .main-area,
        .sidebar {
            width: auto;
            float: none;
        }        
    }
    ```   
    ```CSS
    @media screen and ( min-width: 1300px ) { /*if the screen is larger than 1300px, the code below will bw applied */
        /* CSS code */
    } 
    ```

## Responsive Grids

Insded of writing CSS file to crea a grids system, here i prefer to use [Bootstrap grids system](http://getbootstrap.com/css/#grid).

![Image of grid](https://github.com/Xx-william/Study-Notes/blob/master/CSS/images/bootstrap-grid.png)

- - - - -
## CSS3 Special Effects
### Box Shadow
```CSS
    .box-a {
        box-shadow: 10px 5px 5px #000; /* we can use rgba color to creat transparent shadow */
    }
    .box-b {
        box-shadow: inset 10px 5px 5px #000; /* this can create the inner box shadow */
    }
    .box-c {
         box-shadow: 10px 5px 5px #000 , inset 10px 5px 5px #000 ; /*this will create the inner shadow and outer shadow at the same time */ 
    }
```

### Rounded Corners
```CSS
    border-radius: 10px; /* 4 corners */
    border-radius: 10px 20px;   /* 1. left top and right bottom  2. right top and left bottom */
    border-radius: 10px 10px 25px 25px; /* 4 corners */
    border-radius: 10px/25px; /* horizonal radius / vertical radius */
    border-radius: 50%; 
```

### Transform

1. Rotate
    ```CSS
        .example {
            transform: rotate( 90deg ); /* rotate 90 degree */
        }
    ```
2. Scale
    ```CSS
        .example {
            transform: scale( 2 ); /* double the size of the .example */
        }
    ```
3. Skew
    ```CSS
        .example {
            transform: skewX( 50deg ) skewY( 50deg );
        }
    ```
4. Position ( origin & placement )
    ```CSS
    transform-origin: 0 0; /* set the reference point of the transform */
                                        /* 50% 50% by default */
    transform: translate( 100px, 40px ); /* use in animation purposes , if you want layout purpose , use position: relative*/
    ```
**When you want to use more than 1 transform at the same time, use space in the transform code**

### Transition
```CSS
.example {
    transition-property: color, background-color; /* transition-property: all */
    transition-duration: 2s;
    transition-timing-function: linear; /* ease-in, ease-out, ease-in-out; */
    
    transition: all 2s linear; 
}
```


**Example : whe cusor hover over the image, the description show up**
```CSS
.image-banner {
    position: relative;
    overflow: hidden;
}
.image-banner img {
    display: block;
}
.banner-description {
    position: absolute;
    transition-property: all;
    transition-duration: 1s;
    transform: translateY( 100% ); 
}
.image-banner:hover .banner-description {
    opacity: 1;
     transform: translateY( 0 ); 
}
```

### CSS Animation
**Bounce Animation**
```CSS
@keyframes yourAnimationName {
    0% {
        opacity: 0; /*invisable*/
        transform: translateY( -200% );
    }
    40% { 
        opacity: 0.5;
        transform: translateY( 0 );
    }
    55% {
        transform: translateY( -6px );
    }
    70% {
        opacity 1;
        transform: translateY( 0 );
    }
    85% {
        transform: translateY( -3px );
    }
    100% {
        transform: translateY( 0 );
    }
}
```
**Use Animation**
```CSS
.example {
    animation-name: yourAnimationName;
    animation-duration: 1s;
}
```
**Others**
```CSS
animation-delay: .5s; 
animation-fill-mode: forwards; /* after finish animation, make the element stays at the finish point*/
```

**Star Animation**
```CSS
@keyframes starAnimation {
    50% {
        transform: translateX( 150% ) scale( .5 );
    }
    75% {
        transform: translateX( 150% ) rotate( 180deg ) scale( .5 );
    }
    100% {
        transform : translateX ( 300% ) rotate( 180deg );
    }
}
```
**Use Animation**
```CSS
.star {
    animation: starAnimation 2s;
    animation-fill-mode: fowards;
    animation-iteration-count: infinite; /*the times that animation repeats*/
    animation-direction: alternate;
}
```
- - - - -


## Sass ( CSS Extension Language)
-  **Variables**
```Scss
$favoriteColor: #FFF;
.example {
    background-color: $facoriteColor;
}
```

- **Nesting**
```Scss
.site-header nav{
    ul {
        /*your codes here */
    }
    li {
        /* your codes here */
    }
    a {
        /*your codes here */
    }
}
```

- **Inheritance** / @extend
```Scss
.btn-b {
    @extend .btn-a;
    background-color: #000;
}
```
- **Splitting up code into smaller files** / @import
```Scss
@import 'header'; /*file name is  _header.scss  */
```
- **Minxin** /@mixin @include
Example 1:
```Scss
@mixin verticalGradient($fromColor, $toColor){
    background-image: linear-gradient(to bottom, $fromColor, $toColor);
}
.btn-b {
    @extend .btn-a;
    @include verticalGradient(blue, red);
}
```

Example 2:
```Scss
@mixin bp-babyBear {
    @media only screen and (max-width: 480px ) {
        @content;
    }
}
li {
    @include bp-babyBear {
        float: none;
        margin-right: 0;
        margin-bottom: 2px;        
    }
}

```

There is a community mixins that sharing the mixin.

- **Operators**


**Sass Frameworks**
- Compass
- Bourbon
- Susy

- - - - -
## Cross Browsers
### Feature Detection
[caniuse.com](http://www.caniuse.com)
**Modernizr** ( JavaScript library) : it will comunicate withe the browser and get all the type this browser supports, after that, it will add this type ( all types supported by this browser) into the < html class="" > label.

```CSS
html.cssanimations .box-a { /* if the browser support css animation */
    opacity: 0;
}
```












