# React & Shopify

## Learning Objectives

- Explore some of the Front End tech that drives Shopify 
- Create a form using Polaris, Shopify React Component Library
- Extend the form using **react-form** hook from Shopify's Quilt repo
- Refactor form to include translations using **react-i18n** hook

## How Shopify Has Embraced React

## Working With Shopify Polaris

Polaris is a design system built to help both Shopify and 3rd party developers create a consistent look and feel when building apps for our merchants.  One feature of the Polaris design system that we will be working with today is their Component library, which provides the following benefits:

- comonents are flexible enough to meet diverse needs
- comonents have a well-documented public interface with guidelines and conventions
- components meet accessibillity standards and are responsive to any screen or device

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min
<br>

Let's take a closer look at the [Polaris](https://polaris.shopify.com/) documenation.

<hr>

#### Starter Code

Here is the [Starter CodeSandbox](https://codesandbox.io/s/login-form-starter-polaris-duhck8?file=/src/components/FormPolaris.js) that we will be working with during this lesson.  It contains an existing form which we will rebuild using the Polaris Form Component and supporting styling Polaris layout Components. 

### Form Component

Since were going to rebuild the existing form using Shopify Components let's first take a look at the [Polaris Form Component](https://polaris.shopify.com/components/forms/form#all-examples). 

The documenation provides a CodeSandbox link to begin working with the Component which we can see contains all the functionality required to work with a form, including **state** and **handler** methods.  

<img src="https://screenshot.click/30-47-l4pja-txyc4.png" />

The layout of the form will need some work but for now let's copy/paste this into our exising file and then configure our App to import and render the Component. 

### Missing AppProvider

Instead of rendering the Form as was displayed in the example we are instead presented with the following error: 

<img src="https://screenshot.click/30-50-5a75n-hmzpg.png">

The message indicates that our app must be wrapped in an **AppProvider** Component so let's take a look at the **[App provider docs](https://polaris.shopify.com/components/structure/app-provider#navigation)** and see what this entails. 

Looking at the example it's clear the **AppProvider** wraps the parent level **Page** Component and is also provided an **i18n** prop that is passed some configuration options.  We won't concern oursevles just yet with the **i18n** prop but let's import the provider so we can start working with the Form. 

To do this we will import it into **index.js** which is the highest level of our application. 

<img src="https://screenshot.click/30-13-cvklu-p12gr.png" />

### Rebuilding The Existing Form

With our Form in working condition we can start making the edits needed to recreate the existing Form design and functionality. 

First let's clean up the form and remove any reference to signing up for the newsletter.  This requires we do the following:
- Remove the **Checkbox** Component and it's corresponding import
- Remote the HandleNewsLetterChange function
- delete setNewsLetter() from the **handleSubmit** function
- delete the existing state for **newsLetter**


Now let's setup the form to include the additional functionality needed to support a new password input field which includes the following: 

- adding new state values of **[password, setPassword]**
- add a new handler called **handlePasswordChange**
- update **handleSubmit** to clear the password field
- add/configure the **TextField** Component

Here is what the code required to support our new TextField looks like:

<img src="https://screenshot.click/30-31-1s2ne-uzd67.png">

Now let's add the TextField. All we need to do is copy the existing TextField and rename several of the properties.  Since were also looking to rebuild the existing form we will need to remove the **label** and **helpText** properties and add **placeholder** text for both inputs. 

With all those changes in place our Form should now look like the following: 

<img src="https://screenshot.click/30-37-wx9a1-phlp7.png" />

### Styling The Form

Although we could always opt to use our own CSS to apply styling there are several additional Shopify Components that we can use to bring us closer to the original design. The ones we will work with now can be found under their corresponding categories:

- Action:
    - [Button](https://polaris.shopify.com/components/actions/button#navigation)

- Layout:
    - [Card](https://polaris.shopify.com/components/structure/card#navigation)
    - [Page](https://polaris.shopify.com/components/structure/page#navigation)


**Button**

Lets start with the **Button** Component since that is part of the form.  If we take a look at the docs we can see that we can make use of the following styling options:

- **primary** - changes the color to green
- **fullWidth** - expands the button to full width

```js
 <Button primary fullWidth>Submit</Button>
```

**Card**

It's time to wrap our Form so that it contains the additional white spacing around it and also includes the **Login** text located at the top of the form. 

To do this we will import a **Card** Component and make use of the following props:

- **sectioned** - auto wrap content in section
 - **title** - adds title content for the card

```js
import { Button, Form, FormLayout, TextField, Card } from "@shopify/polaris";

```

```js
<Card sectioned title="Login">
    <Form onSubmit={handleSubmit}>
    // ...rest of code
</Card>
```

Once we add the Card along with it's props we can see the title and additional spacing.  If we take a look in Dev Tools we can see all the structural Components. 

<img src="https://screenshot.click/30-03-ue0yl-b48u8.png">

**Page**

Let's import the **Page** Component which will wrap the entire **Card** and include the following property:

- **narrowWidth**

```js
<Page narrowWidth>
    <Card sectioned title="Login">
        <Form onSubmit={handleSubmit}>
        ...rest of code
        </Form>
    </Card>
</Page>
```

Here is how the Form should look with all the changes we've made:

<img src="https://screenshot.click/30-22-hfpty-n4cfl.png" />

### Last of the Styling

Form is coming along and requires only a few more subtle tweaks to make it look like our original design.  Two things we still need to implement: 

- remove the space between the inputs
- decrease the width

Let's first take a look in Dev Tools and see where the additional spacing is coming from for the input fields and button.  

<img src="https://screenshot.click/30-35-cr4kn-8kd0a.png" />

It's clear that the **Polaris-FormLayout__Item** is where the margin is being assigned. These elements are direct children of the **FormLayout** Component so if we were to add an extra **div** around the inputs then that would be become the **Polaris-FormLayout__Item** and margin would only be applied once.

```js
<FormLayout>
    <div>
        <TextField
```

This seems to do the trick.  Now all we need to do is add a few lines of custom CSS to decrease the width even more and center the Form. 

If we take a look at Dev Tools we shoudl see the setting for **Polaris-Page** and if we assign the following custom CSS to **styles.css** our form will be complete.

```css
.Polaris-Page {
    max-width: 420px;
}
```

**[Solution CodeSandbox](https://codesandbox.io/s/login-form-starter-polaris-duhck8?file=/src/components/FormPolaris.js)**

### Working With Shopify's React-Form Package

Since working with Forms is a common occurence in the **Admin** tool at Shopify, their developers took it one step further and created an entire **React-Form** npm pacakge The package is one of many which are included in their **Quilt library**.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min
<br>

Let's take a closer look at the publicly available [Quilt](https://github.com/Shopify/quilt) library and then specifically the [react-form](https://github.com/Shopify/quilt) package.

<img src="https://screenshot.click/30-34-e4e5r-mysts.png" />

<hr>

### Initial Form

In order to demo **react-form** without rebuilding the template, we've incorporated our previous Polaris Form Component along with a few changes. 

Let's first take a look at the hooks we've imported from **react-form**.

```js
import {
  useField,
  useForm,
  notEmpty,
} from "@shopify/react-form";
```

These hooks will import all the functionality needed to replace **state** and the **handlerFunctions** which were included in the previous **Polaris Form** starter code. 

#### useForm

Let's start with **useForm**. 

<img src="https://screenshot.click/30-05-meguy-b75v1.png">
