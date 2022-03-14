# React Giphy App

Let's build a react giphy app!

![giphy-fun](https://i.imgur.com/DrAlUbT.png)



Here is a [working version of the basic Giphy App](https://pl515.csb.app/)

#### Your task is

* Go to the Giphy docs [HERE](https://developers.giphy.com/docs/), _read_ them
* Create an account and get your Free API key.

* Diagram your App:
  * What components will you have?
  * Where would state "live"?
  * Where would you setup  `useEffect`?
  * Where do you need to pass props?
  * Where do you need to make the API call?

#### 🚀 Completion looks like

* Minimum of the following 3 components: **App (already present), Gif and Form.**
* A single gif should rendered when the page initially loads (think ComponentDidMount)
* On submission of the form make another API call update state with the new Gif
* If the form is submitted with text then search for that type of Giph
* If the form is submitted with no text than search for a random Giph

#### Bonus - Add Context

* Create a new context in App and have the Giph Component consume it.

Here is a working version with **[Context Added](<https://udt5gq.csb.app/>
)**

#### Bonus - Add History

* Create a side list of all the previous Giphs that have been retrieved
* Allow the user to click on any of them and display it in the main section
