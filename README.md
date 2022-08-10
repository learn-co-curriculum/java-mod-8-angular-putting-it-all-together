# Putting it All Together

## Learning Goals

- Use the topics you've learned so far to create a simple application.

## Create a Simple App

Let's create a very simple application that allows the user to enter a message
and "send" it to the application. We're putting "send" in quotes here because
we're not (yet) actually sending a message to anyone, but we are simulating the
sending action by updating our UI with the user's message.

Let's break down what this simple application needs to do:

1. Allow the user to enter a value for the "sender" and a value for the
   "message" from that sender
2. Allow the user to "send" that message
3. When that message is sent (hint: `onSendMessage`), add the message to the
   existing list of messages
4. When the list of messages is updated, update the display of messages on the
   UI

Let's go through the steps we need to execute in order to implement this
functionality:

1. Add variables in our model to hold the `senderName` and the `senderMessage`

```typescript
export class AppComponent {
  senderName = "";
  senderMessage = "";
  title = "flatiron-angular";
  // ...
}
```

2. Update our view to have input fields that are bound to the new variables in
   models using `ngModel`

```html
<p>Sender name: <input type="text" [(ngModel)]="senderName" /></p>
<p>Message: <input type="text" [(ngModel)]="senderMessage" /></p>
```

3. Modify our `onSendMessage()` function to use the values of `senderName` and
   `senderMessage`

```typescript
  onSendMessage() {
    let newMessage = {
      sender: this.senderName,
      message: this.senderMessage
    }
    this.messages.push(newMessage);
  }
```

4. Tie it all together by adding a button that calls the `onSendMessage()`
   function when it's clicked

```html
<div>
  <button (click)="onSendMessage()">Send Message</button>
</div>
```

Putting it all together with some very basic HTML formatting gives us the
following code in our `app.component.html` view:

```html
<div>
  <h1>Chat Application</h1>
  <h2>Send Message</h2>
  <p>Sender name: <input type="text" [(ngModel)]="senderName" /></p>
  <p>Message: <input type="text" [(ngModel)]="senderMessage" /></p>
  <div>
    <button (click)="onSendMessage()">Send Message</button>
  </div>

  <h2>Messages</h2>
  <div>
    <ul>
      <li *ngFor="let currentMessage of messages">
        {{currentMessage.sender}}: {{currentMessage.message}}
      </li>
    </ul>
  </div>
</div>
```

And the following code in our `app.component.ts` code:

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
})
export class AppComponent {
  senderName = "";
  senderMessage = "";
  title = "flatiron-angular";
  messages = [
    {
      sender: "Ludovic",
      message: "Latest message from Ludovic",
    },
    {
      sender: "Jessica",
      message: "Latest message from Jessica",
    },
  ];

  constructor() {
    console.log("Iniating angular AppCompnent class");
  }

  onSendMessage() {
    let newMessage = {
      sender: this.senderName,
      message: this.senderMessage,
    };
    this.messages.push(newMessage);
  }
}
```
