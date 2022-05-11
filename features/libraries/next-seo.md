# Next SEO

### Introduction

Next.js provides a repeatable method for handling output to the `<head>` element using the `<Head>` [component](https://nextjs.org/docs/api-reference/next/head). However, SEO data and its many varied shapes (openGraph, Twitter etc) can be fiddly to deal with.\
\
Next SEO provides a number of helper components to handle the data structures.

### Example Usage

{% hint style="info" %}
Taken from the docs
{% endhint %}

#### Add SEO to Page

Then you need to import `NextSeo` and add the desired properties. This will render out the tags in the `<head>` for SEO. At a bare minimum, you should add a title and description.

**Example with just title and description:**

```tsx
import { NextSeo } from 'next-seo';

const Page = () => (
  <>
    <NextSeo
      title="Simple Usage Example"
      description="A short description goes here."
    />
    <p>Simple tUsage</p>
  </>
);

export default Page;
```

#### Add Product Data

By importing one of Next SEO JsonLd components we are able to insert sturctured output for product data.

```tsx
import { ProductJsonLd } from 'next-seo';

const Page = () => (
  <>
    <h1>Product JSON-LD</h1>
    <ProductJsonLd
      productName="Executive Anvil"
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      description="Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height."
      brand="ACME"
      color="blue"
...
```

