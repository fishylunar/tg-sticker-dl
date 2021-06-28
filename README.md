# tg-sticker-dl
Sticker downloader for https://telegramchannels.me

## Guide
Simply open up DevTools and paste in and run the following script when viewing a sticker page.

#### Example sticker page
https://telegramchannels.me/stickers/s-moodfox

### Raw JS (Inject in console)
```javascript
// TelegramChannels.me Sticker downloader

// Download functiom
async function downloadImage(imageSrc, fileName) {
  const image = await fetch(imageSrc)
  const imageBlog = await image.blob()
  const imageURL = URL.createObjectURL(imageBlog)

  const link = document.createElement('a')
  link.href = imageURL
  link.download = fileName
  document.body.appendChild(link)
  link.click()
  document.body.removeChild(link)
}


// Get Stickers
let stickers = [...document.getElementsByClassName("has-background-light has-radius has-padding has-fixed-size sticker-container")]

// For each sticker
stickers.forEach(sticker => {

// Get info from the currently selected htmlObject
let title = sticker.children[0].title.replace(", Telegram Sticker","").replace("#","")
let url = sticker.children[0].href

// Basic console output
console.log(title + "\n" + url)

// Actually download the image
downloadImage(url, title)
})
```
