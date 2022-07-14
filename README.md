# preact-dialog

Hook and component to use html [dialog](https://developer.mozilla.org/en-US/docs/Web/API/HTMLDialogElement) with (p)react.  
No build tool needed, just [preact](https://github.com/preactjs/preact) and [hyperscript tagged markup (htm)](https://github.com/developit/htm).

[See an example :arrow_right:](https://thinkawitch.github.io/preact-dialog/)

---

### Usage Example


```js
function App() {
    return html`
        <${DialogContextProvider}>
            <div class="card">
                <${DemoComponent} />
            </div>
            <${DialogConfirm} />
            <${DialogAlert} />
            <${DialogPrompt} />
        <//>
    `;
}

function DemoComponent() {
    const { confirm } = useDialogConfirm();
    const { alert } = useDialogAlert();
    const { prompt } = useDialogPrompt();
    const doConfirm = async () => {
        const isConfirmed = await confirm({ message: 'Delete this item?'});
        console.log('confirm answer', isConfirmed)
    }
    const doAlert = async () => {
        const res = await alert({ message: 'Some warning to let you know!'});
        console.log('alert answer', res)
    }
    const doPrompt = async () => {
        const [isConfirmed, value] = await prompt({ message: 'Enter your name', promptValue: 'John Smith'});
        console.log('prompt answer', isConfirmed, 'value', value)
    }
    return html`
        <div class="card-body">
            <button class="btn btn-success" onClick=${doConfirm}>confirm</button>
            <button class="btn btn-warning ms-3" onClick=${doAlert}>alert</button>
            <button class="btn btn-info ms-3" onClick=${doPrompt}>prompt</button>
        </div>
    `;
}
```

---

### Helpful examples

The `preact-dialog` made with help of:  
[Plain javascript dialog usage](https://css-tricks.com/replace-javascript-dialogs-html-dialog-element/)  
[Custom modal with react](https://devrecipes.net/custom-confirm-dialog-with-react-hooks-and-the-context-api/)
