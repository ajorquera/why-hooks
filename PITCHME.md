<img src="https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg" alt="react-logo" width="300"/>

# Why Hooks? 

Note:
* Take this presentation as a "grain of salt". Im not trying to force change but maybe to "Start a conversation on it".
* This is the way react and the community are headed. 
* That is something we could take advantage and apply in our own projects. As I understand we do use it, but maybe not enough

---

# Why?

Issues in react 2018
* Wrapper hell
* Syntax confusion
* Reusability in components
* Classes are hard for humans and machines

----

## Wrapper Hell

* Higher Order Components HOC
* Render Props

> A picture is worth a thousand words

<img src="https://miro.medium.com/max/1400/0*abdiidcjyscMpxwD" alt="wrapper-hell" width="200"/>

---- 

## Syntax confusion 
* React is lying to us - Renderless components

---- 

## Reusability in components
* It can be difficult to reuse logic in class components

Note: 
* Mixins used to be an option, but react team went away from it

---- 

## Classes are hard for humans and robots
* this
* stateless functions components -> class components
* compiler issues 

---

### React hooks in one 10s

<video controls width="400">
    <source src="https://video.twimg.com/tweet_video/DqsCilOU0AAoS7P.mp4" type="video/mp4">
</video>

---

# Coding time
Where can we apply hooks in our projects

* Transforming Class Components into hooks
* Modals (let's see it)

----

#### Modals
Now, we are doing something like this

```jsx
const MyView = (props) => {
    const [isContactModalOpen, setIsContactModalOpen] = useState(false);
    const [isWorkspaceModalOpen, setIsWorkspaceModalOpen] = useState(false);
    const [isConfirmModalOpen, setIsConfirmModalOpen] = useState(false);

    return (
        <div>
            <button onClick={() => setIsContactModalOpen(true)}>Open Contact</button>
            <button onClick={() => setIsWorkspaceModalOpen(true)}>Open Add Workspace</button>
            <button onClick={() => setIsConfirmModalOpen(true)}>Open DeleteWorkspace</button>

            <Modal title="Contact Form" open={isContactModalOpen} onClose={() => setIsContactModalOpen(false)}>
                {(props) => <ContactForm onClose={props.onClose} >
            </Modal>

            <Modal open={isWorkspaceModalOpen} onClose={() => setIsWorkspaceModalOpen(false)}>
                {(props) => <AddWorkspace onClose={props.onClose} data={someData} >
            </Modal>

            <Modal open={isConfirmModalOpen} onClose={() => setIsConfirmModalOpen(false)}>
                {(props) => <ConfirmModal onClose={props.onClose} >
            </Modal>
        </div>
    );
};
```

Note: 
* For simplicity, I wont explain every aspect of it
* There are a few modals in portal-app and sometimes a view can manage multiple modals
* Modal is lying to us
* A lot of boilerplate 

----

```jsx
const MyView = (props) => {
   const [openContactModal, close] = useModal(ContactForm, {title: 'Contact Form'});
   const [openWorkspaceModal] = useModal(AddWorkspace);
   const [openConfirmModal] = useModal(ConfirmModal);

    return (
        <div>
            <button onClick={openContactModal}>Open Contact</button>
            <button onClick={openWorkspaceModal}>Open Add Workspace</button>
            <button onClick={openConfirmModal}>Open DeleteWorkspace</button>
        </div>
    );
};
```

Note: 
* We dont manage the state, the hook does
* We dont need to make the component part of the react tree









