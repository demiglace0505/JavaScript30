## 2 - CSS + JS Clock

> **Important concepts learned**
>
> - CSS transform
> - CSS transition-timing-function
> - Date object and its methods
> - setInterval

___

To rotate a clock hand, CSS [transform](https://www.w3schools.com/cssref/css3_pr_transform.asp) property with rotate value is used. [transform-origin](https://www.w3schools.com/cssref/css3_pr_transform-origin.asp) is then used at 100% to make the hand pivot at the right most side.

For an added eye candy and visual effect, CSS transition-timing-function property was used to adjust the speed of transition, by using a cubic-bezier value.

```css
    .hand {
      width: 50%;
      height: 6px;
      background: black;
      position: absolute;
      top: 50%;
      transform-origin: 100%;
      transform: rotate(90deg);
      transition: all 0.05s;
      transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
    }
```

To make the second hand tick every second, setInterval was used.

```javascript
setInterval(setDate, 1000)
```

Then, the logic for ticking the hands are written in a setDate function. This instantiates a [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) object and uses the date object's getSeconds, getMinutes and getHours method to get the current seconds minutes and hour. The time is converted to base 100 by dividing with number of ticks and multiplying by 360. 90 is added to offset the 90 degrees rotation in the css of the hand class.

```javascript
    const setDate =() => {
      const now = new Date();

      const secondsInDegrees = (now.getSeconds() / 60 * 360) + 90;
      secHand.style.transform = `rotate(${secondsInDegrees}deg)`;

      const minsInDegrees = (now.getMinutes() / 60 * 360) + 90;
      minHand.style.transform = `rotate(${minsInDegrees}deg)`;

      const hoursInDegrees = (now.getHours() / 12 * 360) + 90;
      hourHand.style.transform = `rotate(${hoursInDegrees})`
    }
```

