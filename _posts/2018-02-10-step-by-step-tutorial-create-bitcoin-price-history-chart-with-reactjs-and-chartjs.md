---
title: "[Step-by-Step] Tutorial - Bitcoin Price Chart with Reactjs and Chart.js"
layout: post
tags:
- reactjs
- chartjs
- bitcoin-chart
- tutorial
- web-development
categories:
- tutorial
- reactjs
description:
- "[Step-by-Step] Tutorial - Bitcoin Price Chart with Reactjs and Chart.js"
og_image: btc-chart1.png
---

![](/btc-chart1.png)

<br />
Hello, welcome to super fast and simple ReactJS tutorial. 

In this tutorial, we will do a simple data fetching and show it in chart using Chart.js.

And data we will fetch is **Bitcoin price from last 30 days** from Coindesk API.
<br />
```javascript
const URL = 'https://api.coindesk.com/v1/bpi/historical/close.json'
```
<br />
First, create project:
  
```bash
create-react-app bitcoin-chart && cd bitcoin-chart
```
<br />

The default project structure of `create-react-app`:
<br />
```
bitcoin-chart
├── node_modules/ 
├── public/ 
├── src/ 
│   └── App.css
│   └── App.js
│   └── App.test.js
│   └── index.css
│   └── index.js
│   └── logo.svg
│   └── registerServiceWorker.js
├── package.json
├── README.md 
```
<br />
All project coding must be in `src/` directory. So, let' s start development server by running:
```bash
yarn start
```
<br />
![](/btc-chart2.png)
<br /><br /><br />
Now, let's try to fetch data. In `src/App.js`, delete old code and replace with:
<br />
```jsx
// src/App.js

import React, {Component} from 'react'

const URL = 'https://api.coindesk.com/v1/bpi/historical/close.json'

export default class App extends Component {
    state = {
        btcPrices: {}
    }

    componentDidMount() {
        // call this function after a compoment is mounted.
        this.getBTCPrice()
    }

    getBTCPrice() {
        return fetch(URL)
            .then(r => r.json())
            .then(data => {
                // show response data in console
                console.log('data: ', data)
                this.setState({ btcPrices: data.bpi })
            })
            .catch(err => {
                console.log(err)
            })
    }

    render() {
        return (
            <div>App.js</div>
        )
    }

}
```
<br />

We had updated `btcPrices` state by `this.setState({ btcPrices: data.bpi })` which `data.bpi` is object of bitcoin prices from last 30 days.
<br /> <br />
And in browser console, we should see fetched response data:
<br />
```shell
data: {bpi: {…}, disclaimer: "This data was produced from the CoinDesk Bitcoin Price Index. BPI value data returned as USD.", time: {…}}
```
<br/>

Next, we have to show our fetched data in chart. In this post, we will use Chart.js library. So, add it to our project by:
<br />
```bash
yarn add chart.js
```
<br />

Show Chart by add below code to `src/App.js`:
```jsx
// src/App.js
.
.
.
import Chart from 'chart.js'
// css file
import './App.css'
.
.
.
    componentDidMount() {
        // call this function after a compoment is mounted.
        this.getBTCPrice()
        this.showGraph()
    }


    showGraph() {
        // bitcoin price object
        let btcPrices = this.state.btcPrices

        // label array for using in Chart.js
        let tmp_label = []
        // data array for using in Chart.js
        let tmp_data = []
        Object.keys(btcPrices).forEach(d => {
            tmp_label.push(d)
            tmp_data.push(btcPrices[d])
        })

        const canvas = this.refs.myChart
        const ctx = canvas.getContext('2d')

        return new Chart(ctx, {
            // line type chart
            type: 'line',
            data: {
                // adapt tmp_label here
                labels: tmp_label,
                datasets: [{
                    label: 'Last 30days BTC Price',
                    // adapt tmp_label here
                    data: tmp_data,
                    backgroundColor: [
                        'rgba(255, 99, 132, 0.2)'
                    ],
                    borderColor: [
                        'rgba(255,99,132,1)',
                    ],
                    borderWidth: 1
                }]
            },
            options: {
                tooltips: {
                    callbacks: {
                        // we custom tooltip that will show we point mouse data node in chart
                        label: (tooltipItem, data) => {
                            return 'Price: ' + tooltipItem.yLabel + ' USD';
                        }
                    }
                },
                legend: {
                    display: false
                },
                scales: {
                    yAxes: [{
                        ticks: {
                            beginAtZero: true
                        }
                    }]
                }
            }
        })
    }
		
		
    // update getBTCPrice() function
    getBTCPrice() {
        return fetch(URL)
            .then(r => r.json())
            .then(data => {
                // show response data in console
                console.log('data: ', data)
                this.setState({ btcPrices: data.bpi })
								// add here to update Graph chart when finish fetching data
                this.showGraph()
            })
            .catch(err => {
                console.log(err)
            })
    }
		
	 
    render() {
        return (
            <div className="App">
                <h2>30 Days Bitcoin Price History Chart</h2>
                <br/>
                <canvas id="myChart" ref="myChart" />
            </div>
        )
    }

```
<br />

And add a bit style in `src/App.css`:
```css
.App {
    padding: 30px;
    text-align: center;
}

canvas.chartjs-render-monitor#myChart {
    display: block !important;
    width: 100% !important;
}
```
<br />

That's all of code. Run server by `yarn start` and see result:
<br /> <br />
![](/btc-chart4.png)
<br /><br />
Yey! We got it.
<br />

Now, we come to the end of this tutorial. You can see project code in [Github repository](https://github.com/kphetdev/bitcoin-chart). This is just simple repository. So, PR is always welcome.
<br /><br />
Finally, since this is my first blog post in this site. I might have any error. So, please feel free to comment what you think about this post. Thank you!