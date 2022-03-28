# Context Building

![Building Lab](https://png.pngtree.com/png-vector/20190219/ourlarge/pngtree-set-vector-cartoon-illustration-of-an-abstract-urban-large-modern-buildings-png-image_322118.jpg)

You are the mailroom clerk in a ten story building. Use Context and the useContext hook you need to deliver mail throughout the building.

### Delivering Mail

To send mail down the building, setup an instance of context and its provider in the higher floor and use useContext to receive it on the lower floor.

To send mail up the building, create some state to hold the mail and send the sendState function to the desired floor using context, then run the function in a useEffect call to send the outbox back up the building.

### Starter Code

Here is the [CodeSandbox Starter](https://codesandbox.io/s/usecontext-lab-starter-go9h2) for this exercise to fork.

To see an example Look at Floor 6 who is sending mail to floor 5 and receiving mail from floor 5.

### Scheduled Mail Deliveries

- Floor 10 is sending mail to floor 1
- Floor 1 is sending mail to floor 9
- Floor 8 is sending mail to flor 2
- floor 2 is sending mail to floor 7
- floor 7 is sending mail to floor 10
- floor 9 is sending mail to floor 3
- floor 4 is sending mail to floor 8
