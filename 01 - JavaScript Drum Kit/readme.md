## 1 - Javascript Drum Kit

> **Important concepts learned**
>
> - HTML data-* attributes
> - keydown  and transitionend event listeners
>

___

HTML data- attributes was used to embed custom data to our elements. These data attributes are used to hook up keyboard keys along with an audio element.

```javascript
<div data-key="65" class="key">
  <kbd>A</kbd>
  <span class="sound">clap</span>
</div>

...
<audio data-key="65" src="sounds/clap.wav"></audio>
```

Event listeners are added to the window object on **keydown** trigger. Attribute selector works the same way in javascript as in css. In this instance, I used the keyCode key of the event object to select an audio element and the corresponding div with the key class. 

The audio can be played using the play method of the audio object. Then, the class playing is added to the pressed key to add the styles.

```javascript
  window.addEventListener('keydown', (e) => {
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`)
    const key = document.querySelector(`.key[data-key="${e.keyCode}"]`)
    console.log(audio)
    //<audio data-key="65" src="sounds/clap.wav"></audio> -> on "A" press
    audio.currentTime = 0 // rewind to start
    audio.play();
    key.classList.add('playing')
```

To make the key revert to its normal styling after being pressed, a **transitionend** event listener for each key was added. The removeTransition function is run once the event is fired. Note that function syntax has to be used for **this** to point to the key object, whereas the arrow syntax makes **this** point to the window object.

```javascript
    function removeTransition(e) {
      // console.log(e)
      if (e.propertyName !== 'transform') {
        return // skip if not a transform
      }
      console.log(this) // this = key
      this.classList.remove('playing')
    }
    ...

	const keys = document.querySelectorAll('.key')
    keys.forEach( (key) => {
      key.addEventListener('transitionend', removeTransition)
    })
```

