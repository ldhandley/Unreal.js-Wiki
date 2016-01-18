```js
let request = require('request')
let cheerio = require('cheerio')
const url = 'http://somenice-url.com'
request('GET',url,{res:'string'}).then(result => {
    let $ = cheerio.load(result)            
    let text = $('div').text()
    page.find('page').SetText(text)
}) 
```