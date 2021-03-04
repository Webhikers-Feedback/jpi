# JPI Feedback

Hi there and thanks a lot for the great and fast work on JPI. We really appreciate your time, you efforts and your clean code so far.

Nearby I have some little Feedback, that is actually not related to JPI, but related to all future projects, so you would just need to read this once and then you know it forever.

## Bootstrap CSS Variables

We'd like to use the bootstrap system as much as we can (one reason for this is that we need to integrate some of our nuxt projects with a shop system that we've built for nuxt and it needs to be compatible).
therefore, please follow our [very short tutorial](https://github.com/Webhikers-Docs/nuxt-bootstrap-doc) how to setup and include Bootstrap System in Nuxt, so you can use the bootstrap variables everywhere in your code: [Find the tutorial here](https://github.com/Webhikers-Docs/nuxt-bootstrap-doc).

Now you will be able to use the bootstrap variables in you code like so:

In your `@/components/Homepage/Banner.vue

instead of this:

```vue
<style>
  .content {
    &__title{
      color: map-get($colors, white);
    }
  }
</style>
```

You can now use the bootstrap scss variable (and all other bootstrap variables)

```vue
<style>
  .content {
    &__title{
      color: $white;
    }
  }
</style>
```

In the above short tutorial you will also find how you can overwrite bootstrap variables.

## 2. Bootstrap Components

**generally, please work with as much bootstrap components as you can. It helps reduce the amount of required css code and saves time.**

## 3. Responsive

We found, that it keeps the code simplest and cleanest if we do mobile-first apps. 
That means, you can write all code as you need it just for mobile and do not put it into any media query. And everything that needs to be different on desktop, you can put into a desktop media query.

**Please use the bootstrap colums to make it responsive for desktop, tablet and mobile, but write extra css ONLY FOR DESKTOP.**

You can write CSS just so it looks good on mobile and then add extra css for desktop. No need to write extra css for tablet. Please use Iphone SE in the chrome devtools as the smallest breakpoint.

Of course, we also want to use the bootstrap media queries and therefore there is a very handy scss mixin from bootstrap `@include media-breakpoint-up(lg)`

In your `@/components/Homepage/Banner.vue

So, instead of this:
```vue
<style lang="scss" scoped>
  .content {
    &__group-btn{
      @media (max-width: 525px) {
        flex-direction: column;
      }
    }
  }
</style>
```

Write it like this

```vue
<style lang="scss" scoped>
  .content {
    &__group-btn{
      flex-direction: column;
      @include media-breakpoint-lg(lg){
        flex-direction: row; //or whatever you need here
      }
    }
  }
</style>
```

To keep the responsive code clean and readable, please create a complete new css block for the responsive code, like this:

In your `@/components/Homepage/Banner.vue

So, instead of this:
```vue
<style lang="scss" scoped>
  .content {
    &__group-btn{
      flex-direction: column;
      @include media-breakpoint-lg(lg){
        flex-direction: row; //or whatever you need here
      }
    }
  }
</style>
```

Write it like this

```vue
<style lang="scss" scoped>

  //here goes all regular css code
  .content {
    &__group-btn{
      flex-direction: column;
    }
  }
  
  //here goes all dekstop css code, nicely sorted
  @include media-breakpoint-lg(lg){
    .content {
      &__group-btn{
        flex-direction: row;
      }
    }
  }  
</style>
```

## 4. Scoping

I really love the fact that you're using the Element Block Modifier System for your css. Awesome!!

Since we need to include some of your apps, into our own shop app, we need to ensure compatibility.

1. Please make sure that all `<style></style>` tags you write are always `scoped`. You already did it so far, which is great! This is just a short notification, that it's very important to keep this convention.
2. There is only one css rule that is not only allowed, but required to be set globally (without scoping), which is the font-family. So pleas declare the font family for all headings and body globally in a global.css file.
This way, you can prevent yourself from redeclaring the font family everytime in your css and also you make you site campatible with our systems. Please note that nothing else is allowed to be declared globally.
