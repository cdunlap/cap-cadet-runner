# CAP Cadet Runner

> A tool to make tracking cadets' mile laps and time a little easier. Built for my local [Civil Air Patrol](http://gocivilairpatrol.com) squadron. Free for anybody to use!

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

# Live Site
The site is running live and can be used at http://cap-cadet-runner.surge.sh. No data is stored or sent to any server, this project is entirely client-side and works on all modern devices: phones, tablets, laptops, etc.

## How to use
 * Enter the required number of laps around your mile track
 * Click/tap "Add Cadet" for as many cadets that are running
 * Enter cadet names in the inputs on each row
 * Press the play button to start the timer (when you tell your cadets to "GO")
 * Every time they make a lap, tap the clock next to their name (blue button)
 * Once a cadet has completed the required number of laps, their row will turn green and the lap button will disable
 
The timer can be paused by clicking/tapping the pause button, and reset by clicking/tapping on the refresh button next to the timer (in blue).

Cadets can be deleted by clicking/tapping on the trash can next to their name. **WARNING**: It does _not_ confirm deletion!

To clear a cadet's lap times, press the eraser next to their name. **WARNING**: It does _not_ confirm erase!
