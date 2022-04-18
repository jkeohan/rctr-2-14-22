# React & Shopify

## Learning Objectives

- Explore some of the Front End tech that drives Shopify 
- Create a form using Shopify React Component Library **Polaris**
- Extend the form using **react-form** hook from Shopify's **Quilt** repo
- Refactor the form to include translations using **Quilts react-i18n** hook

## How Shopify Has Embraced React

Read some Shopify Dev Blog articles and come up with a summary. 

## Working With Shopify Polaris

Polaris is a design system built to help both Shopify and 3rd party developers create a consistent look and feel when building apps for our merchants.  One feature of the Polaris design system that we will be working with today is their Component library, which provides the following benefits:

- Components are flexible enough to meet diverse needs
- All Components meet accessibility standards and are responsive to any screen or device
- Shopify provides a well-documented public interface with guidelines and conventions

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min
<br>

Let's take a closer look at the [Polaris](https://polaris.shopify.com/) documenation.

<hr>

#### Starter Code

Here is the [Starter CodeSandbox](https://codesandbox.io/s/login-form-starter-polaris-duhck8?file=/src/components/FormPolaris.js) that we will be working with during this lesson.  It contains an existing form which we will rebuild using the **Polaris Form Component** and supporting Polaris styling layout Components.

### Form Component

Since were going to rebuild the existing form using Shopify Components let's first take a look at the [Polaris Form Component](https://polaris.shopify.com/components/forms/form#all-examples). 

The documenation provides a CodeSandbox link to begin working with the Component which we can see contains all the functionality required to work with a form, including **state** and **handler** methods.  

<img src="https://screenshot.click/30-47-l4pja-txyc4.png" />

The layout of the form will need some work but for now let's copy/paste this into our exising file and then configure our App to import and render the Component. 

### Missing AppProvider

Instead of rendering the Form as was displayed in the example we are instead presented with the following error: 

<img src="https://screenshot.click/30-50-5a75n-hmzpg.png">

The message indicates that our app must be wrapped in an **AppProvider** Component so let's take a look at the **[App provider docs](https://polaris.shopify.com/components/structure/app-provider#navigation)** and see what this entails. 

Looking at the example it's clear the **AppProvider** wraps the parent level **Page** Component and is also provided an **i18n** prop that is passed some configuration options.  

We won't concern ourselves just yet with the **i18n** prop but let's import the provider so we can start working with the Form. 

To do this we will import the **AppProvider** into **App** and render it as the top level Component.  

<img src="https://i.imgur.com/AU4nsWr.png" width="500px"/>

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

#### Solution CodeSandbox

Here is the **[Solution CodeSandbox](https://codesandbox.io/s/login-form-solution-polaris-veyw5g)**

### Working With Shopify's React-Form Package

Since working with Forms is common in the **Admin** tool at Shopify, their developers took it one step further and created an entire **React-Form** npm pacakge that does much of the heavy lifting.  The package is one of many which are included in their **Quilt Repo**.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min
<br>

Let's take a closer look at the publicly available [Quilt](https://github.com/Shopify/quilt) repository of packages and then we a deeper dive into the [react-form](https://github.com/Shopify/quilt) package.

<img src="https://screenshot.click/30-34-e4e5r-mysts.png" width=500/>

<hr>

### Initial Form

In order to demo **react-form** without rebuilding the template, we've incorporated our previous Polaris Form Component along with a few changes. We've also gone ahead and imported **react-form** as a dependency. 

<img src="https://i.imgur.com/FVdoQpg.png" width="300px"/>


This package exports a variety of hooks for all things form state but the quickest way to get up and running is with the following hooks: 

- **useField**: used for handling the state and validations of an input field.
- **useForm** : used for handling all state logic

Let's first import the hooks from the react-form library.

```js
import {
  useField,
  useForm,
} from "@shopify/react-form";
```




#### useForm

Let's start with **useForm** as it's used for handling all state logic. There are several fields we can work with but for now let's focus on the following:

- **fields**: manages the form fields 
- **submit**: replaces the handleSubmit function and handles onSubmit
- **reset**: rests the form once submitted
<!-- 
<img src="https://screenshot.click/30-05-meguy-b75v1.png"> -->

**useForm** requires that we pass it a configuration object that contains a **fields** key and **onSubmit** function.  Let's also add a console.log so we can confirm when the form has been submitted. 
```js
  const { fields, submit} = useForm({
    fields: {
      email: '',
      password: ''
    },
    async onSubmit(form) {
      console.log('onSubmit - form', form);
      return { status: 'success' };
    }
  });
```

Now we need to replace the existing values with the ones we have just instantiated. 

Both the **onSubmit** event listener and **TextField** Components need to be updated. 

```js
<Form onSubmit={submit}>
    <FormLayout>
    <div>
        <TextField placeholder="Email Address" {...fields.email} />
        <TextField placeholder="Password" {...fields.password} />
    </div>
    //...additonal code
    </FormLayout>
</Form>
```

We can confirm that the **onSubmit** function is working by clicking on the **Submit** button and looking at the console.

 ```js
onSubmit - form {email: "", password: ""}
 ```

### useField Hook

If we type into the fields we will notice that the values aren't being captured.  That's because we need the help of the **useField** hook.  

```js
      email: useField({
        value: "",
      }),
      password: useField({
        value: "",
      })
```

Now if we type into the inputs we can see that the text is being rendered in the UI. 

<img src="https://i.imgur.com/X5ydZb7.png" widht="300px"/>

We can also confirm in the console that those values are being captured by the form when we click **Submit**.

```js
onSubmit - form {email: "joe@gmail.com", password: "password"}
```

#### Resetting Form 

When working with a form one thing that we need to do is clear the fields once the **Form** has been submitted.  We can do this by making use of the the **reset** function from **useForm** and calling it in **onSubmit**. 


```js
export default function ReactPolarisForm() {
  const { fields, submit, reset} = useForm({
    fields: {
      email: useField({
        value: "",
      }),
      password: useField({
        value: "",
      })
    },
    async onSubmit(form) {
      console.log('onSubmit - form', form);
      reset()
      return { status: 'success' };
    }
  });
```

#### Validating Fields

Now that we have the basic form functionality working let's add some validation. **useForm** provides the following validation:

- notEmpty - confirms the field has input
- lengthMoreThan - confirms the field meets a certain length criteria

To make use of these setting we will need to import them from **react-form**. 

```js
import {
  useField,
  useForm,
  notEmpty,
  lengthMoreThan
} from '@shopify/react-form';
```

 Applying these validations to **useField** requires that we add a new **validate** key and include an array of validations. 

```js
fields: {
  email: useField({
    value: '',
    validates: [
      notEmpty('field is required'),
      lengthMoreThan(3, 'Email must be more than 3 characters')
    ]
  }),
  password: useField({
    value: '',
    validates: [
      notEmpty('field is required'),
      lengthMoreThan(3, 'Password must be more than 8 characters')
    ]
  })
}
```

### Adding Translations

Shopify is an international company with merchants joining the platform from all over the world.  In order to accommodate this internationalization Shopify has created a **react-i18n** library which can be configured to provide a certain level of translations.  
<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min

<br>

Let's take a closer look at the [react-i18n](https://polaris.shopify.com/) library in the **Quilt** repo. 

<img src="https://i.imgur.com/2a7pdR0.png"/>

<hr>

We've gone ahead and imported the library so we can jump right in.  

<img src="https://i.imgur.com/vYZhl45.png" width="300px"/>

#### I18nContext.Provider

This library requires a provider component which supplies i18n details to the rest of the app, and coordinates the loading of translations. Somewhere near the "top" of your application, render a **I18nContext.Provider** component. This component accepts an **I18nManager** as the value prop, which allows you to specify the global i18n properties. 

One thing to note is the I18nContext.Provider will pass context to App so we will opt to configure the provider as the very top of our application in **index.js**. 

Here we will import both **I18nContext** and **I18Manager**.
```js
import { I18nContext, I18nManager } from "@shopify/react-i18n";
```

Then we will need to define our current locale.  For the sake of this demo we will hard code it but in a production this would be set dynamically.

```js
import { I18nContext, I18nManager } from "@shopify/react-i18n";

const locale = "es";

const i18nManager = new I18nManager({
  locale,
  onError(error) {}
});
```

Let's now enable the **i18nContext.Provider** and pass the **i18Manager**. 
```js
import { I18nContext, I18nManager } from "@shopify/react-i18n";

const locale = "es";

const i18nManager = new I18nManager({
  locale,
  onError(error) {}
});

const rootElement = document.getElementById("root");
ReactDOM.render(
  <I18nContext.Provider value={i18nManager}>
    <App />
  </I18nContext.Provider>,
  rootElement
);
```

#### The useI18n Hook

With our context in place let's configure App to enable translations and pass it down to it's children. This requires that we first import the **useI18n** hook and define a fallback language.

```js
import { useI18n } from '@shopify/react-i18n';
import en from '../translations/en.json';
```

Inside the App component lets instantiate the **useI18n** hook.  The hook returns both an **i18n** value and a **ShareTranslations** Component. 

```js
const [i18n, ShareTranslations] = useI18n({
  id: 'Translations',
  fallback: en,
  translations(locale) {
    return import(`../translations/${locale}.json`);
  }
});
```

#### Using Translations 

We must now configure every child Component to consume the translations by importing the **i18n** hook. Let's go to **ReactForm** Component to import and instantiate the **i18n** hook. 

```js
import { useI18n } from "@shopify/react-i18n";

export default function ReactPolarisForm() {
  const [i18n] = useI18n();
  //...rest of code
}
```

Let's make use of the translations for the **Login** header and **placeholder** text in the **TextField** Components.

```js
<Card sectioned title={i18n.translate('Translations.heading')}>

<TextField
  placeholder={i18n.translate('Translations.email')}
  {...fields.email}
/>
<TextField
  placeholder={i18n.translate('Translations.password')}
  {...fields.password}
/>
```

### Additional Resources 

- [Lost in Translations: Bringing the World to Shopify](https://shopify.engineering/lost-in-translations)
- [Building a Data Table in Polaris](https://shopify.engineering/building-data-table-component-react)
